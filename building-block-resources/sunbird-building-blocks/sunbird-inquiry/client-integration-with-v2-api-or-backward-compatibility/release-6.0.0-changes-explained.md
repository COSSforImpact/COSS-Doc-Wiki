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

* [QuML 1.1 changes](broken-reference)
* [Editor and Player changes](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player)

| **Attribute Name**                                                                                                                                                                                                                                                                                                                                                                              | **Change summary**                                                                                                                                                                                                                                                                                                                                                                                                    | **QuML 1.0 format**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | **QuML 1.1 format**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| responseDeclaration                                                                                                                                                                                                                                                                                                                                                                             | <p>Changes are as follow,</p><ul><li><p>maxScore</p><ul><li>Now part of outcomeDeclaration</li></ul></li><li><p>mapping</p><ul><li>Is a JSON Object with keys as Value and Score</li></ul></li></ul><p>Changes are applicable to Multiple Choice Question and Multi-select MCQ</p><p>Not applicable for subjective question, hence no changes</p>                                                                     | <h4 id="release6.0.0changesexplained-multiplechoicequestion">Multiple Choice Question</h4><pre><code>"responseDeclaration": {
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
}
</code></pre><h4 id="release6.0.0changesexplained-multi-selectmcq">Multi-select MCQ</h4><pre><code>"responseDeclaration": {
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
</code></pre> | <h4 id="release6.0.0changesexplained-multiplechoicequestion.1">Multiple Choice Question</h4><pre><code>"responseDeclaration": {
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
</code></pre><h4 id="release6.0.0changesexplained-multi-selectmcq.1">Multi-select MCQ</h4><pre><code>"responseDeclaration": {
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
  
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| timeLimits                                                                                                                                                                                                                                                                                                                                                                                      | <p>Changes are as follow,</p><ul><li><p>warningTime</p><ul><li>Removed as it is not part of specification</li></ul></li><li><p>maxTime</p><ul><li>Renamed to match the specification</li></ul></li><li><a href="https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#timeLimits">Details are available here for referance</a></li></ul> | <pre><code>timeLimits: {
   "maxTime": "240",
   "warningTime": "60"
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | <pre><code>{
    “timeLimits”: {
        “questionSet”: { // time limits for the question set and for any member sets
            “min”: &#x3C;seconds>,
            “max”: &#x3C;seconds>
        },
        “question”: { // time limits for the questions in the question set
            “min”: &#x3C;seconds>,
            “max”: &#x3C;seconds>
        }
    }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| maxScore                                                                                                                                                                                                                                                                                                                                                                                        | <p>Changes are as follow,</p><ul><li><p>maxScore</p><ul><li>Now part of outcomeDeclaration</li></ul></li></ul>                                                                                                                                                                                                                                                                                                        | <h4 id="release6.0.0changesexplained-question">Question</h4><pre><code>{
  maxScore: 1,
  "responseDeclaration": {
    "response1": {
        "maxScore": 1,
        .....
    }     
  } 
}







</code></pre><h4 id="release6.0.0changesexplained-questionset">QuestionSet</h4><pre><code>{
  ...
  maxScore: 10,
  ...
}



</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | <h4 id="release6.0.0changesexplained-questionlevel">Question level</h4><pre><code>{
  "outcomeDeclaration": {
    "maxScore": {
      "cardinality": "single",
      "type": "integer",
      "defaultValue": 1
    }
  }
}







</code></pre><h4 id="release6.0.0changesexplained-questionset.1">QuestionSet</h4><pre><code>{
  "outcomeDeclaration": {
    "maxScore": {
      "cardinality": "single",
      "type": "integer",
      "defaultValue": 1
    }
  }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| <p>answer</p><ul><li>There is adopter specific use case where the answer property is non-mandatory, like the Survey, Observation. Considering this case, the answer is non-mandatory in 6.0.0 release. This will need further enhancement to override answer property as mandatory or not at the QuestionSet level. Tentative time line for this change to affect is in release 6.2.0</li></ul> | <p>Changes are as follow,</p><ul><li><p>answer</p><ul><li>is mandatory for all types of questions</li><li>answers will be concatenated together under an HTML element</li><li>supports multi-lingual</li><li><a href="https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#answer">More details here</a></li></ul></li></ul>            | <pre><code>"answer": "&#x3C;p>This is test data&#x3C;/p>"
</code></pre><p>Only used for Subjective</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | <h4 id="release6.0.0changesexplained-subjective">Subjective</h4><p><strong>Single Language:</strong></p><pre><code>anwser: '&#x3C;div class="anwser-container">
    &#x3C;div class="anwser-body">
        &#x3C;p>Delhi&#x3C;/p>
    &#x3C;/div>    
&#x3C;/div>'
</code></pre><p><strong>Multi Language:</strong></p><pre><code>answer: {
  en: "&#x3C;div class="anwser-container">
          &#x3C;div class="anwser-body">
              &#x3C;p>Delhi&#x3C;/p>
          &#x3C;/div>    
       &#x3C;/div>",
  hi: "&#x3C;div class="anwser-container">
          &#x3C;div class="anwser-body">
              &#x3C;p>दिल्ली&#x3C;/p>
          &#x3C;/div>    
       &#x3C;/div>"
}
</code></pre><h4 id="release6.0.0changesexplained-mcq">MCQ</h4><p><strong>Single Language:</strong></p><pre><code>anwser: `&#x3C;div class="anwser-container">
    &#x3C;div class="anwser-body">
        &#x3C;p>Delhi&#x3C;/p>
    &#x3C;/div>    
&#x3C;/div>'
</code></pre><p><strong>Multi Language:</strong></p><pre><code>answer: {
  en: "&#x3C;div class="anwser-container">
          &#x3C;div class="anwser-body">
              &#x3C;p>Delhi&#x3C;/p>
          &#x3C;/div>    
       &#x3C;/div>",
  hi: "&#x3C;div class="anwser-container">
          &#x3C;div class="anwser-body">
              &#x3C;p>दिल्ली&#x3C;/p>
          &#x3C;/div>    
       &#x3C;/div>"
}
</code></pre><h4 id="release6.0.0changesexplained-mmcq">MMCQ</h4><p><strong>Single Language:</strong></p><pre><code>anwser: `&#x3C;div class="anwser-container">
    &#x3C;div class="anwser-body">
        &#x3C;p>Delhi&#x3C;/p>
    &#x3C;/div>
    &#x3C;div class="anwser-body">
        &#x3C;p>Bangalore&#x3C;/p>
    &#x3C;/div>
&#x3C;/div>'
</code></pre><p><strong>Multi Language:</strong></p><pre><code>answer: {
  en: "&#x3C;div class="anwser-container">
          &#x3C;div class="anwser-body">
              &#x3C;p>Delhi&#x3C;/p>
          &#x3C;/div>
          &#x3C;div class="anwser-body">
              &#x3C;p>bangalore&#x3C;/p>
          &#x3C;/div>    
       &#x3C;/div>",
  hi: "&#x3C;div class="anwser-container">
          &#x3C;div class="anwser-body">
              &#x3C;p>दिल्ली&#x3C;/p>
          &#x3C;/div> 
          &#x3C;div class="anwser-body">
              &#x3C;p>बैंगलोर&#x3C;/p>
          &#x3C;/div>   
       &#x3C;/div>"
} 
</code></pre> |
| interactions                                                                                                                                                                                                                                                                                                                                                                                    | <p>Changes are as follows,</p><ul><li><p>validation</p><ul><li>Moved under response&#x3C;1> attribute</li></ul></li></ul>                                                                                                                                                                                                                                                                                             | <pre><code>"interactions": {
    "response1": {
        "type": "choice",
        "options": [
            {
                "label": "&#x3C;p>New Delhi&#x3C;/p>",
                "value": 0
            },
            {
                "label": "&#x3C;p>Mumbai&#x3C;/p>",
                "value": 1
            }
        ]
    },
    "validation": {
        "required": "Yes"
    }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | <pre><code>"interactions": {
    "response1": {
        "type": "choice",
        "options": [
            {
                "label": "&#x3C;p>New Delhi&#x3C;/p>",
                "value": 0
            },
            {
                "label": "&#x3C;p>Mumbai&#x3C;/p>",
                "value": 1
            }
        ],
        "validation": {
          "required": "Yes"
        }
    }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| solutions                                                                                                                                                                                                                                                                                                                                                                                       | <p>Changes are as follows,</p><ul><li><p>solutions</p><ul><li>Change of type from array to object</li><li>supports multi-lingual</li></ul></li></ul>                                                                                                                                                                                                                                                                  | <h4 id="release6.0.0changesexplained-imagetext">Image + Text</h4><pre><code>"solutions": [
    {
        "id": "7015c7e4-461a-4032-b29e-fbb7e8155e44",
        "type": "html",
        "value": "&#x3C;figure class=\"image\">&#x3C;img src=\"/assets/public/content/assets/do_2137916546057256961374/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_2137916546057256961374\">&#x3C;/figure>"
    }
]
</code></pre><h4 id="release6.0.0changesexplained-video">Video</h4><pre><code>"solutions": [
    {
        "id": "70c82bf5-9459-4c43-8897-0e58b7e1da62",
        "type": "video",
        "value": "do_2137930190247526401388"
    }
]
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | <h4 id="release6.0.0changesexplained-imagetext.1">Image + Text</h4><pre><code>"solutions": {
    "7015c7e4-461a-4032-b29e-fbb7e8155e44": "&#x3C;figure class=\"image\">&#x3C;img src=\"/assets/public/content/assets/do_2137916546057256961374/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_2137916546057256961374\">&#x3C;/figure>",
}



// Key = UUID / Solution ID
</code></pre><h4 id="release6.0.0changesexplained-video.1">Video</h4><pre><code>"solutions": {
    "70c82bf5-9459-4c43-8897-0e58b7e1da62": "&#x3C;video data-asset-variable="do_2137930187513200641386" width="400" controls="" poster="/assets/public/content/assets/do_2137930188655902721387/gateway-of-india.jpg"> &#x3C;source type="video/mp4" src="/assets/public/content/assets/do_2137980528723230721410/sample-5s.mp4"> &#x3C;source type="video/webm" src="/assets/public/content/assets/do_2137980528723230721410/sample-5s.mp4"> &#x3C;/video>",
}



// Key = UUID
</code></pre><h4 id="release6.0.0changesexplained-multilanguage">Multi Language</h4><pre><code>{
  "solutions": {
    "solution_1": {
      "en": "&#x3C;div>...&#x3C;/div>",
      "hi": "&#x3C;div>...&#x3C;/div>"
    },
    "solution_2": {
      "en": "&#x3C;div>...&#x3C;/div>",
      "hi": "&#x3C;div>...&#x3C;/div>"
    }
  }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| feedback                                                                                                                                                                                                                                                                                                                                                                                        | <p>Changes are as follows,</p><ul><li><p>feedback</p><ul><li>mapping as part of outcomeDeclaration</li><li>supports multi-lingual</li></ul></li></ul>                                                                                                                                                                                                                                                                 | Currently not used in inQuiry                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | <pre><code>“feedback”: {
  “70c82bf5-9459-4c43-8897-0e58b7e1da62”: “&#x3C;h1>Well done!!!&#x3C;/h1>”,
  “70c82bf5-9459-4c43-8897-0e58b7e1da63”: “&#x3C;h1>Better luck next time!!!&#x3C;/h1>”
  “70c82bf5-9459-4c43-8897-0e58b7e1da64”: “&#x3C;h1>You need to work harder!!!&#x3C;/h1>”
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
</code></pre><h4 id="release6.0.0changesexplained-multilanguage.1">Multi Language</h4><pre><code>{
  "feedback": {
    "feedback_1": {
      "en": "&#x3C;div>...&#x3C;/div>",
      "hi": "&#x3C;div>...&#x3C;/div>"
    },
    "feedback_2": {
      "en": "&#x3C;div>...&#x3C;/div>",
      "hi": "&#x3C;div>...&#x3C;/div>"
    }
  }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| hints                                                                                                                                                                                                                                                                                                                                                                                           | <p>Changes are as follows,</p><ul><li><p>hints</p><ul><li>mapping as part of outcomeDeclaration</li><li>supports multi-lingual</li></ul></li></ul>                                                                                                                                                                                                                                                                    | <pre><code>// Question Metadata
{ 
  hints: { 
    en : "string"
  }
}










</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | <pre><code>“hints”: {
  “70c82bf5-9459-4c43-8897-0e58b7e1da62”: “&#x3C;HTML>...&#x3C;/HTML>”,
  “70c82bf5-9459-4c43-8897-0e58b7e1da63”: “&#x3C;HTML>...&#x3C;/HTML>”
  “70c82bf5-9459-4c43-8897-0e58b7e1da64”: “&#x3C;HTML>...&#x3C;/HTML>”
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
</code></pre><h4 id="release6.0.0changesexplained-multilanguage.2">Multi Language</h4><pre><code>{
  "hints": {

    "hint_1": "&#x3C;div>...&#x3C;/div>",

    "hint_2": {
      "en": "&#x3C;div>...&#x3C;/div>",
      "hi": "&#x3C;div>...&#x3C;/div>"
    }
  }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| instructions                                                                                                                                                                                                                                                                                                                                                                                    | <p>Changes are as follows,</p><ul><li><p>instructions</p><ul><li>Change of type from object to string</li><li>supports multi-lingual</li></ul></li></ul>                                                                                                                                                                                                                                                              | <h4 id="release6.0.0changesexplained-question.1">Question</h4><pre><code>{ 
  instructions: { 
    en : "&#x3C;html>...&#x3C;/html>"
  }
}
</code></pre><h4 id="release6.0.0changesexplained-questionset.2">QuestionSet</h4><pre><code>{ 
  instructions: { 
    default : "&#x3C;html>...&#x3C;/html>"
  }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | <h4 id="release6.0.0changesexplained-question.2">Question</h4><pre><code>instructions:  : "&#x3C;html>"



</code></pre><h4 id="release6.0.0changesexplained-questionset.3">QuestionSet</h4><pre><code>instructions:  : "&#x3C;html>"



</code></pre><h4 id="release6.0.0changesexplained-multilingual">Multi Lingual</h4><pre><code>{ 
  instructions: { 
    en : "&#x3C;html>...&#x3C;/html>"
  }
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| showSolutions                                                                                                                                                                                                                                                                                                                                                                                   | <p>Changes are as follows,</p><ul><li><p>showSolutions</p><ul><li>Change of type from string to boolean</li></ul></li></ul>                                                                                                                                                                                                                                                                                           | <pre><code>{ 
  showSolutions: "Yes"
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | <pre><code>{ 
  showSolutions: true
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| showTimer                                                                                                                                                                                                                                                                                                                                                                                       | <p>Changes are as follows,</p><ul><li><p>showTimer</p><ul><li>Change of type from string to boolean</li></ul></li></ul>                                                                                                                                                                                                                                                                                               | <pre><code>{ 
  showTimer: "Yes"
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | <pre><code>{ 
  showTimer: true
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| showFeedback                                                                                                                                                                                                                                                                                                                                                                                    | <p>Changes are as follows,</p><ul><li><p>showFeedback</p><ul><li>Change of type from string to boolean</li></ul></li></ul>                                                                                                                                                                                                                                                                                            | <pre><code>{ 
  showFeedback: "Yes"
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | <pre><code>{ 
  showFeedback: true
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| showHints                                                                                                                                                                                                                                                                                                                                                                                       | <p>Changes are as follows,</p><ul><li><p>showHints</p><ul><li>Change of type from string to boolean</li></ul></li></ul>                                                                                                                                                                                                                                                                                               | <pre><code>{ 
  showHints: "Yes"
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | <pre><code>{ 
  showHints: true
}
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| bloomsLevel                                                                                                                                                                                                                                                                                                                                                                                     | <p>Changes are as follows,</p><ul><li><p>bloomsLevel</p><ul><li>renamed to complexityLevel</li><li>Change of type from string to array</li></ul></li></ul>                                                                                                                                                                                                                                                            | <pre><code>bloomsLevel: "apply"
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | <pre><code>complexityLevel: ["apply"]
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| media                                                                                                                                                                                                                                                                                                                                                                                           | <p>Changes are as follows,</p><ul><li><p>media</p><ul><li>this is a spec updation only and no changes in editor / player / api</li></ul></li></ul>                                                                                                                                                                                                                                                                    | No changes to the format                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | No changes to the format                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
