---
icon: elementor
---

# \[Data Product] Device summarizer

#### Summary <a href="#id-dataproduct-devicesummarizer-summary" id="id-dataproduct-devicesummarizer-summary"></a>

* **Type** - Device Summary - summary of each device per day
* **Granularity** - DAY
* **Dimensions** - `period`, `did` & `channel`
* **Computation Level** - Level 1 (computed from raw telemetry)
* **Frequency** - Runs Daily

#### Purpose <a href="#id-dataproduct-devicesummarizer-purpose" id="id-dataproduct-devicesummarizer-purpose"></a>

Purpose of `Device Summarizer` to compute device level daily summary.

#### Inputs <a href="#id-dataproduct-devicesummarizer-inputs" id="id-dataproduct-devicesummarizer-inputs"></a>

* Raw Telemetry: SEARCH & INTERACT events
* ME\_WORKFLOW\_SUMMARY

#### Output <a href="#id-dataproduct-devicesummarizer-output" id="id-dataproduct-devicesummarizer-output"></a>

* ME\_DEVICE\_SUMMARY

&#x20;Expand source

```
{
    "eid" :"ME_DEVICE_SUMMARY",
    "ets" : Long, // Event generation time in epoch
    "syncts" : Long, // Event sync time in epoch
    "ver" : "1.0",
    "mid" : String, // Unique message id for the device usage for specific sync date
    "context" : {
        "pdata" : {
            "id": "AnalyticsDataPipeline",
            "model" : "DeviceSummary",
            "ver" : "1.0"
        },
        "granularity" : "DAY",
        "date_range" : {
            "from" : Long,
            "to" : Long
        }
    },
    "dimensions" : {
        "period" : Int,
        "channel": String,
        "did" : String // Device id
    },
    "edata" : {
        "eks" :{
            "total_ts": Double, // Total time spent in seconds excluding idle time.
            "total_launches": Long, // Total launches/visits.
            "contents_played": Int, // Total content played
            "unique_contents_played": Int, // Distinct content played
            "dial_stats": {
                "total_count": Int, // QR codes scanned
                "success_count": Int, // QR scans successful
                "failed_count": Int, // QR scans failed
            },
            "content_downloads": Int // Content downloaded
        }
    }
}
```

#### Algorithm Design <a href="#id-dataproduct-devicesummarizer-algorithmdesign" id="id-dataproduct-devicesummarizer-algorithmdesign"></a>

* Group By **did** and **channel**

| Field                                   | Computation                                                                                         | Remarks                  |
| --------------------------------------- | --------------------------------------------------------------------------------------------------- | ------------------------ |
| did                                     | context.did                                                                                         | <p><br></p>              |
| period                                  | Integer value of the DAY                                                                            | <p><br></p>              |
| total\_ts                               | Sum (`edata.eks.time_spent` of all the ME\_WORKFLOW\_SUMMARY events)                                | <p><br></p>              |
| context.date\_range.from(first\_access) | `context.date_range.from` of first ME\_WORKFLOW\_SUMMARY event                                      | <p><br></p>              |
| context.date\_range.to(last\_access)    | `context.date_range.to` of last ME\_WORKFLOW\_SUMMARY event                                         | <p><br></p>              |
| total\_launches                         | Count of ME\_WORKFLOW\_SUMMARY events with `dimensions.type = app`                                  | <p><br></p>              |
| contents\_played                        | Count of ME\_WORKFLOW\_SUMMARY events with `dimensions.type = content` and `dimensions.mode = play` | <p><br></p>              |
| unique\_contents\_played                | Count of unique `object.id` from content play ME\_WORKFLOW\_SUMMARY events                          | <p><br></p>              |
| dial\_stats.total\_count                | Count of SEARCH events where `edata.filters.dialcodes` exists                                       | <p><br></p>              |
| dial\_stats.success\_count              | Count of SEARCH events where `edata.filters.dialcodes` exists and `edata.size` > 0                  | <p><br></p>              |
| dial\_stats.failed\_count               | Count of SEARCH events where `edata.filters.dialcodes` exists and `edata.size` = 0                  | <p><br></p>              |
| content\_downloads                      | Count of INTERACT events with `edata.subType` = "ContentDownload-Success"                           | For portal, it will be 0 |
