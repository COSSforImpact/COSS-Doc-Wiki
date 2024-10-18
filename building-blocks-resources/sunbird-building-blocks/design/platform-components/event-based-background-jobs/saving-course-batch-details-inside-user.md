---
icon: elementor
---

# Saving Course batch details inside user

## Problem statement: <a href="#savingcoursebatchdetailsinsideuser-problemstatement" id="savingcoursebatchdetailsinsideuser-problemstatement"></a>

&#x20;    In course batch stats , we need to do different data sorting and that can be achieve if all data save same place. That's why user course batch some data we are storing inside user index.

Ticket ref: SB-10240

\


\


### Changes required for SB-10240 <a href="#savingcoursebatchdetailsinsideuser-changesrequiredforsb-10240" id="savingcoursebatchdetailsinsideuser-changesrequiredforsb-10240"></a>

Inside user index we need to save following new attribute:

New attribute added in User ES

```
"rootOrgName": "name of rootOrg", // new added
 "organisations" : [
           {
            "userId":"",
            "organisationId":"",
            "orgName":"" // new added
          }
     ],
"batches":[ 
  { "enrolledOn": "", "batchId": "", "courseId": "", "lastAccessedOn": "", "progress": "" } 
 ]

Note: all values will be added on ES only, Cassandra storage won't change.
```

Following point need to be taken care:

1. Sync all the user, and during **sync** we need to add above fields into Elasticsearch (One time job on each Env)
2. Whenever  user is added or removed from batch, we need to call **sync**.
3. Sync batch info to user profile whenever enroll or unenroll api calls happen
4. Sync batch info to user profile whenever update content state api calls
5. Sync batch info to user profile whenever create batch api calls , with participants list
6. Sync batch info to user profile whenever update batch comes  with participants list
7. Update org api
