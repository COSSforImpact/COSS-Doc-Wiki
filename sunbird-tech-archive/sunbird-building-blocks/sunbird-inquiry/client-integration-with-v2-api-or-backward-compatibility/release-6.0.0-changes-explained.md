---
icon: elementor
---

# Release 6.0.0 changes explained

### Context <a href="#release6.0.0changesexplained-context" id="release6.0.0changesexplained-context"></a>

As part of release 6.0.0, inQuiry building block is releasing newer versions of it’s components; QuML Editor, QuML Player and Microservice.

Behaviour of the System post 6.0.0 release is explained below.

There are 2 major changes that is part of this release

* Aligning inQuiry to latest QuML 1.1
* Additional support for Multi Lingual
  * API is extended to support multiple languages and no changes to inQuiry editor / player

### Component Versions vs QuML compatibility <a href="#release6.0.0changesexplained-componentversionsvsqumlcompatibility" id="release6.0.0changesexplained-componentversionsvsqumlcompatibility"></a>

| **Component**              | **Component version (V1)** | **Component version (V2)**                                                                                                                                                                                                                                                                          |
| -------------------------- | -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QuML Editor                | QuML 1.0                   | QuML 1.1                                                                                                                                                                                                                                                                                            |
| QuML Player                | QuML 1.0                   | QuML 1.1                                                                                                                                                                                                                                                                                            |
| inQuiry Microservice (API) | QuML 1.0                   | <p>QuML 1.1</p><p>QuML 1.0 for read only</p><ul><li>inQuiry Microservice provides a capability of reading the old Questions and QuestionSets that are in QuML 1.0.</li><li>The Questions and QuestionSets in QuML 1.0 will be temporarily transformed to QuML 1.1 format by the read APIs</li></ul> |

Support for V1 components will be deprecated in 6 months post the release of 6.0.0

### Component Versions vs API Version compatibility <a href="#release6.0.0changesexplained-componentversionsvsapiversioncompatibility" id="release6.0.0changesexplained-componentversionsvsapiversioncompatibility"></a>

| **Component** | **API (V1)**  | **API (V2)**  |
| ------------- | ------------- | ------------- |
| Editor (V1)   | Allowed       | Not permitted |
| Player (V1)   | Allowed       | Not permitted |
| Editor (V2)   | Not permitted | Allowed       |
| Player (V2)   | Not permitted | Allowed       |

### Behaviour of V2 Consumption APIs when requesting for Old or New Question / QuestionSet identifier <a href="#release6.0.0changesexplained-behaviourofv2consumptionapiswhenrequestingforoldornewquestion-questions" id="release6.0.0changesexplained-behaviourofv2consumptionapiswhenrequestingforoldornewquestion-questions"></a>

| **Scenario**                          | **QuestionSet Read**                                     | **Question List**                                        |
| ------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| Old Question / QuestionSet identifier | <p>Allowed</p><p>temporarily transformed to QuML 1.1</p> | <p>Allowed</p><p>temporarily transformed to QuML 1.1</p> |
| New Question / QuestionSet identifier | Allowed                                                  | Allowed                                                  |

### Behaviour of V2 Create and Update APIs given the specific format of Question / QuestionSet <a href="#release6.0.0changesexplained-behaviourofv2createandupdateapisgiventhespecificformatofquestion-questi" id="release6.0.0changesexplained-behaviourofv2createandupdateapisgiventhespecificformatofquestion-questi"></a>

| **QuML version**                            | **QuestionSet Create** | **QuestionSet Update** | **Question Create** | **Question Update** | **Review**    | **Publish**   |
| ------------------------------------------- | ---------------------- | ---------------------- | ------------------- | ------------------- | ------------- | ------------- |
| Questions / QuestionSets in QuML 1.0 format | Not permitted          | Not permitted          | Not permitted       | Not permitted       | Not permitted | Not permitted |
| Questions / QuestionSets in QuML 1.1 format | Allowed                | Allowed                | Allowed             | Allowed             | Allowed       | Allowed       |

To edit Questions / QuestionSets created in QuML 1.0 using the V2 system, the Question / QuestionSet should be migrated to QuML 1.1

V1 (Editor/Player/Microservice) will be deprecated in 6 months post the release of 6.0.0

### Changes for Making V2 QuML compliant <a href="#release6.0.0changesexplained-changesformakingv2qumlcompliant" id="release6.0.0changesexplained-changesformakingv2qumlcompliant"></a>

While the below table is a summary of changes, the details can be referenced from the below confluence pages

* [QuML 1.1 changes](broken-reference/)
* [Editor and Player changes](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player)

