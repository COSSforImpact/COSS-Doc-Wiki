---
icon: elementor
---

# \[Data Model] Arrange Sequence Questions

### Background <a href="#id-datamodel-arrangesequencequestions-background" id="id-datamodel-arrangesequencequestions-background"></a>

We want to implement Arrange Sequence Question in the Questionset Editor and the QuML Player.

Before starting the implementation we need to decide Arrange sequence Question data model which is to be as per the QuML spec.

### Proposed Data Model of Arrange Sequence Question <a href="#id-datamodel-arrangesequencequestions-proposeddatamodelofarrangesequencequestion" id="id-datamodel-arrangesequencequestions-proposeddatamodelofarrangesequencequestion"></a>

#### body <a href="#id-datamodel-arrangesequencequestions-body" id="id-datamodel-arrangesequencequestions-body"></a>

```
<div class='question-body' tabindex='-1'>
    <div class='asq-title' tabindex='0'>
        <p>Arrange the fruits in alphabetic order</p>
    </div>
    <div data-order-interaction='response1' class='asq-vertical/asq-horizontal'></div>
</div>
```

#### responseDeclaration <a href="#id-datamodel-arrangesequencequestions-responsedeclaration" id="id-datamodel-arrangesequencequestions-responsedeclaration"></a>

**Proposed format1 (Recommended)**

Proposed format of responseDeclaration

```
{
    "response1": {
        "cardinality": "ordered",
        "type": "integer",
        "correctResponse": {
            "value": [
                0,
                1,
                2,
                3
            ]
        },
        "mapping": [
            {
                "value": 0,
                "score": 0.25
            },
            {
                "value": 1,
                "score": 0.25
            },
            {
                "value": 2,
                "score": 0.25
            },
            {
                "value": 3,
                "score": 0.25
            }
        ]
    }
}
```

**Pros:** We will not have to save long options text in the responseDeclaration, when the options will be having images the text of options will become to long and data will become un-readble.

**Cons:** We will not get to see the options value in the responseDeclaration

**Proposed format2**

Proposed format of responseDeclaration

```
"responseDeclaration": {
        "response1": {
            "cardinality": "ordered",
            "type": "integer",
            "correctResponse": {
                "value": ["<p>Apple</p>","<p>Banana</p>","<p>Grapes</p>","<p>Orange</p>"]
            },
            "mapping": [
                {
                    "value": "<p>Apple</p>",
                    "score": 0.25
                },
                {
                    "value": "<p>Banana</p>",
                    "score": 0.25
                },
                {
                    "value": "<p>Grapes</p>",
                    "score": 0.25
                },
                {
                    "value": "<p>Orange</p>",
                    "score": 0.25
                }
            ]
        }
    }
```

#### outcomeDeclaration <a href="#id-datamodel-arrangesequencequestions-outcomedeclaration" id="id-datamodel-arrangesequencequestions-outcomedeclaration"></a>

```
{
    "maxScore": {
        "cardinality": "ordered",
        "type": "integer",
        "defaultValue": 1
    }
}
```

#### interactions <a href="#id-datamodel-arrangesequencequestions-interactions" id="id-datamodel-arrangesequencequestions-interactions"></a>

```
{
    "response1": {
        "type": "order",
        "options": [
            {
                "label": "<p>Apple</p>",
                "value": 0
            },
            {
                "label": "<p>Banana</p>",
                "value": 1
            },
            {
                "label": "<p>Grapes</p>",
                "value": 2
            },
            {
                "label": "<p>Orange</p>",
                "value": 3
            }
        ],
        "validation": {
            "required": "Yes"
        }
    }
}
```

#### answer <a href="#id-datamodel-arrangesequencequestions-answer" id="id-datamodel-arrangesequencequestions-answer"></a>

```
<div class='answer-container'>
    <div class='answer-body'>
        <p>Apple</p>
    </div>
    <div class='answer-body'>
        <p>Banana</p>
    </div>
    <div class='answer-body'>
        <p>Grapes</p>
    </div>
    <div class='answer-body'>
        <p>Orange</p>
    </div>
</div>
```

#### editorState <a href="#id-datamodel-arrangesequencequestions-editorstate" id="id-datamodel-arrangesequencequestions-editorstate"></a>

editor state of question

```
{
    "options": [
        {
            "value": {
                "body": "<p>Apple</p>",
                "value": 0
            }
        },
        {
            "value": {
                "body": "<p>Banana</p>",
                "value": 1
            }
        },
        {
            "value": {
                "body": "<p>Grapes</p>",
                "value": 2
            }
        },
        {
            "value": {
                "body": "<p>Orange</p>",
                "value": 3
            }
        }
    ],
    "question": "<p>Arrange the fruits names in alphabetical order</p>",
    "solutions": [
        {
            "id": "71efa845-2856-4a82-b493-101facfddd26",
            "type": "html",
            "value": "<p>Proper order is Apple, Banana, Grapes, Orange</p>"
        }
    ]
}
```

