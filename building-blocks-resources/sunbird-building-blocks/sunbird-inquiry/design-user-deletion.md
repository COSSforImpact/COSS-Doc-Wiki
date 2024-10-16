---
icon: elementor
---

# \[Design] User Deletion

### Overview <a href="#id-design-userdeletion-overview" id="id-design-userdeletion-overview"></a>

The user deletion requirement in inQuiry has been originated from the below requirement.

PRD: [\[PRD\] Delete Account functionality](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3351969808/PRD+Delete+Account+functionality)

BE Design Lern - [\[Design\] Delete Account Functionality](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3354492949/Design+Delete+Account+Functionality)

FE Design Lern - [\[Design\] \[Front-end\]Delete User Functionality](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3359146039/Design+Front-end+Delete+User+Functionality)

### What is changing? <a href="#id-design-userdeletion-whatischanging" id="id-design-userdeletion-whatischanging"></a>

The user can request for deletion of their account in Sunbird, this means two primary actions to happen.

1. User's Personal Identifiable Information (PII) needs to be removed
2. The assets (like questions, questionSets, content etc) that was created by this user needs to be transferred to an identified user.

### Scope for inQuiry <a href="#id-design-userdeletion-scopeforinquiry" id="id-design-userdeletion-scopeforinquiry"></a>

Inquiry in its question bank stores the users name and id as part of question and questionSet meta data.

Apart from the **User Name**, there is no other User's Personal Identifiable Information (PII) that is stored in the inQuiry data stores.

The user name is stored in the data stores as below

* Neo4J
* Cassandra (In case of hierarchy)
* Elastic Search
* Redis (For Live Objects)
* Cloud (ECAR Bundle)

### Changes in inQuiry <a href="#id-design-userdeletion-changesininquiry" id="id-design-userdeletion-changesininquiry"></a>

* The below two events will be flowing into inquiry as messages which originated from the Lern system.
  * [User Deletion](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3354492949/Design+Delete+Account+Functionality#Delete-User-Kafka-Event)
  * [Ownership Transfer](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3354492949/Design+Delete+Account+Functionality#Flink-Job)

The events are user specific and not in bulk form.

* No API changes required
* A flink job has to be created to consume these 2 events.
* In case of User Deletion,
  * The user name needs to be cleared out with a static default name (_**Deleted User**_). [Refer](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3351969808/PRD+Delete+Account+functionality#Consequences-and-Considerations%3A)
  * The User Name could be stored in the below attributes as per sunbird inQuiry schema,
    * **creator**
    * author
    * publisher
    * owner
  * The User Id (UUID) is stored in the below fields as per sunbird inQuiry schema, this will be left as is.
    * createdBy
    * lastPublishedBy
    * lastUpdatedBy
    * lastSubmittedBy

createdFor is an attribute that stores the organisation name. It is confirmed that the users in the scope of inQuiry, i.e; creator or reviewer, will always have an organisation.

### Impacts if any <a href="#id-design-userdeletion-impactsifany" id="id-design-userdeletion-impactsifany"></a>

No impacts detected,

* As the searches are based on UUID and that is retained
* In the consumption flow only the author name is displayed

### Technical Design <a href="#id-design-userdeletion-technicaldesign" id="id-design-userdeletion-technicaldesign"></a>



* A flink job will will be written to consume both message (user deletion and ownership transfer)
* This flink job will only deal with two object type Question & QuestionSets.
* Assets (appIcon, images/audio/video used as options/solutions) used under Question/QuestionSets will not be processed by this flink job.
  * Those assets should be processed by Knowlg Flink job as inQuiry uses only artifactUrl metadata of those assets. So no dependency from inQuiry functionality.

**User deletion:**

* The job will have below configurations
  * ```
    # In this config, key will be search field and values will be target fields
    user_pii_search_and_target_keys={
    	"createdBy": ["creator", "originData.creator.name"],
    	"lastPublishedBy": ["publisher"]
    }

    # The value will be applied to target fields speicified in above config
    user_pii_replacement_value="Deleted User"
    ```
  * These configurations allows adopter to configure the job based on their schema
  * The job will process each key mentioned in the **user\_pii\_search\_and\_target\_keys** and updated target fields.
  * If target field is a **nested** field, then it should be configured with DOT (.) separator.
  * If User has multiple roles e.g: CONTENT\_CREATOR & CONTENT\_REVIEWER then corresponding metadata’s (key used to search objects when user acted as creator and reviewer) should be configured as separate keys in **user\_pii\_search\_and\_target\_keys**.
  * The configuration will have default values configured as per sunbird inQuiry schema. Adopter can override based on their requirement.
  * The job will only handle **target** fields with **string** data type.
* A Search will be triggered with user-id received in the message to collect the Question/QuestionSet identifiers.
  * search will be in the neo4j database.
  * objects will be fetched from database in batches. a configuration will be given to decide number of objects in single batch (e.g: 50 objects in 1 batch).
* On collected Identifiers, the flink job will start updating target metadata which will have User Name to the value configured in **user\_pii\_replacement\_value**
  * for all status other than **Retired ,** only primary databases (graph + cassandra) will get updated.
  * offline bundles will not be updated and continue to have the user PII information.
  * For object having **Live** status, redis cache will be cleared.
  * ES will get updated automatically when the job update it in neo4j.
  * **author** metadata will be handled in the code, if **creator** metadata value is same as author, then author field will be also updated to the value configured in **user\_pii\_replacement\_value**

**Ownership Transfer:**

Will be updated in Phase-2

### Discussion items <a href="#id-design-userdeletion-discussionitems" id="id-design-userdeletion-discussionitems"></a>