| **Attribute Name**  | **Change summary**                                                                                                                                                                                                                                                                                                                                | **QuML 1.0 format**                                                                               | **QuML 1.1 format** |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------- |
| responseDeclaration | <p>Changes are as follow,</p><ul><li><p>maxScore</p><ul><li>Now part of outcomeDeclaration</li></ul></li><li><p>mapping</p><ul><li>Is a JSON Object with keys as Value and Score</li></ul></li></ul><p>Changes are applicable to Multiple Choice Question and Multi-select MCQ</p><p>Not applicable for subjective question, hence no changes</p> | <p><strong>Multiple Choice Question</strong></p><pre><code>"responseDeclaration": {
</code></pre> |                     |

```
"response1": {
    "maxScore": 1,
    "cardinality": "single",
    "type": "integer",
    "correctResponse": {
        "value": "0",
        "outcomes": {
            "SCORE": 1
        }
    },
    "mapping": [
        {
            "response": 0,
            "outcomes": {
                "score": 1
            }
        }
    ]
}
```

}

#### Multi-select MCQ <a href="#release6.0.0changesexplained-multi-selectmcq" id="release6.0.0changesexplained-multi-selectmcq"></a>

```
"responseDeclaration": {
"response1": {
"maxScore": 1,
"cardinality": "multiple",
"type": "integer",
"correctResponse": {
"value": [1,0],
"outcomes": {
"SCORE": 1
}
},
"mapping": [
{
"response": 1,
"outcomes": {
"score": 0.5
}
},
{
"response": 0,
"outcomes": {
"score": 0.5
}
}
]
}
}
```

|

#### Multiple Choice Question <a href="#release6.0.0changesexplained-multiplechoicequestion.1" id="release6.0.0changesexplained-multiplechoicequestion.1"></a>

```
"responseDeclaration": {
"response1": {
"cardinality": "single",
"type": "integer",
"correctResponse": {
"value": 0
},
"mapping": [
{
"value": 0,
"score": 1
}
]
}
},
"outcomeDeclaration": {
"maxScore": {
"cardinality": "single",
"type": "integer",
"defaultValue": 1
}
}
```

#### Multi-select MCQ <a href="#release6.0.0changesexplained-multi-selectmcq.1" id="release6.0.0changesexplained-multi-selectmcq.1"></a>

```
"responseDeclaration": {
"response1": {
"cardinality": "multiple",
"type": "integer",
"correctResponse": {
"value": [1,0]
},
"mapping": [
{
"value": 1,
"score": 0.5
},
{
"value": 0,
"score": 0.5
}
]
}
},
"outcomeDeclaration": {
"maxScore": {
"cardinality": "multiple",
"type": "integer",
"defaultValue": 1
}
}
```

\| | timeLimits |

Changes are as follow,

* warningTime
  * Removed as it is not part of specification
* maxTime
  * Renamed to match the specification
