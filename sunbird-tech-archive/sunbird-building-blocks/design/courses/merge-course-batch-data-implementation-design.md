---
icon: elementor
---

# Merge Course Batch Data - Implementation Design

### **Impacted tables - content\_consumption, user\_courses** <a href="#mergecoursebatchdata-implementationdesign-impactedtables-content_consumption-user_courses" id="mergecoursebatchdata-implementationdesign-impactedtables-content_consumption-user_courses"></a>

**Data Model**

| <p>user_courses</p><pre><code>    batchid text,
    userid text,
    active boolean,
    addedby text,
    completedon timestamp,
    completionpercentage int,
    contentstatus map&#x3C;text, int>,
    courseid text,
    datetime timestamp,
    delta text,
    enrolleddate text,
    grade text,
    lastreadcontentid text,
    lastreadcontentstatus int,
    progress int,
    status int,
    PRIMARY KEY (batchid, userid)
    CLUSTERING ORDER BY (userid ASC)
</code></pre> | <p>content_consumption</p><pre><code>	userid text,
    contentid text,
    batchid text,
    courseid text,
    completedcount int,
    contentversion text,
    datetime timestamp,
    grade text,
    lastaccesstime text,
    lastcompletedtime text,
    lastupdatedtime text,
    progress int,
    result text,
    score text,
    status int,
    viewcount int,
    PRIMARY KEY (userid, contentid, batchid, courseid)
    CLUSTERING ORDER BY (contentid ASC, batchid ASC, courseid ASC)
</code></pre> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### **Workflow** <a href="#mergecoursebatchdata-implementationdesign-workflow" id="mergecoursebatchdata-implementationdesign-workflow"></a>

1. Get data from content\_consumption table where userId = fromAccountId
2. Check whether toAccountId is present in content\_consumption in the same combination - ~~fromAccountId~~ toAccountId, contentId, batchId, courseId&#x20;
   1. Yes - Update status of toAccountId record in content\_consumption with highest status of 2 records(statuses of fromAccountId and toAccountId records)
   2. No - Insert record in content\_consumption table with data fetched in step 1, with toAccountId replacing fromAccountId for the userId field
3. Delete the record(of fromAccountId) fetched in step 1 from content\_consumption table
4. Get data from user\_courses where batchId = dataFetchedInStep1 and userId = fromAccountId
5. Check whether toAccountId is present in user\_courses table for the same batchId
   1. Yes - Ignore
   2. No - Insert record in user\_courses table with data fetched in step 4, with toAccountId replacing fromAccountId for the userId field
6. Delete the record(of fromAccountId) fetched in step 4 from user\_courses table
7. Generate event and push to Kafka topic

\


\