#### templateId <a href="#id-datamodel-arrangesequencequestions-templateid" id="id-datamodel-arrangesequencequestions-templateid"></a>

```
"templateId": "asq-horizontal" / "asq-vertical"
```

#### primaryCategory <a href="#id-datamodel-arrangesequencequestions-primarycategory" id="id-datamodel-arrangesequencequestions-primarycategory"></a>

```
"primaryCategory": "Arrange Sequence Question"
```

#### qType <a href="#id-datamodel-arrangesequencequestions-qtype" id="id-datamodel-arrangesequencequestions-qtype"></a>

```
"qType": "ASQ" // This will need spec change
```

#### interactionTypes <a href="#id-datamodel-arrangesequencequestions-interactiontypes" id="id-datamodel-arrangesequencequestions-interactiontypes"></a>

```
"interactionTypes": ["order"] // This will need spec change
```

***

#### Let’s Compare ASQ with MCQ data <a href="#id-datamodel-arrangesequencequestions-letscompareasqwithmcqdata" id="id-datamodel-arrangesequencequestions-letscompareasqwithmcqdata"></a>

**Compare MCQ body with ASQ body**

MCQ body vs ASQ body

| **MCQ Body**                                                            | **ASQ Body** |
| ----------------------------------------------------------------------- | ------------ |
| <pre><code>&#x3C;div class='question-body' tabindex='-1'>
</code></pre> |              |

```
&#x3C;div class='mcq-title' tabindex='0'>
    &#x3C;p>Which of the fruits is red in colour?&#x3C;/p>
&#x3C;/div>
&#x3C;div data-choice-interaction='response1' class='mcq-vertical'>&#x3C;/div>
```

\</div> |

```
<div class='question-body' tabindex='-1'>
<div class='asq-title' tabindex='0'>
<p>Arrange the fruits in alphabetic order</p>
</div>
<div data-order-interaction='response1' class='asq-vertical/asq-horizontal'></div>
</div>
```

|

**Compare MCQ interactions with ASQ interactions**

MCQ interactions vs ASQ interactions

| **MCQ interactions**       | **ASQ interactions** |
| -------------------------- | -------------------- |
| <pre><code>{
</code></pre> |                      |

```
"response1": {
    "type": "choice",
    "options": [
        {
            "label": "&#x3C;p>Apple&#x3C;/p>",
            "value": 0
        },
        {
            "label": "&#x3C;p>Banana&#x3C;/p>",
            "value": 1
        },
        {
            "label": "&#x3C;p>Grapes&#x3C;/p>",
            "value": 2
        },
        {
            "label": "&#x3C;p>Orange&#x3C;/p>",
            "value": 3
        }
    ],
    "validation": {
        "required": "Yes"
    }
}
```

} |

```
{
"response1": {
"type": "order",
"options": [
{
"label": "<p>Apple</p>",
"value": 0
},
{
"label": "<p>Banana</p>",
"value": 1
},
{
"label": "<p>Grapes</p>",
"value": 2
},
{
"label": "<p>Orange</p>",
"value": 3
}
],
"validation": {
"required": "Yes"
}
}
}
```

|

**Compare MCQ responseDeclaration with MTF responseDeclaration**

MCQ responseDeclaration vs MTF responseDeclaration

| **MCQ responseDeclaration (multi choice)** | **ASQ responseDeclaration** |
| ------------------------------------------ | --------------------------- |
| <pre><code>{
</code></pre>                 |                             |

```
"response1": {
    "cardinality": "multiple",
    "type": "integer",
    "correctResponse": {
        "value": [0,3]
    },
    "mapping": [
        {
            "value": 0,
            "score": 0.5
        },
        {
            "value": 3,
            "score": 0.5
        }
    ]
}
```

} |

```
{
"response1": {
"cardinality": "ordered",
"type": "integer",
"correctResponse": {
"value": [0,1,2,3]
},
"mapping": [
{
"value": 0,
"score": 0.25
},
{
"value": 1,
"score": 0.25
},
{
"value": 2,
"score": 0.25
},
{
"value": 3,
"score": 0.25
}
]
}
}
```

|

**Compare MCQ outcomeDeclaration with ASQ outcomeDeclaration**

MCQ outcomeDeclaration vs ASQ outcomeDeclaration

