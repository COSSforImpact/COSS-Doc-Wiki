---
icon: elementor
---

# \[Data Model] Fill in the Blanks Questions

#### body <a href="#id-datamodel-fillintheblanksquestions-body" id="id-datamodel-fillintheblanksquestions-body"></a>

```
<div class='question-body'>
    <div class='ftb-title'>
        <p>Capital of india is [[New Delhi]], and capital of USA is [[New York]]</p>
    </div>
    <div data-text-interaction='response1' class='ftb'></div>
</div>
```

#### responseDeclaration <a href="#id-datamodel-fillintheblanksquestions-responsedeclaration" id="id-datamodel-fillintheblanksquestions-responsedeclaration"></a>

| **Format1 (Recommended)**                         | **Format2** | **Format3** |
| ------------------------------------------------- | ----------- | ----------- |
| <pre><code>"responseDeclaration": {
</code></pre> |             |             |
| "response1": {                                    |             |             |

```
"cardinality": "multiple",
"type": "string",
"correctResponse": {
  "value": [
    "New Delhi",
    "New York"
  ]
},
"mapping": [
  {
    "value": "New Delhi",
    "score": 0.5
  },
  {
    "value": "New York",
    "score": 0.5
  }
]
```

} } |

```
"responseDeclaration": {
"response1": {
"cardinality": "multiple",
"type": "string",
"correctResponse": {
"value": [
"0",
"1"
]
},
"mapping": [
{
"value": 0,
"score": 0.5
},
{
"value": 1,
"score": 0.5
}
]
}
}
```

|

```
"responseDeclaration": {
"response1": {
"cardinality": "single",
"type": "string",
"correctResponse": {
"value": "0"
},
"mapping": [
{
"value": "0",
"score": 0.5
}
]
},
"response2": {
"cardinality": "single",
"type": "string",
"correctResponse": {
"value": "1"
},
"mapping": [
{
"value": "1",
"score": 0.5
}
]
}
}
```

|

**Note:** when there are two or more blanks in the question then `cardinality` will be `multiple`. If there is only one blank in the question the `cardinality` will be `single`.

#### outcomeDeclaration <a href="#id-datamodel-fillintheblanksquestions-outcomedeclaration" id="id-datamodel-fillintheblanksquestions-outcomedeclaration"></a>

```
"outcomeDeclaration": {
        "maxScore": {
            "cardinality": "single/multiple",
            "type": "integer",
            "defaultValue": 1
        }
    }
```

#### interactions <a href="#id-datamodel-fillintheblanksquestions-interactions" id="id-datamodel-fillintheblanksquestions-interactions"></a>

| **format1 (recommened)**                              | **format2**                                | **format3** |
| ----------------------------------------------------- | ------------------------------------------ | ----------- |
| <pre><code>No need to store interaction
</code></pre> |                                            |             |
| As this is textfill no                                |                                            |             |
| options to select from so saving                      |                                            |             |
| interactions is not needed                            |                                            |             |
|                                                       | <pre><code>"interactions": {
</code></pre> |             |
| "response1": {                                        |                                            |             |

```
"type": "text",
"options": [{
    "label": "New Delhi",
    "value": 0
  },
  {
    "label": "New York",
    "value": 1
  }
]
```

}, "validation": { "required": "Yes" } } |

```
"interactions": {
"response1": {
"type": "text",
"options": [
{
"label": "New Delhi",
"value": 0
}
]
},
"response2": {
"type": "text",
"options": [
{
"label": "New York",
"value": 1
}
]
},
"validation": {
"required": "Yes"
}
```

\| | | | |

#### editorState <a href="#id-datamodel-fillintheblanksquestions-editorstate" id="id-datamodel-fillintheblanksquestions-editorstate"></a>

```
"editorState": {
        "options": [
            {
                "answer": true,
                "value": {
                    "body": "New Delhi",
                    "value": 0
                }
            },
            {
                "answer": true,
                "value": {
                    "body": "New York",
                    "value": 1
                }
            }
        ],
        "question": "<p>capital of india is [[New Delhi]]. and capital of USA is [[New York]]</p>"
    }
```

#### answer <a href="#id-datamodel-fillintheblanksquestions-answer" id="id-datamodel-fillintheblanksquestions-answer"></a>

```
<div class='answer-container'>
    <div class='answer-body'>
        <p>New Delhi</p>
    </div>
    <div class='answer-body'>
        <p>New York</p>
    </div>
</div>
```

#### templateId <a href="#id-datamodel-fillintheblanksquestions-templateid" id="id-datamodel-fillintheblanksquestions-templateid"></a>

```
templateId: "default"
```

#### primaryCategory <a href="#id-datamodel-fillintheblanksquestions-primarycategory" id="id-datamodel-fillintheblanksquestions-primarycategory"></a>

```
"primaryCategory": "Fill In The Blanks Question"
```

#### qType <a href="#id-datamodel-fillintheblanksquestions-qtype" id="id-datamodel-fillintheblanksquestions-qtype"></a>

```
"qType": "FTB"
```
