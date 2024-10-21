---
icon: elementor
---

# Implementation design for updating the district details from derived location for District Level Report

### **Introduction:** <a href="#implementationdesignforupdatingthedistrictdetailsfromderivedlocationfordistrictlevelreport-introduct" id="implementationdesignforupdatingthedistrictdetailsfromderivedlocationfordistrictlevelreport-introduct"></a>

This document describes the design of updating the DRUID query in Analytics script for the District Level Report.

PRD Link : [District Level Report](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/1054277724/District+Level+Report)

Implementation Design Link for Derived Location : [Implementation design for Location Capture: Device and User](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/1105363340/Implementation+design+for+Location+Capture+Device+and+User)

Jira Ticket :  [SB-15589](https://project-sunbird.atlassian.net/browse/SB-15589?src=confmacro)

Currently, District level report uses **device\_loc\_state** and **device\_loc\_district** which are resolved from the IP address of the device from the device register API. As per the requirement mentioned in the above Jira ticket, the district and state details have to be taken by following priorities.

**\[Priorities mentioned in the ticket]**: System should use the following data in the given order of priority to get the location data. This applies to both Mobile App and Portal:

* If the user is an anonymous user: Use the state, district information explicitly provided by the user
* If usage is by a logged-in user: Use the state, district information in the user profile
* In either of the above two cases, if there is no state, district information: Use IP based state/town information from MaxMind + (City to District Mapping given by States)

The derived location data will be having the district and state details for the particular device as per passing the priorities. So, In the Druid query, the district and state details fields will be updated as mentioned below.

* **device\_loc\_state → derived\_loc\_state**
* **device\_loc\_district → derived\_loc\_district**

## JTBD <a href="#implementationdesignforupdatingthedistrictdetailsfromderivedlocationfordistrictlevelreport-jtbd" id="implementationdesignforupdatingthedistrictdetailsfromderivedlocationfordistrictlevelreport-jtbd"></a>

* **Jobs To Be Done: Update the DRUID query to take District from Derived location details for District level report.**

### Existing Design <a href="#implementationdesignforupdatingthedistrictdetailsfromderivedlocationfordistrictlevelreport-existingd" id="implementationdesignforupdatingthedistrictdetailsfromderivedlocationfordistrictlevelreport-existingd"></a>

Data Source: Druid

start\_date, end\_date State Name are programmatically replaced in the script.

Unique Devices Query Expand source

```
{
  "queryType": "groupBy",
  "dataSource": {
    "type": "table",
    "name": "telemetry-events"
  },
  "intervals": {
    "type": "intervals",
    "intervals": [
      "start_date/end_date"
    ]
  },
  "filter": {
    "type": "and",
    "fields": [
      {
        "type": "selector",
        "dimension": "actor_type",
        "value": "User",
        "extractionFn": null
      },
      {
        "type": "in",
        "dimension": "context_pdata_id",
        "values": [
          "prod.diksha.app",
          "prod.diksha.portal"
        ],
        "extractionFn": null
      },
      {
        "type": "selector",
        "dimension": "device_loc_state",
        "value": "state_name",
        "extractionFn": null
      }
    ]
  },
  "granularity": {
    "type": "all"
  },
  "dimensions": [
    {
      "type": "default",
      "dimension": "device_loc_district",
      "outputName": "District",
      "outputType": "STRING"
    },
    {
      "type": "default",
      "dimension": "context_pdata_id",
      "outputName": "Platform",
      "outputType": "STRING"
    }
  ],
  "aggregations": [
    {
      "fieldName": "context_did",
      "type": "distinctCount",
      "name": "Unique Devices"
    }
  ],
  "postAggregations": [],
  "having": null,
  "limitSpec": {
    "type": "NoopLimitSpec"
  },
  "context": {},
  "descending": false
}
```

QR Scans Expand source

```
{
  "queryType": "groupBy",
  "dataSource": {
    "type": "table",
    "name": "telemetry-events"
  },
  "intervals": {
    "type": "intervals",
    "intervals": [
      "start_date/end_date"
    ]
  },
  "filter": {
    "type": "and",
    "fields": [
      {
        "type": "selector",
        "dimension": "eid",
        "value": "SEARCH",
        "extractionFn": null
      },
      {
        "type": "not",
        "field": {
          "type": "selector",
          "dimension": "edata_filters_dialcodes",
          "value": null
        }
      },
      {
        "type": "in",
        "dimension": "context_pdata_id",
        "values": [
          "prod.diksha.app",
          "prod.diksha.portal"
        ],
        "extractionFn": null
      },
      {
        "type": "selector",
        "dimension": "device_loc_state",
        "value": "state_name",
        "extractionFn": null
      }
    ]
  },
  "granularity": {
    "type": "all"
  },
  "dimensions": [
    {
      "type": "default",
      "dimension": "device_loc_district",
      "outputName": "District",
      "outputType": "STRING"
    },
    {
      "type": "default",
      "dimension": "context_pdata_id",
      "outputName": "Platform",
      "outputType": "STRING"
    }
  ],
  "aggregations": [
    {
      "type": "count",
      "name": "Number of QR Scans"
    }
  ],
  "postAggregations": [],
  "having": null,
  "limitSpec": {
    "type": "NoopLimitSpec"
  },
  "context": {},
  "descending": false
}
```

Content Plays Expand source

```
{
  "queryType": "groupBy",
  "dataSource": {
    "type": "table",
    "name": "summary-events"
  },
  "intervals": {
    "type": "intervals",
    "intervals": [
      "start_date/end_date"
    ]
  },
  "filter": {
    "type": "and",
    "fields": [
      {
        "type": "in",
        "dimension": "dimensions_pdata_id",
        "values": [
          "prod.diksha.app",
          "prod.diksha.portal"
        ],
        "extractionFn": null
      },
      {
        "type": "selector",
        "dimension": "dimensions_mode",
        "value": "play"
      },
      {
        "type": "selector",
        "dimension": "dimensions_type",
        "value": "content"
      },
      {
        "type": "selector",
        "dimension": "device_loc_state",
        "value": "state_name"
      }
    ]
  },
  "granularity": {
    "type": "all"
  },
  "dimensions": [
    {
      "type": "default",
      "dimension": "device_loc_district",
      "outputName": "District",
      "outputType": "STRING"
    },
    {
      "type": "default",
      "dimension": "dimensions_pdata_id",
      "outputName": "Platform",
      "outputType": "STRING"
    }
  ],
  "aggregations": [
    {
      "type": "count",
      "name": "Number of Content Plays"
    }
  ],
  "postAggregations": [],
  "having": null,
  "limitSpec": {
    "type": "NoopLimitSpec"
  },
  "context": {},
  "descending": false
}
```

### Proposed Design <a href="#implementationdesignforupdatingthedistrictdetailsfromderivedlocationfordistrictlevelreport-proposedd" id="implementationdesignforupdatingthedistrictdetailsfromderivedlocationfordistrictlevelreport-proposedd"></a>

Data Source: Druid

Start Date, End Date and State Name are programmatically replaced in the script.

Unique Devices Query Expand source

```
{
  "queryType": "groupBy",
  "dataSource": {
    "type": "table",
    "name": "telemetry-events"
  },
  "intervals": {
    "type": "intervals",
    "intervals": [
      "start_date/end_date"
    ]
  },
  "filter": {
    "type": "and",
    "fields": [
      {
        "type": "selector",
        "dimension": "actor_type",
        "value": "User",
        "extractionFn": null
      },
      {
        "type": "in",
        "dimension": "context_pdata_id",
        "values": [
          "prod.diksha.app",
          "prod.diksha.portal"
        ],
        "extractionFn": null
      },
      {
        "type": "selector",
        "dimension": "derived_loc_state",
        "value": "state_name",
        "extractionFn": null
      }
    ]
  },
  "granularity": {
    "type": "all"
  },
  "dimensions": [
    {
      "type": "default",
      "dimension": "derived_loc_district",
      "outputName": "District",
      "outputType": "STRING"
    },
    {
      "type": "default",
      "dimension": "context_pdata_id",
      "outputName": "Platform",
      "outputType": "STRING"
    }
  ],
  "aggregations": [
    {
      "fieldName": "context_did",
      "type": "distinctCount",
      "name": "Unique Devices"
    }
  ],
  "postAggregations": [],
  "having": null,
  "limitSpec": {
    "type": "NoopLimitSpec"
  },
  "context": {},
  "descending": false
}
```

QR Scans Expand source

```
{
  "queryType": "groupBy",
  "dataSource": {
    "type": "table",
    "name": "telemetry-events"
  },
  "intervals": {
    "type": "intervals",
    "intervals": [
      "start_date/end_date"
    ]
  },
  "filter": {
    "type": "and",
    "fields": [
      {
        "type": "selector",
        "dimension": "eid",
        "value": "SEARCH",
        "extractionFn": null
      },
      {
        "type": "not",
        "field": {
          "type": "selector",
          "dimension": "edata_filters_dialcodes",
          "value": null
        }
      },
      {
        "type": "in",
        "dimension": "context_pdata_id",
        "values": [
          "prod.diksha.app",
          "prod.diksha.portal"
        ],
        "extractionFn": null
      },
      {
        "type": "selector",
        "dimension": "derived_loc_state",
        "value": "state_name",
        "extractionFn": null
      }
    ]
  },
  "granularity": {
    "type": "all"
  },
  "dimensions": [
    {
      "type": "default",
      "dimension": "derived_loc_district",
      "outputName": "District",
      "outputType": "STRING"
    },
    {
      "type": "default",
      "dimension": "context_pdata_id",
      "outputName": "Platform",
      "outputType": "STRING"
    }
  ],
  "aggregations": [
    {
      "type": "count",
      "name": "Number of QR Scans"
    }
  ],
  "postAggregations": [],
  "having": null,
  "limitSpec": {
    "type": "NoopLimitSpec"
  },
  "context": {},
  "descending": false
}
```

Content Plays Expand source

```
{
  "queryType": "groupBy",
  "dataSource": {
    "type": "table",
    "name": "summary-events"
  },
  "intervals": {
    "type": "intervals",
    "intervals": [
      "start_date/end_date"
    ]
  },
  "filter": {
    "type": "and",
    "fields": [
      {
        "type": "in",
        "dimension": "dimensions_pdata_id",
        "values": [
          "prod.diksha.app",
          "prod.diksha.portal"
        ],
        "extractionFn": null
      },
      {
        "type": "selector",
        "dimension": "dimensions_mode",
        "value": "play"
      },
      {
        "type": "selector",
        "dimension": "dimensions_type",
        "value": "content"
      },
      {
        "type": "selector",
        "dimension": "derived_loc_state",
        "value": "state_name"
      }
    ]
  },
  "granularity": {
    "type": "all"
  },
  "dimensions": [
    {
      "type": "default",
      "dimension": "derived_loc_district",
      "outputName": "District",
      "outputType": "STRING"
    },
    {
      "type": "default",
      "dimension": "dimensions_pdata_id",
      "outputName": "Platform",
      "outputType": "STRING"
    }
  ],
  "aggregations": [
    {
      "type": "count",
      "name": "Number of Content Plays"
    }
  ],
  "postAggregations": [],
  "having": null,
  "limitSpec": {
    "type": "NoopLimitSpec"
  },
  "context": {},
  "descending": false
}
```

Queries:

No queries

\
