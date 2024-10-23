---
icon: elementor
---

# Proposed QuML Spec Changes

**Background:**\
We have identified some gaps between QuML Spec (v1) and inquiry implementation (api, service & player). In order to make inquiry QuML compliant we need to modify the schema at the inquiry api, editor, player and add/update few items in the spec as well.\
\
**Spec Changes for Question:**\
\
**Attribute Name**: answer

* answer is needed for non interactive question.

**Current QuML spec (v1):** Not Available

**Proposed QuML spec (v1.1):**

* answer also should support multi-lingual data similar to body.

```
"answer": {
    "description": "answer contains the text, graphics, media objects that describe the question’s content.",
    "oneOf": [
      {
        "type": "string",
        "description": "Answer as HTML string when the answer is used in only one language."
      },
      {
        "$ref": "#/definitions/i18nData"
      }
    ]
  }
```

**Sample Data for QuML (V1.1):**

```
"answer": "<p><span style=\"background-color:#ffffff;color:#202124;\">The challenges faced by India after independence were Partition led to arrival of 8 million people to India from Pakistan for whom homes and jobs had to be found. 500 princely states, each of which was ruled by a maharaja or a nawab, had to be convinced to join the new nation. Also, in the long run, the new nation had to adopt a political system which would best serve the hopes and expectations of its population.</span></p>"

OR

"answer":{
  "en": "<p><span style=\"background-color:#ffffff;color:#202124;\">The challenges faced by India after independence were Partition led to arrival of 8 million people to India from Pakistan for whom homes and jobs had to be found. 500 princely states, each of which was ruled by a maharaja or a nawab, had to be convinced to join the new nation. Also, in the long run, the new nation had to adopt a political system which would best serve the hopes and expectations of its population.</span></p>"
}
```

***

~~**Attribute Name**: interactionTypes~~

