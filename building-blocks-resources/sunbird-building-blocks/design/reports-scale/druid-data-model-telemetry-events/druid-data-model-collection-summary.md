---
icon: elementor
---

# Druid Data Model - Collection Summary

### Data Model: <a href="#druiddatamodel-collectionsummary-datamodel" id="druiddatamodel-collectionsummary-datamodel"></a>

|    | **Dimension In Druid**      | **Field In Report**    | **Description**                                        | **Data Type** |
| -- | --------------------------- | ---------------------- | ------------------------------------------------------ | ------------- |
| 1  | content\_org                | organisation           | Published By or Course Publisher Name or tenant        | String        |
| 2  | user\_org                   | orgname                | User Organisation name                                 | String        |
| 3  | batch\_id                   | batchid                | Unique Batch Identifier                                | String        |
| 4  | collection\_id              | courseid               | Unique Collection Identifier                           | String        |
| 5  | batch\_start\_date          | startdate              | Start Date of the Batch                                | String        |
| 6  | batch\_end\_date            | enddate                | End Date of the Batch                                  | String        |
| 7  | collection\_name            | collectionname         | Name of Course                                         | String        |
| 8  | batch\_name                 | batchname              | Name of the batch                                      | String        |
| 9  | total\_enrolment            | enrolleduserscount     | The number of users are enrolled for the course.       | Long          |
| 10 | total\_completion           | completionuserscount   | The number of users have completed the course          | Long          |
| 11 | total\_certificates\_issued | certificateissuedcount | The number of users received the certificate in course | Long          |
| 12 | content\_status             | contentstatus          | State of Course. Ex: Live, Draft, etc.                 | String        |
| 13 | user\_state                 | state                  | Name of The State                                      | String        |
| 14 | user\_district              | district               | Name of the District                                   | String        |
| 15 | content\_channel            | channel                | Name of the Channel                                    | String        |
| 16 | keywords                    | keywords               | Keywords/Tags which are assigned to course             | List\[String] |
| 17 | timestamp                   | timestamp              | TimeStamp of when the report is generated.             | Long          |
| 18 | content\_channel            | channel                | Channel of the collection/course                       | String        |
| 19 | has\_certificate            | hascertified           | Whether batch is certified or not                      | Boolean       |
