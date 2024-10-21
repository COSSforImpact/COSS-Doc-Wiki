---
icon: elementor
---

# P2: Telemetry 'Interact' data for Library/Resources/Courses tab

### Background <a href="#p2-telemetryinteractdataforlibrary-resources-coursestab-background" id="p2-telemetryinteractdataforlibrary-resources-coursestab-background"></a>

In Sunbird for a logged in user, when the user Clicks on 'Library tab', as of now only the 'Impression' data is generated, the requirement is to generate the telemetry for click ('INTERACT') on Library and Course tabs

#### **Proposed Solution** <a href="#p2-telemetryinteractdataforlibrary-resources-coursestab-proposedsolution" id="p2-telemetryinteractdataforlibrary-resources-coursestab-proposedsolution"></a>

**INTERACT**

When user Clicked on Library tab, the structure of generated telemetry data will be&#x20;

> ```
> {
>   "eid":"INTERACT",
>   "ets":1534508236954,
>   "ver":"3.0",
>   "mid":"INTERACT:285dd6ff3ede96de64f83a9501925a5a",
>   "actor":{
>      "id":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd",
>      "type":"User"
>   },
>   "context":{
>      "channel":"b00bc992ef25f1a9a8d63291e20efc8d",
>      "pdata":{
>         "id":"dev.sunbird.portal",
>         "ver":"1.10.",
>         "pid":"sunbird-portal"
>      },
>      "env":"Library",
>      "sid":"ynAHR-RsQ2h4x_2RjQoJqrE9WGcF_V2j",
>      "did":"9b79e40024f6783174d6bc55c2e2b600",
>      "cdata":[   ],
>      "rollup":{
>         "l1":"ORG_001"
>      },
>      "uid":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd"
>   },
>   "object":{ },
>   "tags":[
>      "ORG_001"
>   ],
>   "edata":{
>      "id":"library tab",
>      "type":"click",
>      "pageid":"resources"
>   }
> }
> ```

When user clicked on the Course tab, the structure of generated telemetry data will be&#x20;

> ```
> {
>    "eid":"INTERACT",
>    "ets":1534508236954,
>    "ver":"3.0",
>    "mid":"INTERACT:285dd6ff3ede96de64f83a9501925a5a",
>    "actor":{
>       "id":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd",
>       "type":"User"
>    },
>    "context":{
>       "channel":"b00bc992ef25f1a9a8d63291e20efc8d",
>       "pdata":{
>          "id":"dev.sunbird.portal",
>          "ver":"1.10.",
>          "pid":"sunbird-portal"
>       },
>       "env":"course",
>       "sid":"ynAHR-RsQ2h4x_2RjQoJqrE9WGcF_V2j",
>       "did":"9b79e40024f6783174d6bc55c2e2b600",
>       "cdata":[  ],
>       "rollup":{
>          "l1":"ORG_001"
>       },
>       "uid":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd"
>    },
>    "object":{ },
>    "tags":[
>       "ORG_001"
>    ],
>   "edata":{
>       "id":"courses tab",
>       "type":"click",
>       "pageid":"learn"
>    }
> }
> ```

When user Clicked on Home tab, generated 'interact' telemetry data&#x20;

> ```
> {
>    "eid":"INTERACT",
>    "ets":1534508236954,
>    "ver":"3.0",
>    "mid":"INTERACT:285dd6ff3ede96de64f83a9501925a5a",
>    "actor":{
>       "id":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd",
>       "type":"User"
>    },
>    "context":{
>       "channel":"b00bc992ef25f1a9a8d63291e20efc8d",
>       "pdata":{
>          "id":"dev.sunbird.portal",
>          "ver":"1.10.",
>          "pid":"sunbird-portal"
>       },
>       "env":"home",
>       "sid":"ynAHR-RsQ2h4x_2RjQoJqrE9WGcF_V2j",
>       "did":"9b79e40024f6783174d6bc55c2e2b600",
>       "cdata":[   ],
>       "rollup":{
>          "l1":"ORG_001"
>       },
>       "uid":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd"
>    },
>    "object":{ },
>    "tags":[
>       "ORG_001"
>    ],
>    "edata":{
>       "id":"home tab",
>       "type":"click",
>       "pageid":"home"
>    }
> }
>
>
> ```

When user Click on the previous / next button of ‘Popular story’ of ‘Resource’ page, generated 'interact' telemetry data :-

> ```
> {
>    "eid":"INTERACT",
>    "ets":1534508236954,
>    "ver":"3.0",
>    "mid":"INTERACT:285dd6ff3ede96de64f83a9501925a5a",
>    "actor":{
>       "id":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd",
>       "type":"User"
>    },
>    "context":{
>       "channel":"b00bc992ef25f1a9a8d63291e20efc8d",
>       "pdata":{
>          "id":"dev.sunbird.portal",
>          "ver":"1.10.",
>          "pid":"sunbird-portal"
>       },
>       "env":"library",
>       "sid":"ynAHR-RsQ2h4x_2RjQoJqrE9WGcF_V2j",
>       "did":"9b79e40024f6783174d6bc55c2e2b600",
>       "cdata":[
>       ],
>       "rollup":{
>          "l1":"ORG_001"
>       },
>       "uid":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd"
>    },
>    "object":{ },
>    "tags":[
>       "ORG_001"
>    ],
>   "edata":{
>       "id":"resource tab",
>       "Type":"click left arrow/ click right arrow",
>       "Pageid":"learn",
>      “section” : “Popular story”
>    }
> }
> ```

### &#x20; Interact data for Webapp exited <a href="#p2-telemetryinteractdataforlibrary-resources-coursestab-interactdataforwebappexited" id="p2-telemetryinteractdataforlibrary-resources-coursestab-interactdataforwebappexited"></a>

#### **Background** <a href="#p2-telemetryinteractdataforlibrary-resources-coursestab-background.1" id="p2-telemetryinteractdataforlibrary-resources-coursestab-background.1"></a>

In Sunbird portal, on click of logout button, there is no telemetry generated, the requirement is to generate the telemetry for 'INTERACT' event.

#### **Proposed Solution** <a href="#p2-telemetryinteractdataforlibrary-resources-coursestab-proposedsolution.1" id="p2-telemetryinteractdataforlibrary-resources-coursestab-proposedsolution.1"></a>

When user Click on the logout button from any page, the genreated telemetry data is:

> ```
> {
>    "eid":"INTERACT",
>    "ets":1534508236954,
>    "ver":"3.0",
>    "mid":"INTERACT:285dd6ff3ede96de64f83a9501925a5a",
>    "actor":{
>       "id":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd",
>       "type":"User"
>    },
>    "context":{
>       "channel":"b00bc992ef25f1a9a8d63291e20efc8d",
>       "pdata":{
>          "id":"dev.sunbird.portal",
>          "ver":"1.10.",
>          "pid":"sunbird-portal"
>       },
>       "env":"public",
>       "sid":"ynAHR-RsQ2h4x_2RjQoJqrE9WGcF_V2j",
>       "did":"9b79e40024f6783174d6bc55c2e2b600",
>       "cdata":[ ],
>       "rollup":{
>          "l1":"ORG_001"
>       },
>       "uid":"781c21fc-5054-4ee0-9a02-fbb1006a4fdd"
>    },
>    "object":{ },
>    "tags":[
>       "ORG_001"
>    ],
>   "edata":{
>       "Id":"logout",
>       "Type":"click",
>       "Pageid":"page_id from where logout is clicked"
>    }
> }
>
>
>
>
>
> ```
