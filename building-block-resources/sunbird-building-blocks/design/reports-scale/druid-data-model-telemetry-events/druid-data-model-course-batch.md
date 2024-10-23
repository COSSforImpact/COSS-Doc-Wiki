---
icon: elementor
---

# Druid Data Model - Course Batch

#### **Introduction:** <a href="#druiddatamodel-coursebatch-introduction" id="druiddatamodel-coursebatch-introduction"></a>

This wiki explains ingestion specification for the Course Batch and its related objects to compute required metrics and compose dashboards using Druid.

#### **Design:** <a href="#druiddatamodel-coursebatch-design" id="druiddatamodel-coursebatch-design"></a>

Below are the objects related to course batch

* Course
* Course Batch
* Enrollment
* User
* Location
* Content
* organization

To denormalize **Course**, **User**, **Location** and **Content** details we use the properties part of the Telemetry ingestion spec.

We use below prefix for each object for easy understanding.

| Object       | Prefix              |
| ------------ | ------------------- |
| Course       | course\_            |
| Course Batch | batch\_             |
| Enrollment   | batch\_enrollment\_ |
| User         | user\_              |
| Location     | location\_          |
| Content      | content\_           |

#### **Data Model:** <a href="#druiddatamodel-coursebatch-datamodel" id="druiddatamodel-coursebatch-datamodel"></a>

| Dimension in Druid                      | The field in Course Batch         | Description                                                                                        | Data Type      |
| --------------------------------------- | --------------------------------- | -------------------------------------------------------------------------------------------------- | -------------- |
| batch\_name                             | name                              | Name of the Course Batch                                                                           | String         |
| batch\_id                               | batchId                           | Identifier of the Course Batch                                                                     | String         |
| batch\_createdBy                        | createdBy                         | Course Batch - created by                                                                          | String         |
| batch\_createdDate                      | createdDate                       | Course Batch - created date                                                                        | Date           |
| batch\_createdFor                       | createdFor                        | Course Batch - created for (organizations)                                                         | String         |
| batch\_enrollmentType                   | enrollmentType                    | Course Batch Type - open or invite-only                                                            | String         |
| batch\_startDate                        | startDate                         | Course Batch - start date                                                                          | Date           |
| batch\_endDate                          | endDate                           | Course Batch - end date                                                                            | Date           |
| batch\_enrollmentEndDate                | enrollmentEndDate                 | Course Batch - enrollment end date                                                                 | Date           |
| batch\_status                           | status                            | Course Batch - status                                                                              | Long           |
| batch\_updatedDate                      | updatedDate                       | Course Batch - updated date                                                                        | Date           |
| batch\_enrollment\_active               | active                            | Enrollment active or inactive                                                                      | Boolean        |
| batch\_enrollment\_completedOn          | completedOn                       | Enrollment completed on                                                                            | Date           |
| batch\_enrollment\_completionPercentage | completionPercentage              | completion percentage                                                                              | Long           |
| batch\_enrollment\_enrolledDate         | enrolledDate                      | Enrollment date                                                                                    | Date           |
| batch\_enrollment\_progress             | progress                          | Count of complete contents in the course                                                           | Integer        |
| batch\_enrollment\_updatedBy            | updatedBy                         | Last updated by                                                                                    | String         |
| batch\_enrollment\_updatedDate          | updatedDate                       | Last updated date                                                                                  | Date           |
| batch\_enrollment\_certificates         | certificates                      | Certificates assigned to the enrollment. Considering only `name`, `lastIssuedOn`, `lastReIssuedOn` | Array\[Object] |
| content\_type                           | contentType                       | type of the content                                                                                | String         |
| content\_assessment\_attemptid          | attempt\_id                       | AttemptId for the content assessment                                                               | Sttring        |
| content\_assessment\_attemptscore       | total\_score                      | total score for the assessment attempt                                                             | Integer        |
| content\_assessment\_maxscore           | total\_max\_score                 | total score for the assessment attempt                                                             | Integer        |
| user\_id                                | userId                            | Enrolled user id                                                                                   | String         |
| user\_name                              | username                          | Enrolled username                                                                                  | String         |
| user\_email                             | email                             | Enrolled user email                                                                                | String         |
| user\_phone                             | phone                             | Enrolled user phone                                                                                | String         |
| user\_organization                      | orgname(organisation table)       | Enrolled user organisation name                                                                    | String         |
| user\_school                            | <p><br></p>                       | <p><br></p>                                                                                        | <p><br></p>    |
| user\_enrollment\_date                  | enrolleddate(user\_courses table) | Enrolled user  enrolled Date                                                                       | Date           |
| user\_board                             | framework.board                   | Enrolled user : board                                                                              | String         |
| user\_grade                             | framework.grade                   | Enrolled user : grade                                                                              | Array\[String] |
| user\_medium                            | framework.medium                  | Enrolled user : medium                                                                             | Array\[String] |
| user\_subject                           | framework.subject                 | Enrolled user : subject                                                                            | Array\[String] |
| user\_signup\_date                      | createdOn                         | Enrolled user : createdOn Date                                                                     | Date           |
| user\_course\_progress                  | progress(user\_courses table)     | Enrolled user : course progress                                                                    | int            |
| user\_signin\_type                      | user\_signin\_type                | Enrolled user : Mode of Signin                                                                     | String         |
| user\_login\_mode                       | <p><br></p>                       | Enrolled user : Mode of device(app/portal/desktop)                                                 | String         |
| user\_org\_externalId                   | externalid                        | Enrolled user : organisation external id                                                           | String         |
| location\_district                      | name(location table)              | district Location of the enrolled user                                                             | String         |
| location\_block                         | name(location table)              | block Location of the enrolled user                                                                | String         |
| course\_id                              | courseid                          | unique id of the course                                                                            | String         |
| course\_name                            | courseadditionalinfo.courseName   | name of the course                                                                                 | String         |
| course\_author                          | coursecreator                     | author of the course                                                                               | String         |
