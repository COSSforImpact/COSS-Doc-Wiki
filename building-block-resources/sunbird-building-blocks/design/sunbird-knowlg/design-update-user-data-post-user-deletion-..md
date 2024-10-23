---
icon: elementor
---

# \[Design] Update User Data Post User Deletion .

### Introduction <a href="#id-design-updateuserdatapostuserdeletion.-introduction" id="id-design-updateuserdatapostuserdeletion.-introduction"></a>

This wiki provides a design approach to handle the post-deletion phase of user accounts. It focuses on searching for assets created by user and updating specified user information within the databases, respectively.

### Overview <a href="#id-design-updateuserdatapostuserdeletion.-overview" id="id-design-updateuserdatapostuserdeletion.-overview"></a>

The requirement in Sunbird Knowlg has been originated from the below requirement:\
[\[PRD\] Delete Account functionality](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3351969808/PRD+Delete+Account+functionality)\
[\[Design\] Delete Account Functionality](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3354492949/Design+Delete+Account+Functionality)\
[\[Design\] \[Front-end\]Delete User Functionality](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3359146039/Design+Front-end+Delete+User+Functionality)

### Background <a href="#id-design-updateuserdatapostuserdeletion.-background" id="id-design-updateuserdatapostuserdeletion.-background"></a>

As per the recent Sunbird update, registered users are now granted access to a "Delete Account" feature, which will delete the user details.\
A challenge arises when a user who has created or updated Assets (e.g., Content, Asset, Collection) initiates the account deletion process. In this scenario, the user information stored within the metadata of these Assets has to be searched and updated/operated in specified keys with respective values.

The user can request for deletion of their account in Sunbird, this means two primary actions to happen.

1. User's Personal Identifiable Information (PII) needs to be removed.
2. The assets (e.g., Content, Asset, Collection, Question, QuestionSet) that was created by this user needs to be transferred to an identified user.

### Problem Statement <a href="#id-design-updateuserdatapostuserdeletion.-problemstatement" id="id-design-updateuserdatapostuserdeletion.-problemstatement"></a>

1. User PII info stored in multiple databases, Which have to be cleaned up.
2. The PII info stored in different properties of each object has to be cleaned up.

### Design <a href="#id-design-updateuserdatapostuserdeletion.-design" id="id-design-updateuserdatapostuserdeletion.-design"></a>



* The User name is stored in the data stores as below
  * Neo4J
  * Cassandra (In case of hierarchy)
  * Elasticsearch
  * Redis (For Live Objects)
  * Cloud (ECAR Bundle)
* The below two events will be flowing into Knowlg as messages which originated from the Lern system.
  * [User Deletion](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3354492949/Design+Delete+Account+Functionality#Delete-User-Kafka-Event)
  * [Ownership Transfer](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3354492949/Design+Delete+Account+Functionality#Flink-Job)

**User Deletion:**

* A Flink job will be written to consume both message (user deletion and ownership transfer)
* A Search will be triggered with user-id received in the message to collect the Object identifiers.
  * Search will be in the neo4j database.
* Flink job will start updating target metadata, which will have Username to the value configured in **user\_pii\_replacement\_value**
  * for all status other than **retired,** only primary databases (graph + Cassandra) will get updated.
  * Offline bundles will not be updated and continue to have the user PII information.
  * For an object having **Live** status, redis cache will be cleared.
  * ES will get updated automatically when the job updates it in neo4j.

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
  * These configurations allow adopter to configure the job based on their schema
  * The job will process each key mentioned in the **user\_pii\_search\_and\_target\_keys** and updated target fields.
  * If target field is a **nested** field, then it should be configured with DOT (.) separator.
  * If a user has multiple roles, e.g: CONTENT\_CREATOR & CONTENT\_REVIEWER then corresponding metadata’s (key used to search objects when user acted as creator and reviewer) should be configured as separate keys in **user\_pii\_search\_and\_target\_keys**.
  * The configuration will have default values configured as per sunbird schema. Adopter can override based on their requirement.
  * The job will handle **target** fields with **string** data type and In the case of an **array**, it will replace the **first occurrence**.

**Ownership Transfer**

Will be updated in next phase.
