---
icon: elementor
---

# SB-26582 Optional Material in a course

### Requirement <a href="#sb-26582optionalmaterialinacourse-requirement" id="sb-26582optionalmaterialinacourse-requirement"></a>

Courses need to support optional material that do not contribute to overall progress of the course , or to the overall score computation for the course.

Jira Id : [![](https://project-sunbird.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10322?size=medium)LR-1](https://project-sunbird.atlassian.net/browse/LR-1) - Backend :: Support for optional material in a course Done

ED Story: [![](https://project-sunbird.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10322?size=medium)ED-258](https://project-sunbird.atlassian.net/browse/ED-258) - Courses>>Support for optional material in a course (mobile+portal) Selected for Contribution

Discussion Thread : [https://github.com/orgs/Sunbird-Ed/discussions/34#discussioncomment-4465619](https://github.com/orgs/Sunbird-Ed/discussions/34#discussioncomment-4465619)

Proposed UI : [https://projects.invisionapp.com/share/SX133YUE5F27#/screens/471152108](https://projects.invisionapp.com/share/SX133YUE5F27#/screens/471152108)

The design approach should focus on below points:

1. The Optional material shouldn’t contribute to the progress % of the trackable collection and hence doesn’t contribute in the completion certificate criteria.
2. The optional material shouldn’t contribute to the final score calculation of the collection and hence doesn’t contribute in the merit certificate criteria.
3. The optional material progress should not be reflected in the progress exhaust.

### Problem Statement <a href="#sb-26582optionalmaterialinacourse-problemstatement" id="sb-26582optionalmaterialinacourse-problemstatement"></a>

1. Adding a new property ‘**optional’** for leaf nodes in Course relational metadata by Sunbird Knowlg
2. Relation Cache updater should update optional nodes in redis
3. Filter out optionalNodes during course progress update
4. Exclude optionalNodes in score computation
5. Exclude optionalNodes from course progress reports
6. Exclude optionalNodes while showing progress in course page.

### Design <a href="#sb-26582optionalmaterialinacourse-design" id="sb-26582optionalmaterialinacourse-design"></a>

1. **Course Relational Metadata changes by Sunbird Knowlg**

Design from Sunbird Knowlg: [\[Editor\] : Support optional material in a course](https://project-sunbird.atlassian.net/wiki/spaces/\~5a5de7e408790741d1ff75a1/pages/3253338150/Editor+Support+optional+material+in+a+course)

To support optional material in courses, specify `optional:boolean`as a new property in course relational metadata.

* Hierarchy child levels can be max 7, default is 4 now
* Last level node will be leaf node
* In between the hierarchy levels, all children are units /folders
* Relational meta data only in the leaf node level
* Leaf node mimetype will be specific to the content, till leaf node all other nodes will have mimetype as collection
* Other than course unit and textbook unit as primary category, everything else can be leaf node now.

![](<../../../../.gitbook/assets/grey\_arrow\_down (3).png>)Sample Course hierarchy:

course{\
courseid:"c1"\
primary category: course /textbook/ collection\
mimeType : "application/vnd.ekstep.content-collection"

leafNodes : \["child1.1.1.1" , "child2.1","childunit3"],

leafNodeCount : 3\
children\[{\
childid : "childunit1"\
primary category: course unit/textbookunit\
children\[{\
childid : "child1.1"\
children\[{\
childid : "child1.1.1"

leafNodes : \["child1.1.1.1" ],

leafNodeCount : 1\
children\[{\
childid : "child1.1.1.1" (leafnode)\
relationalMetadata: {\
optional: true\
}\
}]\
}]\
}]\
},\
{\
childid : "childunit2"

leafNodes : \["child2.1"],

leafNodeCount : 1\
children\[{\
childid : "child2.1" (leafnode)\
}]\
},\
{\
childid : "childunit3"(leafnode)

```
}]
```

}

2\. **RelationCacheUpdater - update the optional nodes list**

After fetching course hierarchy data from `dev_hierarchy_store`.`content_hierarchy` table in cassandra, job should check the relational metadata of the leaf node for optional property.

If the optional property i set to true, fetch the identifier and add it to optionalNodes list.

This should be saved to redis.database.index : 10 along with leafnodes and ancestors.

Scenario1: There wont be a content in a course, which is mandatory in unit1 and optional in unit2 as per current design. Refer : [![](https://project-sunbird.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10322?size=medium)ED-258](https://project-sunbird.atlassian.net/browse/ED-258) - Courses>>Support for optional material in a course (mobile+portal) Selected for Contribution

When same content is added to different units of a course, leafNodes and optional nodes list will have the content id one time only, and leaf node list and count in hierarchy also will not consider duplicate content ids.

With respect to above scenario, when a content is added to multiple units, either in all unit it will be mandatory or in all units it will be optional.

Scenario2: Same content in a course is mandatory in unit1 and optional in unit2 - **This scenario is invalid as per user story.**

In the scenario, where same content in a course is mandatory in unit1 and optional in unit2; then on overall course level we will have to consider it as mandatory for computing total progress and completion count. In this case, relation cache implementation has to change so that, course level optional node list in cache will not have the optional node if atleast in one unit it is mandatory. But unit level optional node list in cache will have the optional node.

So before storing ourse level optional node list in cache, we need to remove the particular optional node which is mandatory in atleast one unit of the course. For implementing this, fetch all mandatory node list and remove those from the course level optional node list before storing it in cache.

![](<../../../../.gitbook/assets/grey\_arrow\_down (3).png>)Sample data in Redis

course id - do\_213398022850707456156

unit id - do\_213398022850707456159

leaf node - do\_21339794950117785147

ancestors - do\_213398022850707456156 (parents)

do\_213398022850707456156:do\_213398022850707456156:leafnodes:\[do\_21339794950117785611,do\_21339794950117785147, do\_213254452773969920123] // Course level leaf nodes

do\_213398022850707456156:do\_213398022850707456159:leafnodes:\[do\_21339794950117785611,do\_21339794950117785147, do\_213254452773969920123] // Unit level leaf nodes\
do\_213398022850707456156:do\_213398022850707456156:optionalnodes:\[do\_213254452773969920123] // Course level optional nodes

do\_213398022850707456156:do\_213398022850707456159:optionalnodes:\[do\_213254452773969920123] // Unit level optional nodes

3\. **Activity\_Aggregator - Filter out optional Nodes from LeafNodes and calculate the progress**

In ActivityAggreagtor job, get the optional nodes along with leafnodes for course id from relational data cache(redis.database.index : 10).\
On Course Level Aggregation, remove the optionalNodes contentids from leafNodes before calculating the overall progress and completion count

In `user_activity_agg` table ‘aggregates’ column, ‘completedCount’ attribute which is calculated by ActivityAggreagtor job should exclude optional node count. The same ‘completedCount’ is stored as progress in user\_enrolments table by ActivityAggreagtor job. But other attributes in ‘aggregates’ column like attempt id, score, max score can be have the same existing logic. These are updated by AssessmentAggregator job. ‘aggregates’ column stores best score of the user in an assessment.

'agg\_details' column in `user_activity_agg` table is updated by AssessmentAggregator job.

![](<../../../../.gitbook/assets/grey\_arrow\_down (3).png>)Activity\_aggregator Data Sample

activity\_type Course\
activity\_id do\_2135062083493396481247\
user\_id e60c9628-a6d4-4003-ad9d-b94a86a06f81\
context\_id cb:013506213033164800114\
agg null\
agg\_details \['{\
"attempt\_id":"bed29c8322d09d21148a44d9d986cd38",\
"last\_attempted\_on":"Mar 31, 2022, 7:14:48 AM",\
"score":4.0,\
"content\_id":"do\_2133470331565588481240",\
"max\_score":4.0,\
"type":"attempt\_metrics"\
}',\
'{\
"attempt\_id":"f6887f0252fb99d6faceaa22c162df5a",\
"last\_attempted\_on":"Mar 31, 2022, 7:14:25 AM",\
"score":2.0,\
"content\_id":"do\_21339794950117785611",\
"max\_score":5.0,\
"type":"attempt\_metrics"\
}']\
aggregates { // attempt which obtained max score is stored with content id and total attempt count on the contentid\
'attempts\_count:do\_2133470331565588481240': 1,\
'attempts\_count:do\_21339794950117785611': 1,\
'completedCount': 3, //total no of completed contents\
'max\_score:do\_2133470331565588481240': 4, // Maximum score the assessment can have\
'max\_score:do\_21339794950117785611': 5,\
'score:do\_2133470331565588481240': 4,\
'score:do\_21339794950117785611': 2 // score the user got\
} agg\_last\_updated {\
'completedCount': '2022-03-31 07:16:13.638000+0000',\
'attempts\_count:do\_2133470331565588481240': '2022-03-31 07:15:22.853000',\
'attempts\_count:do\_21339794950117785611': '2022-03-31 07:15:22.853000+0000',\
'max\_score:do\_2133470331565588481240': '2022-03-31 07:15:22.853000+0000',\
'max\_score:do\_21339794950117785611': '2022-03-31 07:15:22.853000+0000',\
'score:do\_2133470331565588481240': '2022-03-31 07:15:22.853000+0000',\
'score:do\_21339794950117785611': '2022-03-31 07:15:22.853000+0000'\
}

Change required in **user\_enrolments** table **progress** column update. ‘completedCount’ attribute which is calculated by ActivityAggreagtor job should exclude optional node count.

![](<../../../../.gitbook/assets/grey\_arrow\_down (3).png>)user\_enrolments sample data

userid 3034a322-9b4a-489d-82a5-21584e118dd9\
courseid do\_2135062083493396481247\
batchid 013506213033164800114\
active True\
addedby 19b4d86c-ff8f-4674-8990-b4552c6da8af\
certificates null\
certstatus null\
completionpercentage null\
completedon 2022-06-16 11:43:46.480000+0000\
contentstatus {'do\_2133470331565588481240': 2, 'do\_213371885833453568175': 2, 'do\_21339794950117785611': 2}\
datetime 2022-06-16 11:43:46.784000+0000\
enrolled\_date 2022-06-16 11:38:56.798000+0000\
enrolleddate null\
lastcontentaccesstime 2022-06-16 11:43:34.265000+0000\
lastreadcontentid do\_213371885833453568175\
lastreadcontentstatus 2\
progress 3\
status 2\
issued\_certificates \[{\
'identifier': '1-35e37d7a-7dda-49e1-9956-13e6bfdc09a4',\
'lastIssuedOn': '2022-06-16T11:43:47.291+0000',\
'name': 'Merit Certificate',\
'templateUrl': '[https://sunbirdstagingpublic.blob.core.windows.net/sunbird-content-staging/content/do\_21348140206386380811/artifact/-](https://sunbirdstagingpublic.blob.core.windows.net/sunbird-content-staging/content/do\_21348140206386380811/artifact/-)\
do\_21348140206386380811\_1645678963519\_certificate\_2022-02-24\_10\_32.svg',\
'token': '',\
'type':'TrainingCertificate'\
}]

No change required in assessment\_aggregator table update.

![](<../../../../.gitbook/assets/grey\_arrow\_down (3).png>)assessment\_aggregator

user\_id fa53ebdc-4a6f-4979-99f4-f551456075b0\
course\_id do\_2135062083493396481247\
batch\_id 013506213033164800114\
content\_id do\_2133470331565588481240\
attempt\_id deceb12dd2d9747c6b6274561e4a9e58\
created\_on 2022-03-31 07:11:22.263000+0000\
grand\_total 2.0/4.0\
last\_attempted\_on 2022-03-31 07:11:04.309000\
total\_max\_score 4\
total\_score 2\
updated\_on 2022-03-31 07:11:22.263000+0000\
question \[{id: 'do\_2133470529294417921245', assess\_ts: '2022-03-31 07:11:13.769000+0000', max\_score: 1, score: 0, type: 'mcq', title: 'Q3', resvalues: \[{'label': '\<h5>Hello\</h5>', 'selected': 'true', 'value': '3.0'}], params: \[{'answer': 'true', 'value': '{"body":"\u003ch1\u003eHello\u003c/h1\u003e","value":0.0}'}, {'answer': 'false', 'value': '{"body":"\u003ch2\u003eHello\u003c/h2\u003e","value":1.0}'}, {'answer': 'false', 'value': '{"body":"\u003ch3\u003eHello\u003c/h3\u003e","value":2.0}'}, {'answer': 'false', 'value': '{"body":"\u003ch5\u003eHello\u003c/h5\u003e","value":3.0}'}], description: null, duration: 1.0}]

3\. **Assessment Aggregator - **~~**Ignore optional nodes from LeafNodes for score computation -**~~** Assessment cannot be optional as per the ED-258 story**

~~On consuming i/p event in UserScoreAggregateFunction, get the list of optionalNodes contentIds from relation cache.~~\
~~On quering assessment\_aggregator tbl to get the total\_max\_score, total\_score and score, filter out the optionalNodes contentIds.~~

In assessment\_aggregator table, data is stored content-attempt wise.

4\. **Reports**

Progress Exhaust:\
After loading data from content\_hierarchy table, 'leafNodesCount' calculation\
has to be added to exclude optional nodes count. And to compute the completionPercentage\
of the course for displaying total progress, optional nodes' ids has to be excludes from content ids in 'contentstatus' column in user\_enrolment table.

For this contentstatus column is used because eventually user\_enrolment.progess and `user_activity_agg`.aggregates{completedCount} was supposed to be deprecated. These both columns save same value, total no of leafnodes user completed consumption.

As per this Jira ticket [https://project-sunbird.atlassian.net/browse/ED-258.](https://project-sunbird.atlassian.net/browse/ED-258.) score calculation is not affected, because an assessment cannot be optional.

![](<../../../../.gitbook/assets/grey\_arrow\_down (3).png>)Progress Exhaust report fields

1. Collection Id
2. Collection Name
3. Batch Id
4. Batch Name
5. User UUID
6. User Name
7. State
8. District
9. Enrolment Date
10. Completion Date
11. Progress
12. Certificate Status
13. Total Score
14. \<assessment\_id> - Score

### Edge User case Queries <a href="#sb-26582optionalmaterialinacourse-edgeusercasequeries" id="sb-26582optionalmaterialinacourse-edgeusercasequeries"></a>

**Case 1:** if a user have consumed the course. After that course is update for a existing content as optional content. How do we need to update the user consumption and user assessment aggregate?

**Case 2:** As batch service does not store the optional field, whoever does the progress calculation using API will have to call content-service also to check if the leaf node is optional or not

**Case 3:** In a collection, if unit 1 and unit 2 has same content with same content id, and in unit 1 the content is mandatory and unit 2 it is optional, how should the calculation should be handled? How to restrict same content being added as optional and mandatory in different units of same course?

#### Assumptions: <a href="#sb-26582optionalmaterialinacourse-assumptions" id="sb-26582optionalmaterialinacourse-assumptions"></a>

1. An assessment cannot be optional.
2. Same content cannot be optional in one unit and mandatory in another unit of the same course.
