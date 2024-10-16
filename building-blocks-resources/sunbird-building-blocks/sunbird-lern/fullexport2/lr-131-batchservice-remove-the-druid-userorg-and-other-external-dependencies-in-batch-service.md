---
icon: elementor
---

# \[LR-131]BatchService: Remove the druid, userorg and other external dependencies in batch service

Making the installation process of course service easier by decoupling the external dependencies.Current course service is using user org service for some user validation and we make few druid service calls along with some other external dependencies.From this feature, other building block dependencies will be decoupled.

**Dependencies and Approach to Decouple:**

| **Method name / File name / Service name**                                                                                                            | **Dependency / URLs/Variables**                                                                     | **Approach** |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | ------------ |
| **externalresource.properties**                                                                                                                       | **URL’s:**                                                                                          |              |
| \`\`\`                                                                                                                                                |                                                                                                     |              |
| content\_url=/content/v3/hierarchy/                                                                                                                   |                                                                                                     |              |
| ekstep\_course\_publish\_url=/content/v3/publish                                                                                                      |                                                                                                     |              |
| ekstep\_metrics\_api\_url=/metrics/consumption/content-usage                                                                                          |                                                                                                     |              |
| ekstep\_es\_metrics\_api\_url=/metrics/creation/content-snapshot                                                                                      |                                                                                                     |              |
| ekstep\_concept\_base\_url=/domain/v3/{domain}/concepts/list                                                                                          |                                                                                                     |              |
| ekstep\_domain\_url=/domain/v3/list                                                                                                                   |                                                                                                     |              |
| sunbird\_app\_url=                                                                                                                                    |                                                                                                     |              |
| ekstep.channel.reg.api.url=/channel/v3/create                                                                                                         |                                                                                                     |              |
| ekstep.channel.update.api.url=/channel/v3/update                                                                                                      |                                                                                                     |              |
| sunbird\_learner\_service\_url=http://localhost:9000                                                                                                  |                                                                                                     |              |
| sunbird\_lms\_base\_url=http://localhost:9000                                                                                                         |                                                                                                     |              |
| sunbird\_telemetry\_base\_url=http://localhost:9000                                                                                                   |                                                                                                     |              |
| sunbird\_linked\_content\_base\_url=https://dev.sunbirded.org/play/content/                                                                           |                                                                                                     |              |
| sunbird\_cert\_download\_uri=/v1/user/certs/download                                                                                                  |                                                                                                     |              |
| \`\`\`                                                                                                                                                |                                                                                                     |              |
| **Variables:**                                                                                                                                        |                                                                                                     |              |
| \`\`\`none                                                                                                                                            |                                                                                                     |              |
| quartz\_course\_batch\_timer=0 0 0/4 1/1 \* ? \*                                                                                                      |                                                                                                     |              |
| quartz\_upload\_timer=0 0 23 1/1 \* ? \*                                                                                                              |                                                                                                     |              |
| quartz\_course\_publish\_timer=0 0 0/1 1/1 \* ? \*                                                                                                    |                                                                                                     |              |
| quartz\_matrix\_report\_timer=0 0 0/4 1/1 \* ? \*                                                                                                     |                                                                                                     |              |
| quartz\_shadow\_user\_migration\_timer=0 0 2 1/1 \* ? \*                                                                                              |                                                                                                     |              |
| sunbird\_encryption\_mode=local                                                                                                                       |                                                                                                     |              |
| quartz\_metrics\_timer =0 0 0/4 \* \* ? \*                                                                                                            |                                                                                                     |              |
| default\_date\_range=7                                                                                                                                |                                                                                                     |              |
| quartz\_update\_user\_count\_timer=0 0 2 1/1 \* ? \*                                                                                                  |                                                                                                     |              |
| sunbird\_url\_shortner\_access\_token=                                                                                                                |                                                                                                     |              |
| quartz\_channel\_reg\_timer=0 0 1 1/1 \* ? \*                                                                                                         |                                                                                                     |              |
| sunbird\_otp\_allowed\_attempt=2                                                                                                                      |                                                                                                     |              |
| sunbird\_lms\_authorization=                                                                                                                          |                                                                                                     |              |
| sunbird\_installation\_email=dummy@dummy.org                                                                                                          |                                                                                                     |              |
| sunbird\_otp\_hour\_rate\_limit=5                                                                                                                     |                                                                                                     |              |
| sunbird\_otp\_day\_rate\_limit=20                                                                                                                     |                                                                                                     |              |
| sunbird\_user\_create\_sync\_type=ES                                                                                                                  |                                                                                                     |              |
| sunbird\_user\_create\_sync\_topic=local.user.events                                                                                                  |                                                                                                     |              |
| sigterm\_stop\_delay=40                                                                                                                               |                                                                                                     |              |
| sunbird\_msg\_sender=                                                                                                                                 |                                                                                                     |              |
| sunbird\_msg\_91\_auth=                                                                                                                               |                                                                                                     |              |
| sunbird\_valid\_location\_types=state,district,block;cluster                                                                                          |                                                                                                     |              |
| sunbird\_default\_user\_type=teacher                                                                                                                  |                                                                                                     |              |
| sunbird\_app\_name="Sunbird"                                                                                                                          |                                                                                                     |              |
| sunbird\_email\_max\_recipients\_limit=100                                                                                                            |                                                                                                     |              |
| sunbird\_user\_max\_encryption\_limit=100                                                                                                             |                                                                                                     |              |
| sunbird\_rate\_limit\_enabled=true                                                                                                                    |                                                                                                     |              |
| sunbird\_course\_metrics\_container=reports                                                                                                           |                                                                                                     |              |
| sunbird\_course\_metrics\_report\_folder=course-progress-reports                                                                                      |                                                                                                     |              |
| sunbird\_assessment\_report\_folder=assessment-reports                                                                                                |                                                                                                     |              |
| sunbird\_cache\_enable=false                                                                                                                          |                                                                                                     |              |
| sunbird\_audit\_event\_batch\_allowed=false                                                                                                           |                                                                                                     |              |
| sunbird\_fuzzy\_search\_threshold=0.5                                                                                                                 |                                                                                                     |              |
| sunbird\_reset\_pass\_msg=Your have requested to reset password. Click on the link to set a password: {0}                                             |                                                                                                     |              |
| sunbird\_reset\_pass\_mail\_subject=Reset Password                                                                                                    |                                                                                                     |              |
| sunbird\_subdomain\_keycloak\_base\_url=https://merge.dev.sunbirded.org/auth/                                                                         |                                                                                                     |              |
| sunbird\_account\_merge\_body=All your {0} usage details are merged into your account {1} . The account {2} has been deleted                          |                                                                                                     |              |
| sunbird\_user\_upload\_error\_visualization\_threshold=20001                                                                                          |                                                                                                     |              |
| sunbird\_course\_completion\_certificate\_name=100PercentCompletionCertificate                                                                        |                                                                                                     |              |
| sunbird\_migrate\_user\_body=You can now access your {0} state teacher account using {1}. Please log out and login once again to see updated details. |                                                                                                     |              |
| sunbird\_account\_merge\_subject=Account merged successfully                                                                                          |                                                                                                     |              |
| user\_relations=address,education,jobProfileorgUser                                                                                                   |                                                                                                     |              |
| org\_relations=orgUser,address                                                                                                                        |                                                                                                     |              |
| \`\`\`                                                                                                                                                |                                                                                                     |              |
| **API Calls:**                                                                                                                                        |                                                                                                     |              |
| \`\`\`                                                                                                                                                |                                                                                                     |              |
| sunbird\_channel\_read\_api=/v1/channel/read                                                                                                          |                                                                                                     |              |
| sunbird\_framework\_read\_api=/v1/framework/read                                                                                                      |                                                                                                     |              |
| sunbird\_telemetry\_api\_path=/v1/telemetry                                                                                                           |                                                                                                     |              |
| \`\`\`                                                                                                                                                |                                                                                                     |              |
| Remove the unused URL's,variables and API calls from the externalresource.properties other than course/batch service building block.                  |                                                                                                     |              |
| **User org service - Search org** **getOrganisationById**                                                                                             | <p><strong>getOrganisationById:</strong></p><ul><li><strong>PageManagementActor:</strong></li></ul> |              |

1\. \*\*\_validateOrg\_\*\* .getOrganisationById

* \*\*CourseBatchManagementActor:\*\*

1\. \*\*\_isOrgValid\_\*\* .getOrganisationById

We are passing the **organisation id** as the parameter in the request to the **org search API** of user org service and in the response if we have the **CONTENT** part and a value of for the **id(highlighted in red).** we are proceeding with creating the page or else we throw exception as organisation id is invalid. **API:** sunbird\_search\_organisation\_api=/v1/org/search **Request:**

```
{    "request": {        "filters": {            "rootOrgId": "0136556642643394560"        },        "limit": 100    }}
```

**Response :**

```
{  "id": "api.org.search",  "ver": "v1",  "ts": "2020-11-23 09:16:58:628+0000",  "params": {    "resmsgid": null,    "msgid": "ad7135b8-ef64-44bd-adaa-0b131a657689",    "err": null,    "status": "success",    "errmsg": null  },  "responseCode": "OK",  "result": {    "response": {      "count": 1,      "content": [        {          "dateTime": null,          "preferredLanguage": null,          "keys": {},          "channel"": "ChannelNew",          "approvedBy": null,          "description": "Updated Description",          "updatedDate": "2020-12-01 10:29:49:496+0000",          "addressId": "0131630420489011201",          "provider": "channelnew",          "orgCode": null,          "locationId": null,          "theme": null,          "id": "0131630445447741440",          "isApproved": null,          "communityId": null,          "slug": "channelnew",          "email": "info@org.org",          "isSSOEnabled": false,          "identifier": "0131630445447741440",          "thumbnail": null,          "updatedBy"": null,          "orgName": "Org Name",          "address": {},          "externalId": "extid",          "rootOrgId": "0131630445447741440",          "imgUrl": null,          "approvedDate": null,          "homeUrl": null,          "isDefault": null,          "createdDate": "2020-12-01 09:52:46:962+0000",          "createdBy": null,          "hashTagId": "0131630445447741440",          "noOfMembers": null,          "status": 0,          "orgLocation": [            {              "id": "9541f516-4c01-4322-aa06-4062687a0ce5",              "type": "block"            },            {              "id": "6dd69f1c-ba40-4b3b-8981-4fb6813c5e71",              "type": "district"            },            {              "id": "e9207c22-41cf-4a0d-81fb-1fbe3e34ae24",              "type": "cluster"            },            {              "id": "ccc7be29-8e40-4d0a-915b-26ec9228ac4a",              "type": "state"            }          ],          "organisationType": 2,          "isSchool": true,          "isTenant": true        }      ]    }  }}
```

\| | | **User org service - read user** **getUsersByIds** and **getUserById** | **getUsersByIds:**

* **SearchHandlerActor:**

1\. \*\*\_populateCreatorDetails\_\*\* .getUsersByIds

* \*\*CourseBatchManagementActor\*\*

1\. \*\*\_validateMentors\_\*\* .getUsersByIds

* \*\*BulkUploadBackGroundJobActor:\*\*

1\. \*\*\_validateBatchUserListAndAdd.\_\*\* getUsersByIds

**getUserById:**

* **CourseBatchManagementActor**

\*\*\_getRootOrg\_\*\* .getUsersById : We pass the id and auth token to \*\*getUsersById\*\* to get this user info in response,and from this response map we get the \*\*rootOrgId\*\* . \*\*API:\*\* /private/user/v1/read/02bb0640-ae41-41f3-853c-0c0b2f481ffa \*\*Response:\*\* \`\`\` { "id": ".private.user.v1.read.02bb0640-ae41-41f3-853c-0c0b2f481ffa", "ver": "private", "ts": "2022-12-02 11:23:30:811+0530", "params": { "resmsgid": "50ffd259-4aa3-4fe1-806a-79f53b61e8ed", "msgid": "50ffd259-4aa3-4fe1-806a-79f53b61e8ed", "err": null, "status": "SUCCESS", "errmsg": null }, "responseCode": "OK", "result": { "response": { "webPages": null, "maskedPhone": null, "tcStatus": null, "loginId": null, "subject": null, "channel": "channel1003", "profileUserTypes": \[], "language": null, "updatedDate": null, "password": null, "managedBy": null, "flagsValue": 0, "id": "02bb0640-ae41-41f3-853c-0c0b2f481ffa", "recoveryEmail": "", "identifier": "02bb0640-ae41-41f3-853c-0c0b2f481ffa", "thumbnail": null, "profileVisibility": null, "updatedBy": null, "accesscode": null, "locationIds": \[], "registryId": null, "rootOrgId": "0136549971190415360", "prevUsedEmail": "", "firstName": "aiman", "profileLocation": \[], "tncAcceptedOn": null, "allTncAccepted": {}, "profileDetails": null, "phone": "", "dob": null, "grade": null, "currentLoginTime": null, "userType": null, "status": 1, "lastName": "sharief", "gender": null, "prevUsedPhone": "", "stateValidated": false, "encEmail": "AoonPTnXx8T3Ucm6ao43sXhB1mMb5i9dnfudxp9Hw9fv1RPqp/kWL5G3nE9RtFrmtI2mAX3cCv8h\nxrqrXEQNwVDO27LxvyimzUrhOaudAZ+G3CTlL91leS+gNyM2uF+aTQtMGOn7lhkDdxs1iV8l8A==", "isDeleted": false, "organisations": \[ { "isSelfDeclaration": false, "organisationId": "0136549971190415360", "updatedBy": null, "addedByName": null, "addedBy": null, "associationType": 1, "approvedBy": null, "updatedDate": null, "userId": "02bb0640-ae41-41f3-853c-0c0b2f481ffa", "approvaldate": null, "isSystemUpload": false, "isDeleted": false, "hashTagId": "0136549971190415360", "isSSO": true, "isRejected": null, "id": "0136555060112424960", "position": null, "isApproved": null, "orgjoindate": "2022-10-28 10:02:03:290+0530", "orgLeftDate": null } ], "provider": null, "countryCode": null, "maskedEmail": "ai\*\*\*\*\*\*\*\*\*\*@yopmail.com", "tempPassword": null, "email": "ai\*\*\*\*\*\*\*\*\*\*@yopmail.com", "rootOrg": { "dateTime": null, "preferredLanguage": null, "keys": {}, "organisationSubType": null, "approvedBy": null, "channel": "Channel", "description": "Description", "updatedDate": null, "addressId": null, "organisationType": 2, "orgType": null, "isTenant": true, "provider": "channel", "locationId": null, "orgCode": null, "theme": null, "id": "0136549971190415360", "isApproved": null, "communityId": null, "email": "info@org.org", "slug": "channel", "isSSOEnabled": true, "thumbnail": null, "orgName": "Sunbird\_aiman", "updatedBy": null, "locationIds": \[], "externalId": "extid", "orgLocation": \[], "isRootOrg": null, "rootOrgId": "0136549971190415360", "approvedDate": null, "imgUrl": null, "isSchool": true, "homeUrl": null, "orgTypeId": null, "isDefault": null, "createdDate": "2022-10-27 16:39:30:243+0530", "createdBy": "12345", "parentOrgId": null, "hashTagId": "0136549971190415360", "noOfMembers": null, "status": 1 }, "phoneVerified": true, "profileSummary": null, "tcUpdatedDate": null, "recoveryPhone": "", "avatar": null, "userName": "aimansharief", "userId": "02bb0640-ae41-41f3-853c-0c0b2f481ffa", "userSubType": null, "emailVerified": true, "lastLoginTime": null, "createdDate": "2022-10-28 10:02:03:141+0530", "framework": {}, "createdBy": "12345", "profileUserType": {}, "encPhone": null, "location": null, "tncAcceptedVersion": null } \}} \`\`\` | | | \*\*Notification Service\*\* | \*\*sendEmailNotification:\*\*

* \*\*CourseBatchNotificationActor:\*\*

1\. \*\*sendMail.sendEmailNotification\*\*

**API Used:** sunbird\_send\_email\_notifictaion\_api=/v1/notification/email **Template,authtoken** **Request:**

```
{    "request": {        "subject": "subject",        "emailTemplateType": "template",        "body": "Notification mail Body",        "orgName": "orgName",        "courseLogoUrl": "appIcon",        "startDate": "startDate",        "endDate": "endDate",        "courseid": "courseid",        "batchName": "batchName",        "courseName": "name",        "courseBatchUrl": "https://dev.sunbirded.org/learn/course/courseId/batch/batchId",        "signature": "sunbird_course_batch_notification_signature",        "recipientUserIds": "userId"    }}
```

**Response:**

```
Response:{     "id": "api.notification.email",     "ver": "v1",     "ts": "2020-12-06 21:05:11:142+0530",     "params": {         "resmsgid": null,         "msgid": "3c8bd215-4b02-4b9a-a419-7462fc525a73",         "err": null,         "status": "success",         "errmsg": null     },     "responseCode": "OK",     "result": {         "response": "SUCCESS"     } }
```

\| | | **Unused methods/URLs:** | getOrganisationsByIds getUsers sunbird\_search\_user\_api=/v1/user/search LearnerServiceUrls.java | | | **Druid Service Calls** | **CollectionSummaryAggregate.Scala:**

* **getResponseFromDruid**

\*\*Variables:\*\* druid\_proxy\_api\_host=localhostdruid\_proxy\_api\_port=8082druid\_proxy\_api\_endpoint=/druid/v2/ | |

***

\[\[category.storage-team]] \[\[category.confluence]]
