---
icon: folder-open
---

# Course Dashboards

### Course Enrollment Report <a href="#coursedashboards-courseenrollmentreport" id="coursedashboards-courseenrollmentreport"></a>

### Background <a href="#coursedashboards-background" id="coursedashboards-background"></a>

Purpose of this report is to show the course wise enrollment numbers.

Users from any tenant can enrol into an open course batch. In this report only include teachers who belong to the same tenant ID as the report viewer’s tenant id.

#### **Proposed Solution:** <a href="#coursedashboards-proposedsolution" id="coursedashboards-proposedsolution"></a>

Report title: Enrollment Report by Course

X-axis: No. of enrollments

Y-axis: to have individual course names organised alphabetically

Type of Graph  :will be horizontal bar graph.

Course Enrollment Report: Sample Config JSON

```
{
  "id": "api.report",
  "ver": "1.0",
  "ts": "2019-04-25 13:54:53:905+0530",
  "params": {
    "resmsgid": "9a2b9010-6733-11e9-a5f9-a9ba66dcacb1",
    "msgid": null,
    "status": "success",
    "err": null,
    "errmsg": null
  },
  "responseCode": "OK",
  "result": [
    {
      "id": "course_enrollment_report",
      "label": "Course Enrollment Report",
      "title": "Course Enrollment Report",
      "description": "Reports related to show the course wise enrollment numbers,to show the enrollments by course as a timeline graph, to show the enrollments by district.",
      "dataSource": "/reports/sunbird/daily_metrics.json",
      "charts": [
        {
          "datasets": [
            {
              "data": [
                "54814",
                "51356",
                "67348",
                "176538",
                "214892"
              ],
              "label": "Enrollment Report by Course"
            }
          ],
          "colors": [
            {
              "borderColor": "rgb(1, 184, 170)",
              "backgroundColor": "rgba(2, 79, 157, 1)"
            }
          ],
          "labels": [
            "English Training Program",
            "Physical Science Training Program",
            "Maths Training Program"
          ],
          "chartType": "horizontalBar",
          "options": {
            "scales": {
              "yAxes": [
                {
                  "scaleLabel": {
                    "display": true,
                    "labelString": "Course Name"
                  }
                }
              ],
              "xAxes": [
                {
                  "scaleLabel": {
                    "display": true,
                    "labelString": "No of enrollments"
                  }
                }
              ]
            },
            "tooltips": {
              "intersect": false,
              "mode": "x-axis",
              "titleSpacing": 5,
              "bodySpacing": 5
            },
            "title": {
              "fontSize": 16,
              "display": true,
              "text": "Course Enrollment Report"
            },
            "legend": {
              "display": false
            },
            "responsive": true
          }
        }
      ],
      "table": {
        "columnsExpr": "keys",
        "valuesExpr": "tableData"
      },
      "downloadUrl": "/reports/sunbird/course_enrollment.csv"
    }
  ]
}
 
```

\


### Course Timespent Report <a href="#coursedashboards-coursetimespentreport" id="coursedashboards-coursetimespentreport"></a>

### Background <a href="#coursedashboards-background.1" id="coursedashboards-background.1"></a>

Purpose of this report is to show average time spent on the courses at district level.

#### **Proposed Solution:** <a href="#coursedashboards-proposedsolution-.1" id="coursedashboards-proposedsolution-.1"></a>

Report title: Time Spent Report by District

X-axis: Avg time spent (mins)

Y-axis to have individual district names organised alphabetically

Type of Graph  :will be horizontal bar graph with legend .

Course Timespent Report : Sample config.json

```
[
{
"id": "Time Spent Report By District",
"label": "Time Spent Report By District",
"title": "Time Spent Report By District",
"description": "Reports related to show the course wise enrollment numbers,to show the enrollments by course as a timeline graph, to show the enrollments by district.",
"dataSource": "/reports/sunbird/course_enrollment.json",
"charts": [
{
"datasets": [
{
"dataExpr": "data['Avergae Time spent']",
"label": "English Training program"
},
{
"dataExpr": "data['Avergae Time spent']",
"label": "Physical Science Training Program"
},
{
"dataExpr": "data['Avergae Time spent']",
"label": "Maths Training Program"
}
],
"colors": [
{
"borderColor": "rgb(242, 203, 28)",
"backgroundColor": "rgba(2, 79, 157, 1)"
},
{
"borderColor": "rgb(55, 70, 73)",
"backgroundColor": "rgba(255, 0, 0, 1)"
},
{
"borderColor": "rgb(55, 70, 73)",
"backgroundColor": "rgba(242, 203, 28, 0.2)"
}
],
"labelsExpr": "data.District",
"chartType": "horizontalBar",
"options": {
"scales": {
"yAxes": [
{
"scaleLabel": {
"display": true,
"labelString": "Name Of District"
}
}
],
"xAxes": [
{
"scaleLabel": {
"display": true,
"labelString": "Avg time spent(mins)"
}
}
]
},
"tooltips": {
"intersect": false,
"mode": "x-axis",
"titleSpacing": 5,
"bodySpacing": 5
},
"title": {
"fontSize": 16,
"display": true,
"text": "Time Spent Report By District"
},
"responsive": true
}
}
],
"table": {
"columnsExpr": "keys",
"valuesExpr": "tableData"
},
"downloadUrl": "/reports/sunbird/avg_time_spent_report.csv"
}
]
```

