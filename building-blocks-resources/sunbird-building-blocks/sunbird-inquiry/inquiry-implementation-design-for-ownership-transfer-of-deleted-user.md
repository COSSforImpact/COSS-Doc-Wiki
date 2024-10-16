---
icon: elementor
---

# inQuiry - Implementation Design for ownership transfer of deleted user

### Problem Statement: <a href="#inquiry-implementationdesignforownershiptransferofdeleteduser-problemstatement" id="inquiry-implementationdesignforownershiptransferofdeleteduser-problemstatement"></a>

* When user gets deleted in Sunbird System, the user pii information will be removed but ownership remains with deleted user, which need to be transfered to another user for further maintainence of the asset.

### Solution: <a href="#inquiry-implementationdesignforownershiptransferofdeleteduser-solution" id="inquiry-implementationdesignforownershiptransferofdeleteduser-solution"></a>

* Sunbird Learn BB Spark Job will generate a report for asset owned by deleted user.
* The Org Admin user will have two option for ownership transfer through ownership transfer api.
  1. All Asset Transfer From Deleted User to Speicifc User Having Similar Roles.
  2. Partial/Selected Asset Transfer From Deleted User to Speicifc User Having Similar Roles.
* In both cases, the api will trigger kafka event which need to be processed at inQuiry/Knowlg BB Level.
* kafka events will also have First Name & Last Name of the user, where transfer should happen.
  * the name should be formed and stampped against the target field used during cleanup of PII.
* Sample Kafka Event for All Asset Transfer:
* ```
  {
    "eid": "BE_JOB_REQUEST",
    "ets": 1619527882745,
    "mid": "LP.1619527882745.32dc378a-430f-49f6-83b5-bd73b767ad36",
    "actor": {
      "id": "ownership-transfer",
      "type": "System"
    },
    "context": {
      "pdata": {
        "id": "org.sunbird.platform",
        "ver": "1.0"
      }
    },
    "object": {
      "id": "<from-userId>",
      "type": "User"
    },
    "edata": {
      "action": "ownership-transfer",
      "organisationId": "{{organisationId}}",
      "context": "User Deletion", // "User Deletion", "Role Change", etc.
      "actionBy": {
  		"userId": {{user_id}},
  		"userName": {{user_name}}
      },
      "fromUserProfile": {
  		"userId": {{}},
  		"userName": {{}},
  		"channel":{{}},
  		"organisationId": {{}},
  		"roles": {
            
  		}
      },
      "toUserProfile": {
  		"userId": {{}},
  		"userName": {{}},
  		"firstName": "",
  		"lastName": "",
  		"roles": {
            
  		}
      },   
      "iteration": 1
    }
  }
  ```
* Sample Kafka Event for Partial/Selected Asset Transfer:
* ```
  {
    "eid": "BE_JOB_REQUEST",
    "ets": 1619527882745,
    "mid": "LP.1619527882745.32dc378a-430f-49f6-83b5-bd73b767ad36",
    "actor": {
      "id": "ownership-transfer",
      "type": "System"
    },
    "context": {
      "pdata": {
        "id": "org.sunbird.platform",
        "ver": "1.0"
      }
    },
    "object": {
      "id": "<from-userId>",
      "type": "User"
    },
    "edata": {
      "action": "ownership-transfer",
      "organisationId": "{{organisationId}}",
      "context": "User Deletion", // "User Deletion", "Role Change", etc.
      "actionBy": {
  		"userId": {{user_id}},
  		"userName": {{user_name}}
      },
      "fromUserProfile": {
  		"userId": {{}},
  		"userName": {{}},
  		"channel":{{}},
  		"organisationId": {{}},
  		"roles": {
            
  		}
      },
      "toUserProfile": {
  		"userId": {{}},
  		"userName": {{}},
  		"firstName": "",
  		"lastName": "",
  		"roles": {
            
  		}
      },   
      "assetInformation": {
        "objectType": "{{objectType}}",
        "identifier": "{{resource_identifier}}"
      },
      "iteration": 1
    }
  }
  ```
* inQuiry will enhance the existing flink job "**user-pii-data-updater**" to process ownership transfer request.
* the flink job will process both events (all & partial/selected asset transfer)

#### Case-1: All Asset Transfer: <a href="#inquiry-implementationdesignforownershiptransferofdeleteduser-case-1-allassettransfer" id="inquiry-implementationdesignforownershiptransferofdeleteduser-case-1-allassettransfer"></a>

* the job will process each event for all objects configured under **valid\_object\_types** configuration. (e.g: Asset, Content, Question, QuestionSet, Collection).
* the job will search for each objectType assets belong to the deleted user (userId will be taken from fromUserProfile).
  * the lookup key will be taken from PII\_Fields.user config of each target object type.
  *   sample config:

      ```
      "PII_Fields": {
          		"user": {
            			"createdBy": ["creator"]
          		},
          		"org": {
          		}
        		}
      ```
* the job will validate the role of new user against a list of roles configured in the job. e.g: **ownership\_transfer\_roles**=\["CONTENT\_CREATOR"]
* the job will update graph data only for target fields
  * update will happen one by one for all individual objects.
  * lookupKey will also be updated by userId taken from toUserProfile.
  * other target fields configured will be updated by "User Name" formed using First Name & Last Name.

#### Case-2: Partial/Selected Asset Transfer: <a href="#inquiry-implementationdesignforownershiptransferofdeleteduser-case-2-partial-selectedassettransfer" id="inquiry-implementationdesignforownershiptransferofdeleteduser-case-2-partial-selectedassettransfer"></a>

* the job will take asset details from "assetInformation" attribute of event.
* the job will validate if the objectType of the asset comes under objectTypes configured in the job (config: **valid\_object\_types**).
* the job will validate role of to User against **ownership\_transfer\_roles** config values.
* the job will read the data using identifier.
* the job will read the **PII\_Fields** from object schema and validate the **lookupKey** entry in the object.
* the job will update the target fields along with lookupKey and save data in graph.

#### &#x20;Common Points Applicable to Both Cases: <a href="#inquiry-implementationdesignforownershiptransferofdeleteduser-commonpointsapplicabletobothcases" id="inquiry-implementationdesignforownershiptransferofdeleteduser-commonpointsapplicabletobothcases"></a>

* the job won't make any changes to hierarchal data.
* the job won't re-publish the asset which are in Live status.
* the job won't send any notification to the org admin for transfer confirmation.