* need to be added for interactive questions.
* Ref: [Question Definition](https://project-sunbird.atlassian.net/wiki/spaces/CO/pages/1629356033/Question+Definition)

**Current QuML spec (v1):** Not Available

**Proposed QuML spec (v1.1):**

```
"interactionTypes": {
    "description": "interactionTypes contains the kind of interaction a interactive question can have",
    "type": "array",
    "items": {
      "type": "string",
      "enum": [
        "choice",
        "text",
        "select",
        "date",
        "file-upload",
        "canvas"
      ]
    }
  }
```

**Sample Data:**\


```
"interactionTypes": ["choice"]
```

***

**Attribute Name**: media

* spec need to be updated based on discussion (ref: [\[Design\] - Making Question Set Editor and QuML Player QuML Compliant](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3276865545/Design+-+Making+Question+Set+Editor+and+QuML+Player+QuML+Compliant) )

**Current QuML spec (v1):**

```
"media": {
    "type": "object",
    "required": [
      "id",
      "mediaType",
      "src"
    ],
    "properties": {
      "id": {
        "type": "string"
      },
      "mimeType": {
        "enum": [
          "image/png",
          "audio/mp3",
          "video/mp4",
          "video/webm"
        ]
      },
      "mediaType": {
        "enum": [
          "image",
          "audio",
          "video"
        ]
      },
      "src": {
        "type": "string"
      },
      "baseUrl": {
        "type": "string"
      }
    },
    "additionalProperties": false
  }
```

**Proposed QuML spec (v1.1):**

```
"media": {
    "type": "object",
    "required": [
      "id",
      "type",
      "src"
    ],
    "properties": {
      "id": {
        "type": "string"
      },
      "mimeType": {
        "type": "string"
      },
      "type": {
        "enum": [
          "application",
          "audio",
          "font",
          "example",
          "image",
          "message",
          "model",
          "multipart",
          "text",
          "video"
        ]
      },
      "src": {
        "type": "string"
      },
      "baseUrl": {
        "type": "string"
      }
    },
    "additionalProperties": true
  }
```

**Sample Data for QuML(V 1.1):**\


```
"media":[
  {
    "id": "do_2137498365362995201237",
    "type": "image",
    "mimeType": "image/jpeg"
    "src": "/assets/public/content/assets/do_2137498365362995201237/tea.jpeg",
    "baseUrl": "https://dev.inquiry.sunbird.org"
    // any additional properties goes here by implementation if needed.
  }
]
```

***

**Attribute Name**: responseDeclaration.mapping

* the mapping spec need to be updated.

\
**Current QuML spec (v1):**

```
"mappingDef": {
            "type": "object",
            "required": ["key", "value"],
            "properties": {
                "key": {"$ref": "#/definitions/anyTypeDef"},
                "value": {"type": "number"},
                "caseSensitive": {"type": "boolean", "default": false}
            },
            "additionalProperties": false
        }
```

**Proposed QuML spec (v1.1):**

```
"mappingDef": {
            "type": "array",
            "items": {
                "type": "object",
                "required": ["value", "score"],
                "properties": {
                    "value": {"$ref": "#/definitions/anyTypeDef"},
                    "score": {"type": "number"},
                    "caseSensitive": {"type": "boolean", "default": false}
                },
                "additionalProperties": false
            }
        }
```

**Sample Data for QuML (v1.1):**

```
"mapping": [
        {
          "value": 2,
          "score": 0.5
        },
        {
          "value": 1,
          "score": 0.25
        }
      ]
```

***

~~**Attribute Name:** interactions~~

* In Case of multiple interaction types (e.g: choice & text), the implementation can have multiple variables for each interaction types (e.g: response1 for choice and response2 for text)

\
**Current QuML spec (v1):**

```
"interactions": {
      "type": "array",
      "items": {"type": "string"},
      "description": "List of interactions present in the question."
}
```

\
**Proposed QuML spec (v1.1):**

```
"interactions": {
      "description": "List of interactions present in the question.",
      "type": "object",
      "properties": {
        "validation": {
          "type": "object",
          "properties": {
            "required": {
              "type": "string"
            }
          },
          "additionalProperties": false
        }
      },
      "additionalProperties": {
        "$ref": "#/definitions/interactionsVariableDef"
      }
    }

"interactionsVariableDef": {
      "type": "object",
      "required": ["type", "options"],
      "properties": {
        "type": {
          "type": "string"
        },
        "options": {
          "oneOf": [
            {
              "$ref": "#/definitions/optionsDef"
            },
            {
              "type": "object",
              "additionalProperties": {
                "$ref": "#/definitions/optionsDef"
              }
            }
          ]
        }
        },
      "additionalProperties": false
    }

"optionsDef": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "label": {
            "type": "string"
          },
          "value": {
            "type": "number"
          }
        },
        "additionalProperties": false
      }
    }
```

**Open Questions:**\
1\. Do we always have **options** array for all different types of interactions like date, select, canvas, file-upload?

***

**Attribute Name:** solutions

* Current Solutions Spec is not covering internal data structure.

**Current QuML spec (v1):**

```
"solutions": {
      "description": "Solutions to the question.",
      "oneOf": [
        {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "List of solutions without association to any specific language",
          "minItems": 1
        },
        {
          "type": "array",
          "items": { "$ref": "#/definitions/i18nData" },
          "description": "Solutions in different languages for multi-lingual questions.",
          "minItems": 1
        }
      ]
    }
```

**Sample Data for Quml Spec (1.0):**\


```
// for single language
{
  "solutions": [
    "solution 1 having html string",
    "solution 2 having html string",
    "solution 3 having html string"
  ]
}

//for multi language
{
  "solutions": [
    {
      "en": "solution 1 having html string"
    },
    {
      "hi": "solution 2 having html string"
    }
  ]
}
```

\
**Proposed QuML spec (v1.1):**

```
"solutions": {
      "description": "Solutions to the question.",
      "type": "object",
      "additionalProperties": {
        "oneOf": [
          {
            "type": "string"
          },
          { "$ref": "#/definitions/i18nData" }
        ]
      }
    }
```

Sample Data for QuML Spec (v1.1):

```
// for single language

{
  "solutions": {
    "solution_1": "<div>...</div>",
    "solution_2": "<div>...</div>"
  }
}

//for multi language 
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

solution_1 & solution_2 are unique identifiers for different solution
```

***

**Attribute Name:** bloomsLevel

* Data type mismatch found between spec json and wiki page.
* [https://github.com/sunbird-specs/QuML/blob/master/v1/question-schema.json](https://github.com/sunbird-specs/QuML/blob/master/v1/question-schema.json)
* [Question Definition](https://project-sunbird.atlassian.net/wiki/spaces/CO/pages/1629356033/Question+Definition)

**Current QuML spec (v1):**

```
"bloomsLevel": {
      "type": "array",
      "enum": [""],
      "description": "Cognitive processes involved to answer the question."
    }
```

**Proposed QuML spec (v1.1):**

```
"complexityLevel": {
    "type": "array",
    "items": {
      "type": "string",
    },
    "description": "Cognitive processes involved to answer the question."
  }
```

***

**Attribute Name:** feedback\
**Current QuML spec (v1):**

```
"feedback": {
      "description": "Feedback shown to the students after response processing.",
      "type": "array",
      "items": {
        "type": "object",
        "required": [ "id", "body" ],
        "properties": {
          "id": {
            "description": "Identifier of the feedback object.",
            "type": "string"
          },
          "body": {
            "description": "Body of the feedback to be rendered for the specified feedback identifier.",
            "oneOf": [
              {
                "type": "string",
                "description": "Feedback as HTML string when the question is used in only one language."
              },
              { "$ref": "#/definitions/i18nData" }
            ]
          }
        }
      }
    }
```

**Sample Data for QuML (v1.0):**

```
// single language
{
  "feedback": [
      {
        "id": "feedback_1",
        "body": "<div>...</div>"
      },
      {
        "id": "feedback_2",
        "body": "<div>...</div>"
      }
    ]
}

// multi language:

{
	"feedback": [
    {
      "id": "feedback_1",
      "body": {
        "en": "<div>...</div>",
        "hi": "<div>...</div>",
        "ka": "<div>...</div>"
      }
    },
    {
      "id": "feedback_2",
      "body": {
        "en": "<div>...</div>",
        "ka": "<div>...</div>"
      }
    }
  ]
}
```

**Proposed QuML spec (v1.1):**

```
"feedback": {
      "description": "Feedback shown to the students after response processing.",
      "type": "object",
      "additionalProperties": {
        "oneOf": [
          {
            "type": "string"
          },
          { "$ref": "#/definitions/i18nData" }
        ]
      }
    }
```

**Sample Data for QuML (v1.1):**

```
//single language:
{
  "feedback": {
    "feedback_1": "<div>...</div>",
    "feedback_2": "<div>...</div>"
  }
}


//multi language:
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

***

**Attribute Name:** hints\
**Current QuML spec (v1):**

```
"hints": {
      "description": "Hints are shown to the students after response processing or when the student requests for hints.",
      "type": "array",
      "items": {
        "type": "object",
        "required": [ "id", "body" ],
        "properties": {
          "id": {
            "description": "Identifier of the hint object.",
            "type": "string"
          },
          "body": {
            "description": "Body of the hint to be rendered for the specified hint identifier.",
            "oneOf": [
              {
                "type": "string",
                "description": "Hint as HTML string when the question is used in only one language."
              },
              { "$ref": "#/definitions/i18nData" }
            ]
          }
        }
      }
    }
```

**Sample Data for QuML (v1.0):**

```
{
  "hints": [
      {
        "id": "hint_1",
        "body": "<div>...</div>"
      },
      {
        "id": "hint_2",
        "body": {
          "en": "<div>...</div>",
          "hi": "<div>...</div>",
          "ka": "<div>...</div>"
        }
      }
    ]
}
```

**Proposed QuML spec (v1.1):**

```
"hints": {
      "description": "Hints of the question.",
      "type": "object",
      "additionalProperties": {
        "oneOf": [
          {
            "type": "string"
          },
          { "$ref": "#/definitions/i18nData" }
        ]
      }
    }
```

**Sample Data for QuML (v1.1):**

```
{
  "hints": {

    "hint_1": "<div>...</div>",

    "hint_2": {
      "en": "<div>...</div>",
      "hi": "<div>...</div>"
    }
  }
}
```

***

**Spec Changes for QuestionSet:**

* There are some special characters in line number 27 & 51. So need to re-write these lines.
* `coordinateDef` is not available but coordinate definition is available which is being referred from line number 215. So need correction at line number 215.
* media definition is missing which is being referred from `anyTypeDef` (line number: 224). So need to add media definition.\
  \
  \
  \
