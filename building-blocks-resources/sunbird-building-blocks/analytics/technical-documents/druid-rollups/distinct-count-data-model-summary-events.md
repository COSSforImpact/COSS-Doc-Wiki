---
icon: elementor
---

# Distinct-Count-Data-Model---Summary-Events

**Dimensions:**

| #  | Dimension in Druid     | Field in Telemetry                                | Description                                 | Datatype |
| -- | ---------------------- | ------------------------------------------------- | ------------------------------------------- | -------- |
| 1  | ets                    | context\_date\_range\_to                          | Event timestamp                             | Long     |
| 2  | dimensions\_channel    | dimensions.channel                                | Channel Id as dimension from raw telemetry  | String   |
| 3  | dimensions\_pdata\_id  | [dimensions.pdata.id](http://dimensions.pdata.id) | Producer Id as dimension from raw telemetry | String   |
| 4  | dimensions\_pdata\_ver | dimensions.pdata.ver                              | Producer version number                     | String   |
| 5  | dimensions\_type       | dimensions.type                                   | Type of summary                             | String   |
| 6  | dimensions\_mode       | dimensions.mode                                   | Mode of the summary                         | String   |
| 7  | content\_board         | contentdata.board                                 | Mode of action in the session               | String   |
| 8  | content\_name          | [contentdata.name](http://contentdata.name)       | Name of the content                         | String   |
| 9  | content\_type          | contentdata.contenttype                           | Type of the resource                        | String   |
| 10 | content\_gradelevel    | contendata.gradelevel                             | Type of gradelevel                          | String   |
| 11 | object\_id             | [object.id](http://object.id)                     | Content Id                                  | String   |
| 12 | object\_rollup\_l1     | object.rollup.l1                                  | Object level1 rollup                        | String   |
| 13 | derived\_loc\_state    | derivedlocationdata.state                         | Derived location state of the user          | String   |
| 14 | derived\_loc\_district | derivedlocationdata.district                      | Derived location district of the user       | String   |

**Metrics:**

| # | Dimension in Druid | Field in Telemetry | Description    | Datatype             |
| - | ------------------ | ------------------ | -------------- | -------------------- |
| 1 | unique\_devices    | dimenstion\_did    | HLLSketchBuild | No of unique devices |
| 2 | unique\_users      | actor\_id          | HLLSketchBuild | No of unique users   |

***

\[\[category.storage-team]] \[\[category.confluence]]
