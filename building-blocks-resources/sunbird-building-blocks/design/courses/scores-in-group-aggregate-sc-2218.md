---
icon: elementor
---

# Scores-in-Group-aggregate---SC-2218

### Overview

This document details the design options for introducing scores as part of group aggregate API and reports.

### Design

Currently, only trackable collections and their progress are stored in user\_activity\_agg table.

Below is the flow used to show scores in group aggregates.

**AssessmentAggregator job changes:**

Create a new process function to compute the best attempted score and store it in user\_activity\_agg table in below format.

| activity\_type | activity\_id | user\_id  | context\_id   | agg                                                   | agg\_last\_updated                                                            |
| -------------- | ------------ | --------- | ------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------- |
| Course         | collectionId | user\_123 | cb:batch\_123 | {'score:assessmentId\_1': ,'score:assessmentId\_2': } | {'score:assessmentId\_1': ‘timestamp’, 'score:assessmentId\_2':: ‘timestamp’} |

**Implementation steps:**

* Read the best score from assessment\_aggregate table using courseId, userId, batchId and contentId from the event
* Partial update the agg and agg\_last\_updated columns in user\_activity\_agg

**Group Aggregate API changes:**

The response contains the score aggregates also if the collection contains self assessments.

**Response:**

```
{
    "id": "api.group.activity.agg",
    "ver": "v1",
    "ts": "2021-04-14 17:49:30:782+0530",
    "params": {
        "resmsgid": null,
        "msgid": "70b89413-fe1f-482a-b92a-e27d4af0ae4f",
        "err": null,
        "status": "success",
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {
        "activity": {
            "id": "collectionId",
            "type": "Course",
            "agg": [
                {
                    "metric": "enrolmentCount",
                    "lastUpdatedOn": 1618390479814,
                    "value": 1 <totla number of enrolments>
                }
            ]
        },
        "groupId": "groupId",
        "members": [
            {
                "agg": [
                    {
                        "metric": "completedCount",
                        "value": 2,
                        "lastUpdatedOn": 1596647700613
                    },
                    {
                        "metric": "score:assessmentId_1",
                        "value": 10, <best attempted score>
                        "lastUpdatedOn": 1618390479814
                    },
                    {
                        "metric": "score:assessmentId_2",
                        "value": 20, <best attempted score>
                        "lastUpdatedOn": 1618390479814
                    }
                ],
                "name": "",
                "role": "admin",
                "status": "active",
                "createdBy": "userId",
                "userId": "userId"
            }
        ]
    }
}
```

***

\[\[category.storage-team]] \[\[category.confluence]]
