---
icon: elementor
---

# QuML Migration Notes - From V1.0 TO V1.1

## **Problem Statement:** <a href="#qumlmigrationnotes-fromv1.0tov1.1-problemstatement" id="qumlmigrationnotes-fromv1.0tov1.1-problemstatement"></a>

* inQuiry released v2 api’s in release-6.0.0 which works only with QuML version 1.1 and above. So If you need to use v2 api, the existing data having data as per QuML version 1.0 need to be migrated first.

## **Solution:** <a href="#qumlmigrationnotes-fromv1.0tov1.1-solution" id="qumlmigrationnotes-fromv1.0tov1.1-solution"></a>

* inQuiry released set of tools for QuML Migration (V1.0 to V1.1) in release-6.1.0.
* Below tools released as part of [release-6.1.0](https://inquiry.sunbird.org/use/release-notes/inquiry-release-v6.1.0)
  * [sync-tool](https://inquiry.sunbird.org/use/release-notes/inquiry-release-v6.1.0#sync-tool)
  * [quml-migrator](https://inquiry.sunbird.org/use/release-notes/inquiry-release-v6.1.0#question-and-question-set-service)
  * [questionset-republish](https://inquiry.sunbird.org/use/release-notes/inquiry-release-v6.1.0#question-and-question-set-service)

## **Migration Tools:** <a href="#qumlmigrationnotes-fromv1.0tov1.1-migrationtools" id="qumlmigrationnotes-fromv1.0tov1.1-migrationtools"></a>

#### **sync-tool:** <a href="#qumlmigrationnotes-fromv1.0tov1.1-sync-tool" id="qumlmigrationnotes-fromv1.0tov1.1-sync-tool"></a>

* It is an existing tool in Knowlg BB. Enhancement done for QuML Migration.
* A new command **migrateQuml** introduced for QuML migration requirement.
* This tool is used to generate migration event (kafka event) based on various criteria.
* Currently QuML 1.0 format nodes are not having metadata like **qumlVersion** & **schemaVersion**. So all nodes will be fetched which will not have qumlVersion & schemaVersion property.
* It is recommended to generate event for Image Node (e.g: Object Type QuestionImage or QuestionSetImage) separately.
* migrateQuml command can take below parameters:

| **Parameter** | **Description**                                                                                                                                                                                                                                                                                | **Mandatory/Optional** |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| --objectType  | <ul><li>Object Type Can be passed. e.g: Question or QuestionSet</li><li>Multiple ObjectType can be passed. e.g: --objectType Question,QuestionImage</li></ul>                                                                                                                                  | Mandatory              |
| --status      | <ul><li>More than one status can be passed. e.g: --status Draft,Review</li><li>It is recommended to migrate one status at a time. so that tracking would be easy</li><li>If any status is not passed, tool will consider all status available in the database</li></ul>                        | Optional               |
| --limit       | <ul><li>an integer value (multiple of 50) can be passed to control number of events to be generated at a time.</li><li>Generally this parameter should be used, if data volume is huge.</li><li>If no limit is passed, then the tool will generate events for all available objects.</li></ul> | Optional               |
| --delay       | <ul><li>time value in millisecond can be given to create gap between event generation for each batch (default batch size is 50)</li></ul>                                                                                                                                                      | Optional               |

**Sample Commands:**

| **Command**                                                                  | **Descriotion**                                                         |
| ---------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| migrateQuml --objectType Question --status Draft,Review --delay 2000         | Migrate All Question object which are in Draft or Review status         |
| migrateQuml --objectType Question --status Live --delay 2000                 | Migrate All Question object which are in Live status                    |
| migrateQuml --objectType QuestionImage --status Draft,Review --delay 2000    | Migrate All QuestionImage object which are in Draft or Review status    |
| migrateQuml --objectType QuestionSet --status Draft,Review --delay 2000      | Migrate All QuestionSet object which are in status Draft or Review      |
| migrateQuml --objectType QuestionSet --status Live --delay 2000              | Migrate All QuestionSet object which are in Live status                 |
| migrateQuml --objectType QuestionSetImage --status Draft,Review --delay 2000 | Migrate All QuestionSetImage object which are in Draft or Review status |

**quml-migrator:**

* quml-migrator is a flink job available in inQuiry [data-pipeline](https://github.com/Sunbird-inQuiry/data-pipeline/tree/release-6.1.0\_RC2) repo.
* This flink job will process migration event generated by **sync tool** (migrateQuml command)
* This flink job will perform all migration activity and stamp few additional metadata as below:
  * migrationVersion - a value which will indicate the status of migration. For more details, Please refer to Migration Version Table.
  * migrationError - In case of any error during migration
  * qumlVersion - value 1.1 will be stamped, only if migration success.
  * schemaVersion - value 1.1 will be stamped, only if migration success
* If the object/node status is **Live**, this job will send an event for **re-publish** post migration activity.
* The **re-publish** operation require another flink job **questionset-republish** to be deployed.
*   Performance of **quml-migrator** flink job can be optimised using below configuration parameter:\


    ```
    task {
          consumer.parallelism = {{ quml_migrator_consumer_parallelism }}
          parallelism = {{ quml_migrator_task_parallelism }}
          router.parallelism = {{ quml_migrator_router_parallelism }}
          question_migration.parallelism = {{ question_migration_parallelism }},
          questionset_migration.parallelism = {{ questionset_migration_parallelism }}
        }
    ```
* By default, all parameters are set to 1.

**questionset-republish:**

* questionset-republish is an existing flink job in inQuiry [data-pipeline](https://github.com/Sunbird-inQuiry/data-pipeline/tree/release-6.1.0\_RC2) repo which is enhanced for re-publish activity post QuML migration.
* This job will not consider any image node and only publish the current version (live one).

#### Migration Sequence: <a href="#qumlmigrationnotes-fromv1.0tov1.1-migrationsequence" id="qumlmigrationnotes-fromv1.0tov1.1-migrationsequence"></a>

**Step-1:** All Questions including visibility Parent/Default should be migrated first (all status).

* We can further split Question Migration based on different status, if the data volume is large.

**Step-2:** Migrate All QuestionSet having status other than Live.

**Step-3:** All QuestionSet having Live status, should be migrated.

#### Migration Steps: <a href="#qumlmigrationnotes-fromv1.0tov1.1-migrationsteps" id="qumlmigrationnotes-fromv1.0tov1.1-migrationsteps"></a>

**Step-1:** Execute below queries in neo4j graph database and save the output for later reference.

```
# Get All Question Object Count, Which need to be migrated
Match(n:domain) where n.IL_FUNC_OBJECT_TYPE IN ["Question", "QuestionImage"] and n.IL_SYS_NODE_TYPE="DATA_NODE" and n.qumlVersion is null and n.schemaVersion is null return n.IL_FUNC_OBJECT_TYPE as ObjectType,n.status as Status,count(n) as Count;

# Get All QuestionSet Object Count, Which need to be migrated
Match(n:domain) where n.IL_FUNC_OBJECT_TYPE IN ["QuestionSet", "QuestionSetImage"] and n.IL_SYS_NODE_TYPE="DATA_NODE" and n.qumlVersion is null and n.schemaVersion is null return n.IL_FUNC_OBJECT_TYPE as ObjectType,n.status as Status,count(n) as Count;
```

**Step-2:** Deploy Sync-tool and run below command to migrate the data.

* Migration Sequence has to be maintained for successful migration.
* You can execute any command from below table as per requirement (based on data).
* ```
  ## migrateQuml --objectType Question --status Draft,Review,Retired,Failed --delay 2000

  	-> Migrate all Question with status Draft,Review,Retired,Failed

  ## migrateQuml --objectType QuestionImage --status Draft,Review,Retired,Failed --delay 2000

  	-> Migrate all QuestionImage with status Draft,Review,Retired,Failed

  ## migrateQuml --objectType Question --status Live --delay 2000

  	-> Migrate all Question with Live status.

  ## migrateQuml --objectType QuestionSet --status Draft,Review,Retired,Failed --delay 2000

  	->  Migrate all QuestionSet with status Draft,Review,Retired,Failed

  ## migrateQuml --objectType QuestionSetImage --status Draft,Review,Retired,Failed --delay 2000

  	-> Migrate all QuestionSetImage with status Draft,Review,Retired,Failed

  ## migrateQuml --objectType QuestionSet --status Live --delay 2000

  	-> Migrate all QuestionSet with status Live.
  ```

**Step-3:** [Verify the migration status](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3351511041/QuML+Migration+Notes+-+From+V1.0+TO+V1.1#Migration-Verification%3A%5BhardBreak%5D).

#### **Migration Version Description:** <a href="#qumlmigrationnotes-fromv1.0tov1.1-migrationversiondescription" id="qumlmigrationnotes-fromv1.0tov1.1-migrationversiondescription"></a>

* We have different values for `migrationVersion` metadata which indicates different stages of QuML migration. Below table covers all possible values of `migrationVersion` indicating succes / failure states.

| **migrationVersion** | **Description**                                                  |
| -------------------- | ---------------------------------------------------------------- |
| 3.0                  | Migration successful, if Asset status is other than Live         |
| 3.1                  | Migration and republish both successful, if Asset status is Live |
| 2.1                  | Migration failed irrespective of status of the Asset.            |
| 2.2                  | Republish failed. Applicable only on Live status Asset           |
| 2.3                  | Migration skipped because of data validation issue               |

#### Migration Verification:  <a href="#qumlmigrationnotes-fromv1.0tov1.1-migrationverification" id="qumlmigrationnotes-fromv1.0tov1.1-migrationverification"></a>

*   Execute below queries in neo4j graph database and compare the result with pre-migration query (query executed in Step 1) result.

    ```
    # Get All Question Object Count, Which need to be migrated
    Match(n:domain) where n.IL_FUNC_OBJECT_TYPE IN ["Question", "QuestionImage"] and n.IL_SYS_NODE_TYPE="DATA_NODE" and n.qumlVersion is null and n.schemaVersion is null return n.IL_FUNC_OBJECT_TYPE as ObjectType,n.status as Status,count(n) as Count;

    # Get All QuestionSet Object Count, Which need to be migrated
    Match(n:domain) where n.IL_FUNC_OBJECT_TYPE IN ["QuestionSet", "QuestionSetImage"] and n.IL_SYS_NODE_TYPE="DATA_NODE" and n.qumlVersion is null and n.schemaVersion is null return n.IL_FUNC_OBJECT_TYPE as ObjectType,n.status as Status,count(n) as Count;
    ```
* If the count is Zero (0) for above query, Then Migration Process Completed Successfully. If not, then please check if quml-migrator job is still processing data or having any other issue.
* Once the count is Zero, you can execute below queries in neo4j graph database to see exact status of the migration.
* ```
  Match (n:domain) where n.IL_FUNC_OBJECT_TYPE IN ["Question", "QuestionImage"] and n.IL_SYS_NODE_TYPE="DATA_NODE" and n.migrationVersion>2.0 return n.IL_FUNC_OBJECT_TYPE as ObjectType,n.status as Status,count(n) as Count,n.migrationVersion as MigrationVersion,n.migrationError as MigrationError;

  Match (n:domain) where n.IL_FUNC_OBJECT_TYPE IN ["QuestionSet", "QuestionSetImage"] and n.IL_SYS_NODE_TYPE="DATA_NODE" and n.migrationVersion>2.0 return n.IL_FUNC_OBJECT_TYPE as ObjectType,n.status as Status,count(n) as Count,n.migrationVersion as MigrationVersion,n.migrationError as MigrationError;
  ```
* Output of above queries can be analysed based on migrationVersion and further action can be defined.
