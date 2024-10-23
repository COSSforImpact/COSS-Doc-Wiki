---
icon: elementor
---

# Rollup Data Model - Summary Events

### **Dimensions:** <a href="#rollupdatamodel-summaryevents-dimensions" id="rollupdatamodel-summaryevents-dimensions"></a>

| #  | Dimension in Druid     | Field in Telemetry                                 | Description                                                      | Datatype |
| -- | ---------------------- | -------------------------------------------------- | ---------------------------------------------------------------- | -------- |
| 1  | eid                    | eid                                                | Event Id                                                         | String   |
| 2  | dimensions\_pdata\_id  | [dimensions.pdata.id](http://dimensions.pdata.id/) | Producer Id as dimension from raw telemetry                      | String   |
| 3  | dimensions\_pdata\_pid | dimensions.pdata.pid                               | Producer Process Id as dimension from raw telemetry              | String   |
| 4  | dimensions\_mode       | dimensions.mode                                    | Context Environment                                              | String   |
| 5  | dimensions\_type       | dimensions.type                                    | Type of summary                                                  | String   |
| 6  | content\_name          | [contentdata.name](http://contentdata.name/)       | Name of the content                                              | String   |
| 7  | content\_board         | contentdata.board                                  | Board of affiliation                                             | String   |
| 8  | object\_id             | [object.id](http://object.id/)                     | Content Id                                                       | String   |
| 9  | object\_type           | object.type                                        | Content Type                                                     | String   |
| 10 | object\_rollup\_l1     | object.rollup.l1                                   | Object level1 rollup                                             | String   |
| 11 | derived\_loc\_state    | derivedlocationdata.state                          | Derived location state of the user                               | String   |
| 12 | derived\_loc\_district | derivedlocationdata.district                       | Derived location district of the user                            | String   |
| 13 | dialcode\_channel      | dialcodedata.channel                               | Channel for which dialcode is generated                          | String   |
| 14 | user\_type             | userdata.type                                      | Type of user                                                     | String   |
| 15 | user\_signin\_type     | userdata.usersignintype                            | User sign-in type info                                           | String   |
| 16 | collection\_name       | [collectiondata.name](http://collectiondata.name/) | Name of the collection (Denormalised for object.rollup.l1 field) | String   |
| 17 | collection\_type       | collectiondata.contenttype                         | Type of the resource                                             | String   |
| 18 | collection\_board      | collectiondata.board                               | Board of affiliation                                             | String   |

\


### **Metrics:** <a href="#rollupdatamodel-summaryevents-metrics" id="rollupdatamodel-summaryevents-metrics"></a>

| # | Dimension in Druid  | Field in  Telemetry               | Metrics type                         | DataType |
| - | ------------------- | --------------------------------- | ------------------------------------ | -------- |
| 1 | count               | N/A                               | count                                | Integer  |
| 2 | total\_time\_spent  | edata.eks.time\_spent             | longSum(edata\_time\_spent)          | Long     |
| 3 | total\_interactions | edata.eks.interact\_events\_count | doubleSum(edata\_interaction\_count) | Double   |