\


Sample: course\_enrollment.json

```
{"id":"api.report","ver":"1.0","ts":"2019-04-26 13:42:33:912+0530","params":{"resmsgid":"0b835780-67fb-11e9-a849-43872b42b8e5","msgid":null,"status":"success","err":null,"errmsg":null},"responseCode":"OK","result":{"data":{"District":["East Godavari","West Godavari","Krishna"],"Avergae Time spent":["0","500","1000","1500"]}}}
```

ScreenShot:

### Sunbird platform api details: <a href="#coursedashboards-sunbirdplatformapidetails" id="coursedashboards-sunbirdplatformapidetails"></a>

&#x20;Api details to generate reports data:

1\.

Get course batch list

```
Method : POST
URI: {{host}}/course/v1/batch/list
Description : This api will provide all associated batch details for provided courseId. This is a search api, you can call this with different request param combination.
Request body :
{
    "request": {
        "filters": {
            "courseId": [
                "do_21266334005810790415935",
                "do_2125734183857930241202"
            ]
        },
        "fields": [  // list of fields which you need 
            "identifier",
            "courseAdditionalInfo",
            "courseId",
            "id"
        ]
    }
}

Sample Data for one course batch:

 {
                    "identifier": "01266334273421312013",
                    "createdFor": [
                        "0125683555607347207"
                    ],
                    "courseAdditionalInfo": {
                        "courseName": "My creation",
                        "leafNodesCount": "7",
                        "description": "Enter description for Course",
                        "courseLogoUrl": "https://ntpstagingall.blob.core.windows.net/ntp-content-staging/content/do_21266334005810790415935/artifact/download_1540471112504.thumb.png",
                        "tocUrl": "https://ntpstagingall.blob.core.windows.net/ntp-content-staging/content/do_21266334005810790415935/artifact/do_21266334005810790415935toc.json",
                        "status": "Live"
                    },
                    "endDate": null,
                    "countIncrementDate": "2018-12-26 09:54:00:047+0000",
                    "description": "",
                    "countDecrementDate": null,
                    "updatedDate": null,
                    "completedCount": 0,
                    "countIncrementStatus": true,
                    "createdDate": "2018-12-26 09:53:59:919+0000",
                    "reportUpdatedOn": "2019-04-26T11:38:54Z",
                    "createdBy": "d32e170d-010b-4bc5-ae55-3ac5e547e35b",
                    "courseCreator": "d32e170d-010b-4bc5-ae55-3ac5e547e35b",
                    "hashTagId": "01266334273421312013",
                    "participantCount": 1,
                    "mentors": [
                        "fe1785ab-7c28-4322-bd7c-c7e926d39147"
                    ],
                    "countDecrementStatus": false,
                    "name": "Batcxh",
                    "id": "01266334273421312013",
                    "enrollmentType": "invite-only",
                    "courseId": "do_21266334005810790415935",
                    "startDate": "2018-12-26",
                    "status": 1
 }

```

2\.  Once you have batch Id you can make call of download reports api, which will provide you enrolled user details, progress etc.

\


Course dashboard reports

```
Method: GET
URI : {host}/dashboard/v1/progress/course/{batchId}/export?period=fromBegining&format=csv


Sample Data for reports: (First column is header)
User Name,Email ID,Mobile Number,District Name,Organisation Name,School Name,Enrollment Date,Course Progress
Open 8,op*******@yopmail.com,******3134,,Sunbird QA Tenant,MES2019,2019-03-25 05:29:07:049+0000,0.0%
Open 8,op*******@yopmail.com,******3134,,Sunbird QA Tenant,MES2019,2019-03-25 05:29:07:049+0000,0.0%


```

\


\
