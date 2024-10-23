---
icon: elementor
---

# A/B testing available framework evaluation

## **Overview** <a href="#a-btestingavailableframeworkevaluation-overview" id="a-btestingavailableframeworkevaluation-overview"></a>

**Jira Ticket:** [**SB-10068**](https://project-sunbird.atlassian.net/browse/SB-10068?src=confmacro)

As part of implementation of A/B framework, we have evaluated 4 frameworks' that are available for A/B testing. Planout (by Facebook), Wasabi (by Intuit), Alephbet & sixpack (by seatgeek)

We will list down the salient feature and comparison among this tools in following table&#x20;

\


| <p><br></p>                 | Planout                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Wasabi                                                    | Sixpack                                                                                                                                                                                                                                                                                                | Alephbet                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Implemented By**          | Facebook (Python), Hubspot(Javascript), GlassDoor (Java)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Intuit                                                    | SeatGeek                                                                                                                                                                                                                                                                                               | GingerLime                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **Server Implementation**   | Multiple - Python, Java, PHP                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Java                                                      | Python                                                                                                                                                                                                                                                                                                 | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **Event logging mechanism** | Add own logic for log-event - event object is received as an input                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Full-fledged API - for assignment, impression, engagement | API for collection impression/engagement                                                                                                                                                                                                                                                               | Stores in javascript localstore, gives plug-in point                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| License information         | BSD                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Apache 2.0                                                | BSD                                                                                                                                                                                                                                                                                                    | MIT                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Other dependency            | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Cassandra/MySQL                                           | Redis                                                                                                                                                                                                                                                                                                  | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Other standout feature      | Support's namespace  - can be used to qualify experiment further                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Has UI for configuring and looking at analytics data      | Has UI for configuring and looking at analytics data                                                                                                                                                                                                                                                   | Has support for tracking adapters, as well as allows to implement custom tracking adapter.                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Config Syntax               | <pre><code>//Extend experiment class 
//and over-ride assign function to
//initiate variants
</code></pre><pre><code>class MyExperiment extends 
PlanOut.Experiment {
</code></pre><pre><code>
assign(params, args) { 
params.set(‘foo’, new PlanOut
.Ops.Random
.UniformChoice({‘choices’: [‘a’, ‘b’], 
‘unit’: args.id})); 
}

}

//Following is way to get value out 
of experiment object
</code></pre><pre><code>var exp =
 new MyExperiment({‘id’: user.id });
console.log(“User has foo 
param set to “ + exp.get(‘foo’));
</code></pre><p><br></p> | They have back-end and UI for confguri                    | <pre><code>var session = new sixpack.Session();
session.participate('test-exp', ['alt-one'
, 'alt-two'], function (err, res) {
  if (err) throw err;
  alt = res.alternative.name
  if (alt == 'alt-one') {
    console.log('default: ' + alt);
  } else {
    console.log(alt);
  }
});
</code></pre> | <pre><code>var button_color_experiment = new AlephBet.Experiment({
  name: 'button color', 
 // the name of this experiment; required.
  variants: {  
   // variants for this experiment; required.
    blue: {
      activate: function() { 
     // activate function to execute if variant is selected
        $('#my-btn').attr('style', 'color: blue;');
      }
    },
    red: {
      activate: function() {
        $('#my-btn').attr('style', 'color: red;');
      }
    }
  },
});
</code></pre> |

It is desirable to use, just java-script implementation as minimal data storage or even just telemetry generation is enough for gathering data. So Planout/Alephbet are better fit for our purpose.

## **Sample Configuration for audience selection** <a href="#a-btestingavailableframeworkevaluation-sampleconfigurationforaudienceselection" id="a-btestingavailableframeworkevaluation-sampleconfigurationforaudienceselection"></a>

\


Syntax

```
{
  "activeExperiments": [
    {
      "ExperimentName": "<Name of experiment>", //Experiment name
      "startDate": "2019-01-01", //Start date from which experiment is applicable.
      "endDate": "2019-01-31", //End date when experiment expires
      "rendering": true/false, //toggle for enable/disable the experiement - regardless of toher paramters.
      "deploymentVersion": 1.14,
	  "rules": {
        "stateCode": [ //Value should be one of the configured
          "state1",
          "state2"..."stateN"
        ],
        "browser": [
          "browser1",
          "browser2"..."browserN"
        ],
        "userType": [
          "Student",
          "Teacher",
          ..."Other"
        ],
        "framework.id": [
          "NCF",
          ..."Framework2"
        ],
        "framework.board": [
          "CBSE",
          ..."ICSE"
        ],
        "framework.medium": [
          "English",
          ..."Telugu"
        ]
      }
    },
    {
      "ExperimentName": "<Name of experiment>""startDate": "2019-02-01",
      "endDate": "2019-02-28",
      "rendering": true/false"deploymentVersion": 1.14"rules": {
        "stateCode": [
          "state1",
          "state2"..."stateN"
        ],
        "browser": [
          "browser1",
          "browser2"..."browserN"
        ],
        "userType": [
          "Student",
          "Teacher",
          ..."Other"
        ],
        "framework.id": [
          "NCF",
          ..."Framework2"
        ],
        "framework.board": [
          "CBSE",
          ..."ICSE"
        ],
        "framework.medium": [
          "English",
          ..."Telugu"
        ]
      }
    }
  ]
}
```

\


Example configuration

```
{
  "activeExperiments": [
    {
      "ExperimentName": "TestLibPage",
      "startDate": "2019-01-01",
      "endDate": "2019-01-31",
      "rendering": true,
      "deploymentVersion": 1.14"rules": {
        'stateCode': [
          "AP",
          "KA"
        ],
        'browser': [
          "Chrome"
        ]
      }
    },
    {
      "ExperimentName": "TestLibPage",
      "startDate": "2019-02-01",
      "endDate": "2019-02-28",
      "rendering": true,
      "deploymentVersion": 1.15"rules": {
        "browser": [
          "Firefox"
        ]
      }
    }
  }
]
```

\


\
