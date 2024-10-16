---
icon: folder-open
---

# Sunbird-Lern-Code,-Flink-Jobs-and-Data-Products-

Lern BB has multiple components and most of the components have flink jobs, adhoc scripts and Data products spread across multiple GitHub repositories. The objective is bring all these under Lern BB space in GitHub and separate out the code into different component level repositories under Lern BB space.

### Proposed Structure:

[https://github.com/Sunbird-Lern](https://github.com/Sunbird-Lern) ([/github.com/Sunbird-Lern](https://github.com/Sunbird-Lern))

All independent repos in project-sunbird and sunbird-ed will move to new lern space. Other BB dependent repos remain in same place and a copy of the repos will be created in new Lern BB space except for devops, devops-private, flink jobs and dataproduct repos.

Queries and Concerns :

1. **Sunbird-utils** will move to Lern space.
2. What should be done to **sunbird-devops** related configurations and ES Mappings? For now we can continue to use sunbird-devops repo.
3. **Flink job configurations** will be in new lern data-pipeline repo and sunbird-devops-private repo
4. Should we move other jobs and scripts like druid job submitter, consumption reports and other jobs in to Lern or it can remain in current sunbird-data-products? Classify scripts and jobs and handover diksha specific jobs.
5. **Jenkins Jobs** specific to Lern need to be created
6. Check GitHub repo move with new name will retain the old history or not, if not move with current name and then change to new name. - move with new name will retain history.
7. How to deploy Ed in Lern **infra to test groups, notification and DiscussionForum** ? Till new sites are created for testing, setup sunbird-Ed and use it for testing
8. Update the **pod names** also as per repo/components - This will not happen in first phase- repo names and pod names will change in 2nd phase.

#### Jenkins and Devops-

* Lern
  * All lern related jobs will be newly created. These jobs will point to new repos and it will deploying into new Lern K8 cluster.

Need to move flink job configuration from sunbird-learning-platform, **to the lern data-pipeline repo.**

Later when devops repo is created in lern API and env will nove to that or to respective components

Sunbird-Lern/devops (Environment and API Configurations and ES Mappings)

Sunbird-Lern/devops-private

**Cassandra migration:**

**Sunbird-utils** will move inLern space. Cassandra cluster will remain same.

**ES:**

ES mappings will remain in sunbird-devops. ES cluster will remain same. Jobs will be separate.

**Redis:**

Redis cluster will remain same. Separate DBs are used.

**Postgres:**

Postgres cluster will remain same. Separate DBs are used.

**Graylog, Grafana, Keycloak, Superset, Druid, Azure** - clubbed as of now

**API Manager and nginx proxy** - separate setup for Lern

\[\[Lern BB repositories|Lern-BB-repositories]] Repositories details

\| | UserOrg Service | Batch Service | Notification Service | Groups Service | Discussion Forum | | **Core Code** - These repos will move to Lern space. |

1. sunbird-lms-service
2. sunbird-auth
3. sunbird-apimanager-util

“sunbird-lms-service” will change to “sunbird-userorg-service” in Phase2, not now. |

1. sunbird-course-service
2. sunbird-viewer-service
3. certificate-registry
4. cert-service

“sunbird-course-service” will change to “sunbird-batch-service” in Phase2, not now. |

1. sunbird-notification-UI ( move in Phase2, not now.)
2. sunbird-notification-service

|

1. groups-service

|

1. discussions-UI ( move in Phase2, not now.)
2. discussions-middleware
3. nodebb-plugin-sunbird-api
4. nodebb-plugin-sunbird-oidc
5. nodebb-plugin-azure-storage
6. nodebb-plugin-sunbird-telemetry
7. sunbird-nodebb

\| | **Data Products** - | Single **data-products** repo in Lern for all components./adhocscripts(scala/python/java) /jobs(reports/etl)

1. Geo report (stateadmingeoreport)
2. User-consent report( stateadminreport)
3. User declaration report
4. user details report
5. Cassandramigrator job
6. course status updater
7. collection reconcilation
8. coursebatch status updater
9. progressexhaustjob
10. responseexhaust
11. userinfoexhaust
12. course consumption
13. course enrolment
14. collectionsummaryjobv2

\| | **Flink Jobs** - | Single data-pipeline repo in Lern for all components. Jobs-core will be a copy in new repo. Later Obsrv will create a maven dependency for jobs-core.

1. Notification job
2. assessment aggregate updater
3. merge courses job
4. activity aggregate updater
5. certificate processor
6. collection-cert-pre-processor
7. colletion-certificate-generator
8. relation cache updater
9. enrolment-reconciliation

|

Batch service and KP flink jobs Approach and Estimation : \[\[Batch Service Code refactoring approach and Estimation|Batch-Service-Code-refactoring-approach-and-Estimation]]

Data Products separation Approach and Estimation : \[\[Migration of Data Products in Sunbird-LERN|Migration-of-Data-Products-in-Sunbird-LERN]]

**Notification Job migration** : \[\[SB-28322 Migrate notification samza jobs into flink and remove other jobs|SB-28322-Migrate-notification-samza-jobs-into-flink-and-remove-other-jobs]]

Merge Courses Job Migration: \[\[SB-28061 Migrate Merge-User-Courses samza to flink job|SB-28061-Migrate-Merge-User-Courses-samza-to-flink-job]]

**Remove existing samza job steps:**

1. Stop the notification-job, merge-user-course samza jobs in the hadoop dashboard
2. remove the tar.gz files from the server

### Current Structure:

1. **User Org Service**
   1. project-sunbird/sunbird-lms-service (UserOrg Service)
   2. project-sunbird/sunbird-auth ( Authentication - Keycloak SPI)
   3. project-sunbird/sunbird-apimanager-util (API Manager Util)
   4. Sunbird-Ed/sunbird-data-products (Report Jobs : Geo report, User-consent report)
   5. project-sunbird/sunbird-devops (Environment and API Configurations)
   6. project-sunbird/sunbird-utils/sunbird-cassandra-migration (Database setup)
   7. project-sunbird/sunbird-devops/ansible/roles/es-mapping (ES Mappings)
   8. project-sunbird/sunbird-data-pipeline (user-cache-updater-2.0)
2. **Notification Service**
   1. NavKumarV/sunbird-notification (Notification UI)
   2. project-sunbird/sunbird-notification-service (Notification Service)
   3. project-sunbird/sunbird-lms-jobs (Notification Job - Notification flink job details are \[\[here|SB-28322-Migrate-notification-samza-jobs-into-flink-and-remove-other-jobs]])
   4. project-sunbird/sunbird-devops (Environment and API Configurations)
   5. project-sunbird/sunbird-utils/sunbird-cassandra-migration (Database setup)
3. **Group service**
   1. Sunbird-Ed/SunbirdEd-portal (Groups UI)
   2. project-sunbird/groups-service ( Groups Service)
   3. project-sunbird/sunbird-devops (Environment and API Configurations)
   4. project-sunbird/sunbird-utils/sunbird-cassandra-migration (Database setup)
4. **Discussion Forum**
   1. Sunbird-Ed/discussions-UI (Discussions-UI)
   2. Sunbird-Ed/discussions-middleware
   3. Sunbird-Ed/nodebb-plugin-sunbird-api
   4. Sunbird-Ed/nodebb-plugin-sunbird-oidc
   5. Sunbird-Ed/nodebb-plugin-azure-storage
   6. Sunbird-Ed/nodebb-plugin-sunbird-telemetry
   7. project-sunbird/sunbird-nodebb
5. **Batch Service**
   1. project-sunbird/sunbird-course-service
   2. project-sunbird/sunbird-viewer-service
   3. project-sunbird/certificate-registry
   4. project-sunbird/cert-service
   5. project-sunbird/sunbird-data-pipeline

i. assessment aggregate updater job

```
1. project-sunbird/sunbird-learning-platform 


1. KP and  Learning platform Flink Job Configurations


1. Merge courses job(samza) for details visit [[here|SB-28061-Migrate-Merge-User-Courses-samza-to-flink-job]])




1. project-sunbird/knowledge-platform-jobs 


1. Activity aggregate updater flink job


1. Credential generator flink jobs


1. Certificate processor


1. Collection-cert-pre-processor


1. Colletion-certificate-generator




1. Relation cache updater


1. Enrolment-reconciliation





```

8\. **Data -products**

Sunbird-Ed/sunbird-data-products

/adhoc-scripts

a. userorgdatamigration

b. course data migration

c. course status updater

/data-products

/audit

a. assessmentscore correction

b. collection reconcilation

c. coursebatch status updater

/exhaust

a. progressexhaustjob

b. responseexhaust

c. userinfoexhaust

/job

a. course consumption

b. course enrolment

c. etbmetris

d. stateadminreport

e. stateadmingeoreport

f. collectionsummaryjobv2

g.assessmentcorrectionjob

\-/updater

a.Cassandramigrator job

/etl-jobs

/analytics

a. UserCacheIndexer.scala

/learner

b. GroupsServiceTablesMigration.scala

c. UserLookupMigration.scala

/pythonscripts

/consumption

a. content consumption (consumption of contents for last week and last 6 months as two report files)

b. ecg\_learning (trend graph of http request count in Diksha environment for last 7 days)

/location

a. user declaration report

b. user details report

/misc

a. druid job submitter (Submit the Druid query processor reports(hawk eye reports) based on the scheduler)

***

\[\[category.storage-team]] \[\[category.confluence]]
