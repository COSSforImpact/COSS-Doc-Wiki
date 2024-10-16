---
icon: elementor
---

# Distinct Count Data Model - Raw Telemetry

### **Dimensions:** <a href="#distinctcountdatamodel-rawtelemetry-dimensions" id="distinctcountdatamodel-rawtelemetry-dimensions"></a>

| #  | Dimension in Druid     | Field in Telemetry                           | Description                             | Datatype |
| -- | ---------------------- | -------------------------------------------- | --------------------------------------- | -------- |
| 1  | eid                    | eid                                          | Event Id                                | String   |
| 2  | context\_channel       | context.channel                              | Channel Id                              | String   |
| 3  | context\_pdata\_id     | [context.pdata.id](http://context.pdata.id/) | Producer Id                             | String   |
| 4  | context\_pdata\_pid    | context.pdata.pid                            | Producer Process Id                     | String   |
| 5  | object\_id             | [object.id](http://object.id/)               | Content Id                              | String   |
| 6  | object\_type           | object.type                                  | Content Type                            | String   |
| 8  | content\_board         | contentdata.board                            | Board of affiliation                    | String   |
| 9  | content\_name          | [contentdata.name](http://contentdata.name/) | Name of the content                     | String   |
| 10 | derived\_loc\_state    | derivedlocationdata.state                    | Derived location state of the user      | String   |
| 11 | derived\_loc\_district | derivedlocationdata.district                 | Derived location district of the user   | String   |
| 12 | derived\_loc\_from     | derivedlocationdata.from                     | Derived location                        | String   |
| 14 | collection\_type       | collectiondata.contenttype                   | Type of the resource                    | String   |
| 15 | collection\_board      | collectiondata.board                         | Board of affiliation                    | String   |
| 16 | dialcode\_channel      | dialcodedata.channel                         | Channel for which dialcode is generated | String   |
| 17 | user\_type             | userdata.type                                | Type of user                            | String   |
| 18 | user\_signin\_type     | userdata.usersignintype                      | User sign-in type info                  | String   |

\


### **Metrics:** <a href="#distinctcountdatamodel-rawtelemetry-metrics" id="distinctcountdatamodel-rawtelemetry-metrics"></a>

| # | Dimension in Druid | Field in  Telemetry | Metrics type   | Description           |
| - | ------------------ | ------------------- | -------------- | --------------------- |
| 1 | unique\_devices    | context\_did        | HLLSketchBuild | No of  unique devices |
| 2 | unique\_users      | actor\_id           | HLLSketchBuild | No of  unique users   |
| 3 | unique\_content    | object\_id          | HLLSketchBuild | No of  unique content |