| MCQ outcomeDeclaration     | ASQ outcomeDeclaration |
| -------------------------- | ---------------------- |
| <pre><code>{
</code></pre> |                        |

```
    "maxScore": {
        "cardinality": "multiple",
        "type": "integer",
        "defaultValue": 1
    }
}
```

|

```
{
"maxScore": {
"cardinality": "ordered",
"type": "integer",
"defaultValue": 1
}
}
```

|

**Compare MCQ editorState with MTF editorState**

MCQ editorState vs MTF editorState

| MCQ editorState            | MTF editorState |
| -------------------------- | --------------- |
| <pre><code>{
</code></pre> |                 |

```
"options": [
    {
        "answer": true,
        "value": {
            "body": "&#x3C;p>Apple&#x3C;/p>",
            "value": 0
        }
    },
    {
        "answer": false,
        "value": {
            "body": "&#x3C;p>Banana&#x3C;/p>",
            "value": 1
        }
    },
    {
        "answer": false,
        "value": {
            "body": "&#x3C;p>Grapes&#x3C;/p>",
            "value": 2
        }
    },
    {
        "answer": true,
        "value": {
            "body": "&#x3C;p>Strawberry&#x3C;/p>",
            "value": 3
        }
    }
],
"question": "&#x3C;p>Which of the fruits is red in colour?&#x3C;/p>",
"solutions": [
    {
        "id": "71efa845-2856-4a82-b493-101facfddd26",
        "type": "html",
        "value": "&#x3C;p>Apple is red in colour&#x3C;/p>"
    }
]
```

} |

```
{
"options": [
{
"value": {
"body": "<p>Apple</p>",
"value": 0
}
},
{
"value": {
"body": "<p>Banana</p>",
"value": 1
}
},
{
"value": {
"body": "<p>Grapes</p>",
"value": 2
}
},
{
"value": {
"body": "<p>Orange</p>",
"value": 3
}
}
],
"question": "<p>Arrange the fruits names in alphabetical order</p>",
"solutions": [
{
"id": "71efa845-2856-4a82-b493-101facfddd26",
"type": "html",
"value": "<p>Proper order is Apple, Banana, Grapes, Orange</p>"
}
]
}
```

|

***

**Complete ASQ Question Metadata Example:**

ASQ question metadata

```
{
    "mimeType": "application/vnd.sunbird.question",
    "media": [],
    "editorState": {
        "options": [
            {
                "value": {
                    "body": "<p>One</p>",
                    "value": 0
                }
            },
            {
                "value": {
                    "body": "<p>Two</p>",
                    "value": 1
                }
            },
            {
                "value": {
                    "body": "<p>Three</p>",
                    "value": 2
                }
            },
            {
                "value": {
                    "body": "<p>Four</p>",
                    "value": 3
                }
            }
        ],
        "question": "<p>Arrange the numbers in ascending order</p>",
        "solutions": [
            {
                "id": "81938f25-62b2-458d-8e23-dc0223a6c3x7",
                "type": "html",
                "value": "<p>One</p><p>Two</p><p>Three</p><p>Four</p>"
            }
        ]
    },
    "templateId": "asq-vertical",
    "complexityLevel": [],
    "maxScore": 1,
    "name": "ASQ Number",
    "qumlVersion": 1.1,
    "responseDeclaration": {
        "response1": {
            "cardinality": "ordered",
            "type": "integer",
            "correctResponse": {
                "value": [
                    0,
                    1,
                    2,
                    3
                ]
            },
            "mapping": [
                {
                    "value": 0,
                    "score": 0.25
                },
                {
                    "value": 1,
                    "score": 0.25
                },
                {
                    "value": 2,
                    "score": 0.25
                },
                {
                    "value": 3,
                    "score": 0.25
                }
            ]
        }
    },
    "outcomeDeclaration": {
        "maxScore": {
            "cardinality": "ordered",
            "type": "integer",
            "defaultValue": 1
        }
    },
    "interactionTypes": [
        "order"
    ],
    "interactions": {
        "response1": {
            "type": "order",
            "options": [
                {
                    "label": "<p>One</p>",
                    "value": 0
                },
                {
                    "label": "<p>Two</p>",
                    "value": 1
                },
                {
                    "label": "<p>Three</p>",
                    "value": 2
                },
                {
                    "label": "<p>Four</p>",
                    "value": 3
                }
            ],
            "validation": {
                "required": "Yes"
            }
        }
    },
    "qType": "ASQ",
    "primaryCategory": "Arrange Sequence Question",
    "body": "<div class='question-body' tabindex='-1'><div class='asq-title' tabindex='0'><p>Match the following colour with the fruits</p></div><div data-match-interaction='response1' class='asq-vertical'></div></div>",
    "answer": "<div class='arrange-sequence-container'><div class='options'><div class='option'><p>One</p></div><div class='option'><p>Two</p></div><div class='option'><p>Three</p></div><div class='option'><p>Four</p></div></div></div>",
    "solutions": {
        "81938f25-62b2-458d-8e23-dc0223a6c3x7": "<p>Numbers in ascending order is One,Two, Three, Four</p>"
    }
}
```