* [Details are available here for referance](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#timeLimits)

|

```
timeLimits: {
"maxTime": "240",
"warningTime": "60"
}
```

|

```
{
“timeLimits”: {
“questionSet”: { // time limits for the question set and for any member sets
“min”: <seconds>,
“max”: <seconds>
},
“question”: { // time limits for the questions in the question set
“min”: <seconds>,
“max”: <seconds>
}
}
}
```

\| | maxScore |

Changes are as follow,

* maxScore
  * Now part of outcomeDeclaration

|

#### Question <a href="#release6.0.0changesexplained-question" id="release6.0.0changesexplained-question"></a>

```
{
maxScore: 1,
"responseDeclaration": {
"response1": {
"maxScore": 1,
.....
}

}
}
```

#### QuestionSet <a href="#release6.0.0changesexplained-questionset" id="release6.0.0changesexplained-questionset"></a>

```
{
...
maxScore: 10,
...
}
```

|

#### Question level <a href="#release6.0.0changesexplained-questionlevel" id="release6.0.0changesexplained-questionlevel"></a>

```
{
"outcomeDeclaration": {
"maxScore": {
"cardinality": "single",
"type": "integer",
"defaultValue": 1
}
}
}
```

#### QuestionSet <a href="#release6.0.0changesexplained-questionset.1" id="release6.0.0changesexplained-questionset.1"></a>

```
{
"outcomeDeclaration": {
"maxScore": {
"cardinality": "single",
"type": "integer",
"defaultValue": 1
}
}
}
```

\| |

answer

* There is adopter specific use case where the answer property is non-mandatory, like the Survey, Observation. Considering this case, the answer is non-mandatory in 6.0.0 release. This will need further enhancement to override answer property as mandatory or not at the QuestionSet level. Tentative time line for this change to affect is in release 6.2.0

|

Changes are as follow,

* answer
  * is mandatory for all types of questions
  * answers will be concatenated together under an HTML element
  * supports multi-lingual
  * [More details here](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#answer)

|

```
"answer": "<p>This is test data</p>"
```

Only used for Subjective

|

#### Subjective <a href="#release6.0.0changesexplained-subjective" id="release6.0.0changesexplained-subjective"></a>

**Single Language:**

```
anwser: '<div class="anwser-container">
<div class="anwser-body">
<p>Delhi</p>
</div>

</div>'
```

**Multi Language:**

```
answer: {
en: "<div class="anwser-container">
<div class="anwser-body">
<p>Delhi</p>
</div>

</div>",
hi: "<div class="anwser-container">
<div class="anwser-body">
<p>दिल्ली</p>
</div>

</div>"
}
```

#### MCQ <a href="#release6.0.0changesexplained-mcq" id="release6.0.0changesexplained-mcq"></a>

**Single Language:**

```
anwser: &#x3C;div class="anwser-container">     &#x3C;div class="anwser-body">         &#x3C;p>Delhi&#x3C;/p>     &#x3C;/div>     &#x3C;/div>' </code></pre><p><strong>Multi Language:</strong></p><pre><code>answer: {   en: "&#x3C;div class="anwser-container">           &#x3C;div class="anwser-body">               &#x3C;p>Delhi&#x3C;/p>           &#x3C;/div>            &#x3C;/div>",   hi: "&#x3C;div class="anwser-container">           &#x3C;div class="anwser-body">               &#x3C;p>दिल्ली&#x3C;/p>           &#x3C;/div>            &#x3C;/div>" } </code></pre><h4 id="release6.0.0changesexplained-mmcq">MMCQ</h4><p><strong>Single Language:</strong></p><pre><code>anwser: <div class="anwser-container">
<div class="anwser-body">
<p>Delhi</p>
</div>
<div class="anwser-body">
<p>Bangalore</p>
</div>
</div>'
```

**Multi Language:**

```
answer: {
en: "<div class="anwser-container">
<div class="anwser-body">
<p>Delhi</p>
</div>
<div class="anwser-body">
<p>bangalore</p>
</div>

</div>",
hi: "<div class="anwser-container">
<div class="anwser-body">
<p>दिल्ली</p>
</div>
<div class="anwser-body">
<p>बैंगलोर</p>
</div>

</div>"
}
```

\| | interactions |

Changes are as follows,

* validation
  * Moved under response<1> attribute

|

```
"interactions": {
"response1": {
"type": "choice",
"options": [
{
"label": "<p>New Delhi</p>",
"value": 0
},
{
"label": "<p>Mumbai</p>",
"value": 1
}
]
},
"validation": {
"required": "Yes"
}
}
```

|

```
"interactions": {
"response1": {
"type": "choice",
"options": [
{
"label": "<p>New Delhi</p>",
"value": 0
},
{
"label": "<p>Mumbai</p>",
"value": 1
}
],
"validation": {
"required": "Yes"
}
}
}
```

\| | solutions |

Changes are as follows,

* solutions
  * Change of type from array to object
  * supports multi-lingual

|

#### Image + Text <a href="#release6.0.0changesexplained-imagetext" id="release6.0.0changesexplained-imagetext"></a>

```
"solutions": [
{
"id": "7015c7e4-461a-4032-b29e-fbb7e8155e44",
"type": "html",
"value": "<figure class="image"><img src="/assets/public/content/assets/do_2137916546057256961374/indiagate.jpeg" alt="indiaGate" data-asset-variable="do_2137916546057256961374"></figure>"
}
]
```

#### Video <a href="#release6.0.0changesexplained-video" id="release6.0.0changesexplained-video"></a>

```
"solutions": [
{
"id": "70c82bf5-9459-4c43-8897-0e58b7e1da62",
"type": "video",
"value": "do_2137930190247526401388"
}
]
```

|

#### Image + Text <a href="#release6.0.0changesexplained-imagetext.1" id="release6.0.0changesexplained-imagetext.1"></a>

```
"solutions": {
"7015c7e4-461a-4032-b29e-fbb7e8155e44": "<figure class="image"><img src="/assets/public/content/assets/do_2137916546057256961374/indiagate.jpeg" alt="indiaGate" data-asset-variable="do_2137916546057256961374"></figure>",
}
// Key = UUID / Solution ID
```

#### Video <a href="#release6.0.0changesexplained-video.1" id="release6.0.0changesexplained-video.1"></a>

```
"solutions": {
"70c82bf5-9459-4c43-8897-0e58b7e1da62": "<video data-asset-variable="do_2137930187513200641386" width="400" controls="" poster="/assets/public/content/assets/do_2137930188655902721387/gateway-of-india.jpg"> <source type="video/mp4" src="/assets/public/content/assets/do_2137980528723230721410/sample-5s.mp4"> <source type="video/webm" src="/assets/public/content/assets/do_2137980528723230721410/sample-5s.mp4"> </video>",
}
// Key = UUID
```

#### Multi Language <a href="#release6.0.0changesexplained-multilanguage" id="release6.0.0changesexplained-multilanguage"></a>

```
{
"solutions": {
"solution_1": {
"en": "<div>...</div>",
"hi": "<div>...</div>"
},
"solution_2": {
"en": "<div>...</div>",
"hi": "<div>...</div>"
}
}
}
```

\| | feedback |

Changes are as follows,

* feedback
  * mapping as part of outcomeDeclaration
  * supports multi-lingual

\| Currently not used in inQuiry |

```
“feedback”: {
“70c82bf5-9459-4c43-8897-0e58b7e1da62”: “<h1>Well done!!!</h1>”,
“70c82bf5-9459-4c43-8897-0e58b7e1da63”: “<h1>Better luck next time!!!</h1>”
“70c82bf5-9459-4c43-8897-0e58b7e1da64”: “<h1>You need to work harder!!!</h1>”
}
// key = UUID
// Referenced from outcomeDeclaration
"outcomeDeclaration": {
"feedback": {
"cardinality": "single",
"type": "string",
"defaultValue": "70c82bf5-9459-4c43-8897-0e58b7e1da62"
}
}
```

#### Multi Language <a href="#release6.0.0changesexplained-multilanguage.1" id="release6.0.0changesexplained-multilanguage.1"></a>

```
{
"feedback": {
"feedback_1": {
"en": "<div>...</div>",
"hi": "<div>...</div>"
},
"feedback_2": {
"en": "<div>...</div>",
"hi": "<div>...</div>"
}
}
}
```

\| | hints |

Changes are as follows,

* hints
  * mapping as part of outcomeDeclaration
  * supports multi-lingual

|

```
// Question Metadata
{
hints: {
en : "string"
}
}
```

|

```
“hints”: {
“70c82bf5-9459-4c43-8897-0e58b7e1da62”: “<HTML>...</HTML>”,
“70c82bf5-9459-4c43-8897-0e58b7e1da63”: “<HTML>...</HTML>”
“70c82bf5-9459-4c43-8897-0e58b7e1da64”: “<HTML>...</HTML>”
}
// key = UUID
// Referenced from outcomeDeclaration
"outcomeDeclaration": {
"hint": {
"cardinality": "single",
"type": "string",
"defaultValue": "70c82bf5-9459-4c43-8897-0e58b7e1da62"
}
}
```

#### Multi Language <a href="#release6.0.0changesexplained-multilanguage.2" id="release6.0.0changesexplained-multilanguage.2"></a>

```
{
"hints": {
"hint_1": "&#x3C;div>...&#x3C;/div>","hint_2": {  "en": "&#x3C;div>...&#x3C;/div>",  "hi": "&#x3C;div>...&#x3C;/div>"}
}
}
```

\| | instructions |

Changes are as follows,

* instructions
  * Change of type from object to string
  * supports multi-lingual

|

#### Question <a href="#release6.0.0changesexplained-question.1" id="release6.0.0changesexplained-question.1"></a>

```
{
instructions: {
en : "<html>...</html>"
}
}
```

#### QuestionSet <a href="#release6.0.0changesexplained-questionset.2" id="release6.0.0changesexplained-questionset.2"></a>

```
{
instructions: {
default : "<html>...</html>"
}
}
```

|

#### Question <a href="#release6.0.0changesexplained-question.2" id="release6.0.0changesexplained-question.2"></a>

```
instructions:  : "<html>"
```

#### QuestionSet <a href="#release6.0.0changesexplained-questionset.3" id="release6.0.0changesexplained-questionset.3"></a>

```
instructions:  : "<html>"
```

#### Multi Lingual <a href="#release6.0.0changesexplained-multilingual" id="release6.0.0changesexplained-multilingual"></a>

```
{
instructions: {
en : "<html>...</html>"
}
}
```

\| | showSolutions |

Changes are as follows,

* showSolutions
  * Change of type from string to boolean

|

```
{
showSolutions: "Yes"
}
```

|

```
{
showSolutions: true
}
```

\| | showTimer |

Changes are as follows,

* showTimer
  * Change of type from string to boolean

|

```
{
showTimer: "Yes"
}
```

|

```
{
showTimer: true
}
```

\| | showFeedback |

Changes are as follows,

* showFeedback
  * Change of type from string to boolean

|

```
{
showFeedback: "Yes"
}
```

|

```
{
showFeedback: true
}
```

\| | showHints |

Changes are as follows,

* showHints
  * Change of type from string to boolean

|

```
{
showHints: "Yes"
}
```

|

```
{
showHints: true
}
```

\| | bloomsLevel |

Changes are as follows,

* bloomsLevel
  * renamed to complexityLevel
  * Change of type from string to array

|

```
bloomsLevel: "apply"
```

|

```
complexityLevel: ["apply"]
```

\| | media |

Changes are as follows,

* media
  * this is a spec updation only and no changes in editor / player / api

\| No changes to the format | No changes to the format |
