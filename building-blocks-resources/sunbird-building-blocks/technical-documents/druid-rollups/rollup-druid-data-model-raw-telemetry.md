---
icon: elementor
---

# Rollup-Druid-Data-Model----Raw-Telemetry

**Dimensions:**

| #  | Dimensions in Druid    | Field in Telemetry                                | Description                                                      | Datatype |
| -- | ---------------------- | ------------------------------------------------- | ---------------------------------------------------------------- | -------- |
| 1  | eid                    | eid                                               | Event Id                                                         | String   |
| 2  | context\_channel       | context.channel                                   | Channel Id                                                       | String   |
| 3  | context\_pdata\_id     | [context.pdata.id](http://context.pdata.id)       | Producer Id                                                      | String   |
| 4  | context\_pdata\_pid    | context.pdata.pid                                 | Producer Process Id                                              | String   |
| 5  | object\_id             | [object.id](http://object.id)                     | Content Id                                                       | String   |
| 6  | object\_type           | object.type                                       | Content Type                                                     | String   |
| 7  | object\_rollup\_l1     | object.rollup.l1                                  | Content level 1 rollup                                           | String   |
| 8  | content\_board         | contentdata.board                                 | Board of affiliation                                             | String   |
| 9  | content\_name          | [contentdata.name](http://contentdata.name)       | Name of the content                                              | String   |
| 10 | derived\_loc\_state    | derivedlocationdata.state                         | Derived location state of the user                               | String   |
| 11 | derived\_loc\_district | derivedlocationdata.district                      | Derived location district of the user                            | String   |
| 12 | derived\_loc\_from     | derivedlocationdata.from                          | Derived location                                                 | String   |
| 13 | collection\_name       | [collectiondata.name](http://collectiondata.name) | Name of the collection (Denormalised for object.rollup.l1 field) | String   |
| 14 | collection\_type       | collectiondata.contenttype                        | Type of the resource                                             | String   |
| 15 | collection\_board      | collectiondata.board                              | Board of affiliation                                             | String   |
| 16 | dialcode\_channel      | dialcodedata.channel                              | Channel for which dialcode is generated                          | String   |
| 17 | user\_type             | userdata.type                                     | Type of user                                                     | String   |
| 18 | user\_signin\_type     | userdata.usersignintype                           | User sign-in type info                                           | String   |
| 19 | edata\_item\_id        | [edata.item.id](http://edata.item.id)             | ASSESS event Assessment item id                                  | String   |
| 20 | edata\_item\_title     | edata.item.title                                  | ASSESS event Assessment item title                               | String   |
| 21 | edata\_state           | edata.state                                       | AUDIT event current state                                        | String   |

**Metrics:**

| # | Dimensions in Druid    | Field in Telemetry  | Description                                 | Datatype |
| - | ---------------------- | ------------------- | ------------------------------------------- | -------- |
| 1 | total\_count           | NA                  | count(\*)                                   | Long     |
| 2 | total\_edata\_duration | edata.duration      | Rolled up metric - sum(edata.duration)      | Double   |
| 3 | total\_edata\_rating   | edata.rating        | Rolled up metric - sum(edata.rating)        | Double   |
| 4 | total\_edata\_score    | edata.score         | Rolled up metric - sum(edata.score)         | Double   |
| 5 | total\_max\_score      | edata.item.maxscore | Rolled up metric - sum(edata.item.maxscore) | Double   |

***

\[\[category.storage-team]] \[\[category.confluence]]
