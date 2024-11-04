---
icon: elementor
---

# Sunbird Design : Static data - JSON format

\\

### **Problem Statement** <a href="#staticdata-jsonformat-problemstatement" id="staticdata-jsonformat-problemstatement"></a>

Define a JSON format to store the static data to be displayed in Dashboard Metrics

\\

### **Approach 1** - Single JSON file for all static data configuration <a href="#staticdata-jsonformat-approach1-singlejsonfileforallstaticdataconfiguration" id="staticdata-jsonformat-approach1-singlejsonfileforallstaticdataconfiguration"></a>

\\

```
{
  "metricsSummary": {
    "metricsAsOnYear": "2019",
    "onboardSummary": {
      "stateCount": 26
    },
    "etbSummary": {
      "etbPrintCount": 20000000,
      "boardCount": 26
    },
    "contentCreationSummary": {
      "languages": 15,
      "teachers": 6000
    }
  },
  "onboardMetrics": {
    "states": [
      {
        "stateName": "Maharashtra",
        "onboardStatus": "Live",
        "academicYear": "2018-19"
      },
      {
        "stateName": "Assam",
        "onboardStatus": "In Progress",
        "academicYear": "2019-20"
      }
    ]
  },
  "etbPrintMetrics": {
    "boards": [
      {
        "board": "DSERT",
        "stateName": "Karnataka",
        "classes": "1,2,6,8",
        "subjects": "English, Science",
        "etbPrintCount": 20000,
        "etbAcademicYear": "2018-19",
        "status": "Live"
      },
      {
        "board": "CBSE",
        "stateName": "-",
        "classes": "6,8",
        "subjects": "Maths, Social Studies",
        "etbPrintCount": 15000,
        "etbAcademicYear": "2019-20",
        "status": "Inprogress"
      }
    ]
  }
}
```

***

### **Approach 2** - Separate JSON files to configure summary and drill down data <a href="#staticdata-jsonformat-approach2-separatejsonfilestoconfiguresummaryanddrilldowndata" id="staticdata-jsonformat-approach2-separatejsonfilestoconfiguresummaryanddrilldowndata"></a>

\\

| **Metrics Summary**        | **Onboard Metrics Drill-down Data** | **ETB Metrics Drill-down Data** |
| -------------------------- | ----------------------------------- | ------------------------------- |
| <pre><code>{
</code></pre> |                                     |                                 |
| "metricsSummary": {        |                                     |                                 |

```
"metricsAsOnYear": "2019",
"onboardSummary": {
  "stateCount": 26
},
"etbSummary": {
  "etbPrintCount": 20000000,
  "boardCount": 26
},
"contentCreationSummary": {
  "languages": 15,
  "teachers": 6000
}
```

} } |

```
{
"onboardMetrics": {
"states": [
{
"stateName": "Maharashtra",
"onboardStatus": "Live",
"academicYear": "2018-19"
},
{
"stateName": "Assam",
"onboardStatus": "In Progress",
"academicYear": "2019-20"
}
]
}
}
```

|

```
{
"etbPrintMetrics": {
"boards": [
{
"board": "DSERT",
"stateName": "Karnataka",
"classes": "1,2,6,8",
"subjects": "English, Science",
"etbPrintCount": 20000,
"etbAcademicYear": "2018-19",
"status": "Live"
},
{
"board": "CBSE",
"stateName": "-",
"classes": "6,8",
"subjects": "Maths, Social Studies",
"etbPrintCount": 15000,
"etbAcademicYear": "2019-20",
"status": "Inprogress"
}
]
}
}
```

|

***

### **Approach 3** - Separate metric-wise(summary+drill-down data) JSON configuration files <a href="#staticdata-jsonformat-approach3-separatemetric-wise-summarydrill-downdata-jsonconfigurationfiles" id="staticdata-jsonformat-approach3-separatemetric-wise-summarydrill-downdata-jsonconfigurationfiles"></a>

\\

| **Onboard Metrics**        | **ETB Metrics** | **Content Creation Metrics** |
| -------------------------- | --------------- | ---------------------------- |
| <pre><code>{
</code></pre> |                 |                              |
| "onboardMetrics": {        |                 |                              |

```
"metricsAsOnYear": "2019",
"stateCount": 26,
"states": [
  {
    "stateName": "Maharashtra",
    "onboardStatus": "Live",
    "academicYear": "2018-19"
  },
  {
    "stateName": "Assam",
    "onboardStatus": "In Progress",
    "academicYear": "2019-20"
  }
]
```

} } |

```
{
"etbPrintMetrics": {
"metricsAsOnYear": "2019",
"boardCount": 29,
"etbTotalPrintCount": 4500000000,
"boards": [
{
"board": "DSERT",
"stateName": "Karnataka",
"classes": "1,2,6,8",
"subjects": "English, Science",
"etbPrintCount": 20000,
"etbAcademicYear": "2018-19",
"status": "Live"
},
{
"board": "CBSE",
"stateName": "-",
"classes": "6,8",
"subjects": "Maths, Social Studies",
"etbPrintCount": 15000,
"etbAcademicYear": "2019-20",
"status": "Inprogress"
}
]
}
}
```

|

```
{
"contentCreationMetrics": {
"metricsAsOnYear": "2019",
"teachers": 6000,
"languages": 15
}
}
```

|
