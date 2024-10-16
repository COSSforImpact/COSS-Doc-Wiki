---
icon: elementor
---

# \[Data Model] Match The Following Question

### Background <a href="#id-datamodel-matchthefollowingquestion-background" id="id-datamodel-matchthefollowingquestion-background"></a>

We have received the MTF Question contribution in the C4GT 2023 program for the editor and the code is merged one of the feature branch.

Player side implementation is not done yet, before starting the player implementation we need to re-look into the MTF data model if it’s as per the QuML spec and if any improvement can be done in it to make it easy to understand.

### Data Model of MTF Question <a href="#id-datamodel-matchthefollowingquestion-datamodelofmtfquestion" id="id-datamodel-matchthefollowingquestion-datamodelofmtfquestion"></a>

#### body <a href="#id-datamodel-matchthefollowingquestion-body" id="id-datamodel-matchthefollowingquestion-body"></a>

```
<div class='question-body' tabindex='-1'>
    <div class='mtf-title' tabindex='0'>
        <p>Match the colour with the fruits.</p>
    </div>
    <div data-match-interaction='response1' class='mtf-horizontal'></div>
</div>
```

Question [body](https://github.com/Sunbird-inQuiry/inquiry-api-service/blob/release-7.0.0/schemas/question/1.1/schema.json#L286) is per the QuML spec

#### responseDeclaration - C4GT 2023 contributed Format <a href="#id-datamodel-matchthefollowingquestion-responsedeclaration-c4gt2023contributedformat" id="id-datamodel-matchthefollowingquestion-responsedeclaration-c4gt2023contributedformat"></a>

C4GT contribution exits in feature branch - [C4GT\_Issue\_42](https://github.com/Sunbird-inQuiry/editor/tree/C4GT\_Issue\_42)

```
{
        "response1": {
            "cardinality": "multiple",
            "type": "map",
            "correctResponse": {
                "value": [
                    {
                        "0": 0
                    },
                    {
                        "1": 1
                    },
                    {
                        "2": 2
                    },
                    {
                        "3": 3
                    }
                ]
            },
            "mapping": [
                {
                    "value": {
                        "0": 0
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "1": 1
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "2": 2
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "3": 3
                    },
                    "score": 0.25
                }
            ]
        }
    }
```

[responseDeclaration](https://github.com/Sunbird-inQuiry/inquiry-api-service/blob/release-7.0.0/schemas/question/1.1/schema.json#L411C6-L411C25) is as per the QuML spec

But above format of responseDeclaration it not self explanatory

**Here are few new proposed Format for responseDeclaration**

Cardinality for MTF Question should be `"cardinality": "ordered"`

**Format1 (Recommended)**

Proposed Format1 of responseDeclaration:

```
{
    "response1": {
        "cardinality": "ordered",
        "type": "map",
        "correctResponse": {
            "value": [
                {
                    "lhs": 0,
                    "rhs": 0
                },
                {
                    "lhs": 1,
                    "rhs": 1
                },
                {
                    "lhs": 2,
                    "rhs": 2
                },
                {
                    "lhs": 3,
                    "rhs": 3
                }
            ]
        },
        "mapping": [
            {
                "value": {
                    "lhs": 0,
                    "rhs": 0
                },
                "score": 0.25
            },
            {
                "value": {
                    "lhs": 1,
                    "rhs": 1
                },
                "score": 0.25
            },
            {
                "value": {
                    "lhs": 2,
                    "rhs": 2
                },
                "score": 0.25
            },
            {
                "value": {
                    "lhs": 3,
                    "rhs": 3
                },
                "score": 0.25
            }
        ]
    }
}
```

**Format2**

Proposed Format2 of responseDeclaration:

```
{
    "response1": {
        "cardinality": "ordered",
        "type": "map",
        "correctResponse": {
            "value": [
                {
                    "leftIndex": 0,
                    "rightIndex": 0
                },
                {
                    "leftIndex": 1,
                    "rightIndex": 1
                },
                {
                    "leftIndex": 2,
                    "rightIndex": 2
                },
                {
                    "leftIndex": 3,
                    "rightIndex": 3
                }
            ]
        },
        "mapping": [
            {
                "value": {
                    "leftIndex": 0,
                    "rightIndex": 0
                },
                "score": 0.25
            },
            {
                "value": {
                    "leftIndex": 1,
                    "rightIndex": 1
                },
                "score": 0.25
            },
            {
                "value": {
                    "leftIndex": 2,
                    "rightIndex": 2
                },
                "score": 0.25
            },
            {
                "value": {
                    "leftIndex": 3,
                    "rightIndex": 3
                },
                "score": 0.25
            }
        ]
    }
}
```

**Format3**

Proposed Format3 of responseDeclaration:

```
{
    "response1": {
        "cardinality": "ordered",
        "type": "map",
        "correctResponse": {
            "value": [
                {
                    "left": 0,
                    "right": 0
                },
                {
                    "left": 1,
                    "right": 1
                },
                {
                    "left": 2,
                    "right": 2
                },
                {
                    "left": 3,
                    "right": 3
                }
            ]
        },
        "mapping": [
            {
                "value": {
                    "left": 0,
                    "right": 0
                },
                "score": 0.25
            },
            {
                "value": {
                    "left": 1,
                    "right": 1
                },
                "score": 0.25
            },
            {
                "value": {
                    "left": 2,
                    "right": 2
                },
                "score": 0.25
            },
            {
                "value": {
                    "left": 3,
                    "right": 3
                },
                "score": 0.25
            }
        ]
    }
}
```

Final Format of responseDeclaration: **?**

**Note** - [cardinality enum](https://github.com/Sunbird-inQuiry/inquiry-api-service/blob/release-7.0.0/schemas/question/1.1/schema.json#L421) should be changed in inQuiry schema to fit in `"cardinality": "ordered"`

Since MTF and Arrange Sequence question is type of question where score is calculated based on order of response, the `cardinality` should be `ordered`. Refer [QuML spec - cardinality](https://quml.sunbird.org/v1/common#cardinality)

#### outcomeDeclaration <a href="#id-datamodel-matchthefollowingquestion-outcomedeclaration" id="id-datamodel-matchthefollowingquestion-outcomedeclaration"></a>

```
{
        "maxScore": {
            "cardinality": "ordered",
            "type": "integer",
            "defaultValue": 1
        }
    }
```

For more info on outcomeDeclarartion - [refer](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/3276865545/Design+-+Making+Question+Set+Editor+and+QuML+Player+QuML+Compliant) , [reference2](https://github.com/krgauraw/QuML/blob/v1.1\_local/v1.1/question-schema.json#L320)

#### interactions <a href="#id-datamodel-matchthefollowingquestion-interactions" id="id-datamodel-matchthefollowingquestion-interactions"></a>

```
{
    "response1": { 
        "type": "match",
        "options": {
            "left": [
                {
                    "label": "<p>Red</p>",
                    "value": 0
                },
                {
                    "label": "<p>Yellow</p>",
                    "value": 1
                },
                {
                    "label": "<p>Green</p>",
                    "value": 2
                },
                {
                    "label": "<p>Orange</p>",
                    "value": 3
                }
            ],
            "right": [
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
            ]
        },
        "validation": {
            "required": "Yes"
        }
    }
}
```

Question [interactions](https://github.com/Sunbird-inQuiry/inquiry-api-service/blob/release-7.0.0/schemas/question/1.1/schema.json#L455) is of type object so it is as per the QuML spec

#### editorState <a href="#id-datamodel-matchthefollowingquestion-editorstate" id="id-datamodel-matchthefollowingquestion-editorstate"></a>

editorState of Question

```
{
    "options": {
        "left": [
            {
                "value": {
                    "body": "<p>Red</p>",
                    "value": 0
                }
            },
            {
                "value": {
                    "body": "<p>Yellow</p>",
                    "value": 1
                }
            },
            {
                "value": {
                    "body": "<p>Green</p>",
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
        "right": [
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
        ]
    },
    "question": "<p>Match the colour with the fruits.</p>",
    "solutions": [
        {
            "id": "3fe0e600-9746-4673-81a9-3429af3fef41",
            "type": "html",
            "value": "<figure class=\"table\"><table><tbody><tr><td>Red</td><td>Apple</td></tr><tr><td>Yellow</td><td>Banana</td></tr><tr><td>Green</td><td>Grapes</td></tr><tr><td>Orange</td><td>Orange</td></tr></tbody></table></figure><p>In the solution we can use the feature of ckeditor so we can also add table as above. using table menu.<br>We can add solution as text + image / Video / Audi (Yet to come)</p>"
        }
    ]
}
```

editorState Stores editor specific data.

#### templateId <a href="#id-datamodel-matchthefollowingquestion-templateid" id="id-datamodel-matchthefollowingquestion-templateid"></a>

```
"templateId": "mtf-horizontal" / "mtf-vertical"
```

#### primaryCategory <a href="#id-datamodel-matchthefollowingquestion-primarycategory" id="id-datamodel-matchthefollowingquestion-primarycategory"></a>

```
"primaryCategory": "Match The Following Question"
```

#### qType <a href="#id-datamodel-matchthefollowingquestion-qtype" id="id-datamodel-matchthefollowingquestion-qtype"></a>

```
"qType": "MTF"
```

#### interactionTypes <a href="#id-datamodel-matchthefollowingquestion-interactiontypes" id="id-datamodel-matchthefollowingquestion-interactiontypes"></a>

```
"interactionTypes": ["match"]
```

***

#### Let’s Compare MTF with MCQ data <a href="#id-datamodel-matchthefollowingquestion-letscomparemtfwithmcqdata" id="id-datamodel-matchthefollowingquestion-letscomparemtfwithmcqdata"></a>

**Compare MCQ body with MTF body**

MCQ body vs MTF body

| **MCQ Body**                                                                                                                                                                                                                                                                                        | **MTF Body**                                                                                                                                                                                                                                                                                     |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <pre><code>&#x3C;div class='question-body' tabindex='-1'>
    &#x3C;div class='mcq-title' tabindex='0'>
        &#x3C;p>Which of the fruits is red in colour?&#x3C;/p>
    &#x3C;/div>
    &#x3C;div data-choice-interaction='response1' class='mcq-vertical'>&#x3C;/div>
&#x3C;/div>
</code></pre> | <pre><code>&#x3C;div class='question-body' tabindex='-1'>
    &#x3C;div class='mtf-title' tabindex='0'>
        &#x3C;p>Match the colour with the fruits.&#x3C;/p>
    &#x3C;/div>
    &#x3C;div data-match-interaction='response1' class='mtf-horizontal'>&#x3C;/div>
&#x3C;/div>
</code></pre> |

**Compare MCQ interactions with MTF interactions**

MCQ interactions vs MTF interactions

| **MCQ interaction**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | **MTF interaction**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>{
    "response1": {
        "type": "choice",
        "options": [
            {
                "label": "&#x3C;p>Apple&#x3C;/p>",
                "value": 0,
                "hint": ""
            },
            {
                "label": "&#x3C;p>Banana&#x3C;/p>",
                "value": 1,
                "hint": ""
            },
            {
                "label": "&#x3C;p>Grapes&#x3C;/p>",
                "value": 2,
                "hint": ""
            },
            {
                "label": "&#x3C;p>Orange&#x3C;/p>",
                "value": 3,
                "hint": ""
            }
        ],
        "validation": {
            "required": "Yes"
        }
    }
}
</code></pre> | <pre><code>{
    "response1": {
        "type": "match",
        "options": {
            "left": [
                {
                    "label": "&#x3C;p>Red&#x3C;/p>",
                    "value": 0
                },
                {
                    "label": "&#x3C;p>Yellow&#x3C;/p>",
                    "value": 1
                },
                {
                    "label": "&#x3C;p>Green&#x3C;/p>",
                    "value": 2
                },
                {
                    "label": "&#x3C;p>Orange&#x3C;/p>",
                    "value": 3
                }
            ],
            "right": [
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
            ]
        },
        "validation": {
            "required": "Yes"
        }
    }
}
</code></pre> |

**Compare MCQ responseDeclaration with MTF responseDeclaration**

MCQ responseDeclaration vs MTF responseDeclaration

| **MCQ responseDeclaration**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | **MTF responseDeclaration**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>{
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
}
</code></pre><pre><code>//MMCQ
{
        "response1": {
            "cardinality": "multiple",
            "type": "integer",
            "correctResponse": {
                "value": [
                    0,
                    3
                ]
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
    }
</code></pre> | <pre><code>{
        "response1": {
            "cardinality": "multiple",
            "type": "map",
            "correctResponse": {
                "value": [
                    {
                        "0": 0
                    },
                    {
                        "1": 1
                    },
                    {
                        "2": 2
                    },
                    {
                        "3": 3
                    }
                ]
            },
            "mapping": [
                {
                    "value": {
                        "0": 0
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "1": 1
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "2": 2
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "3": 3
                    },
                    "score": 0.25
                }
            ]
        }
    }
</code></pre> |

**Compare MCQ outcomeDeclaration with MTF outcomeDeclaration**

MCQ outcomeDeclaration vs MTF outcomeDeclaration

| MCQ outcomeDeclaration                                                                                                                                               | MTF outcomeDeclaration                                                                                                                                               |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>{
        "maxScore": {
            "cardinality": "multiple",
            "type": "integer",
            "defaultValue": 1
        }
    }
</code></pre> | <pre><code>{
        "maxScore": {
            "cardinality": "multiple",
            "type": "integer",
            "defaultValue": 1
        }
    }
</code></pre> |

**Compare MCQ editorState with MTF editorState**

MCQ editorState vs MTF editorState

| MCQ editorState                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | MTF editorState                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <pre><code>{
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
    }
</code></pre> | <pre><code>
</code></pre><pre><code>{
    "options": {
        "left": [
            {
                "value": {
                    "body": "&#x3C;p>Red&#x3C;/p>",
                    "value": 0
                }
            },
            {
                "value": {
                    "body": "&#x3C;p>Yellow&#x3C;/p>",
                    "value": 1
                }
            },
            {
                "value": {
                    "body": "&#x3C;p>Green&#x3C;/p>",
                    "value": 2
                }
            },
            {
                "value": {
                    "body": "&#x3C;p>Orange&#x3C;/p>",
                    "value": 3
                }
            }
        ],
        "right": [
            {
                "value": {
                    "body": "&#x3C;p>Apple&#x3C;/p>",
                    "value": 0
                }
            },
            {
                "value": {
                    "body": "&#x3C;p>Banana&#x3C;/p>",
                    "value": 1
                }
            },
            {
                "value": {
                    "body": "&#x3C;p>Grapes&#x3C;/p>",
                    "value": 2
                }
            },
            {
                "value": {
                    "body": "&#x3C;p>Orange&#x3C;/p>",
                    "value": 3
                }
            }
        ]
    },
    "question": "&#x3C;p>Match the colour with the fruits.&#x3C;/p>",
    "solutions": [
        {
            "id": "3fe0e600-9746-4673-81a9-3429af3fef41",
            "type": "html",
            "value": "&#x3C;figure class=\"table\">&#x3C;table>&#x3C;tbody>&#x3C;tr>&#x3C;td>Red&#x3C;/td>&#x3C;td>Apple&#x3C;/td>&#x3C;/tr>&#x3C;tr>&#x3C;td>Yellow&#x3C;/td>&#x3C;td>Banana&#x3C;/td>&#x3C;/tr>&#x3C;tr>&#x3C;td>Green&#x3C;/td>&#x3C;td>Grapes&#x3C;/td>&#x3C;/tr>&#x3C;tr>&#x3C;td>Orange&#x3C;/td>&#x3C;td>Orange&#x3C;/td>&#x3C;/tr>&#x3C;/tbody>&#x3C;/table>&#x3C;/figure>&#x3C;p>In the solution we can use the feature of ckeditor so we can also add table as above. using table menu.&#x3C;br>We can add solution as text + image / Video / Audi (Yet to come)&#x3C;/p>"
        }
    ]
}
</code></pre> |



***

**Complete MTF Question Metadata Example:**

MTF question metadata

```
{
    "mimeType": "application/vnd.sunbird.question",
    "media": [],
    "editorState": {
        "options": {
            "left": [
                {
                    "value": {
                        "body": "<p>Red</p>",
                        "value": 0
                    }
                },
                {
                    "value": {
                        "body": "<p>Yellow</p>",
                        "value": 1
                    }
                },
                {
                    "value": {
                        "body": "<p>Green</p>",
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
            "right": [
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
            ]
        },
        "question": "<p>Match the colour with the fruits.</p>",
        "solutions": [
            {
                "id": "3fe0e600-9746-4673-81a9-3429af3fef41",
                "type": "html",
                "value": "<figure class=\"table\"><table><tbody><tr><td>Red</td><td>Apple</td></tr><tr><td>Yellow</td><td>Banana</td></tr><tr><td>Green</td><td>Grapes</td></tr><tr><td>Orange</td><td>Orange</td></tr></tbody></table></figure><p>In the solution we can use the feature of ckeditor so we can also add table as above. using table menu.<br>We can add solution as text + image / Video / Audi (Yet to come)</p>"
            }
        ]
    },
    "templateId": "mtf-horizontal",
    "complexityLevel": [],
    "maxScore": 1,
    "name": "MTF",
    "responseDeclaration": {
        "response1": {
            "cardinality": "multiple",
            "type": "map",
            "correctResponse": {
                "value": [
                    {
                        "0": 0
                    },
                    {
                        "1": 1
                    },
                    {
                        "2": 2
                    },
                    {
                        "3": 3
                    }
                ]
            },
            "mapping": [
                {
                    "value": {
                        "0": 0
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "1": 1
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "2": 2
                    },
                    "score": 0.25
                },
                {
                    "value": {
                        "3": 3
                    },
                    "score": 0.25
                }
            ]
        }
    },
    "outcomeDeclaration": {
        "maxScore": {
            "cardinality": "multiple",
            "type": "integer",
            "defaultValue": 1
        },
        "hint": {
            "cardinality": "single",
            "type": "string",
            "defaultValue": "098eacc6-07fd-45ba-9e3c-372042154cd3"
        }
    },
    "interactionTypes": [
        "match"
    ],
    "interactions": {
        "response1": {
            "type": "match",
            "options": {
                "left": [
                    {
                        "label": "<p>Red</p>",
                        "value": 0
                    },
                    {
                        "label": "<p>Yellow</p>",
                        "value": 1
                    },
                    {
                        "label": "<p>Green</p>",
                        "value": 2
                    },
                    {
                        "label": "<p>Orange</p>",
                        "value": 3
                    }
                ],
                "right": [
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
                ]
            },
            "validation": {
                "required": "Yes"
            }
        }
    },
    "qType": "MTF",
    "primaryCategory": "Match The Following Question",
    "solutions": {
        "3fe0e600-9746-4673-81a9-3429af3fef41": "<figure class=\"table\"><table><tbody><tr><td>Red</td><td>Apple</td></tr><tr><td>Yellow</td><td>Banana</td></tr><tr><td>Green</td><td>Grapes</td></tr><tr><td>Orange</td><td>Orange</td></tr></tbody></table></figure><p>In the solution we can use the feature of ckeditor so we can also add table as above. using table menu.<br>We can add solution as text + image / Video / Audi (Yet to come)</p>"
    },
    "body": "<div class='question-body' tabindex='-1'><div class='mtf-title' tabindex='0'><p>Match the colour with the fruits.</p></div><div data-match-interaction='response1' class='mtf-horizontal'></div></div>",
    "answer": "<div class='match-container'><div class='left-options'><div class='left-option'><p>Red</p></div><div class='left-option'><p>Yellow</p></div><div class='left-option'><p>Green</p></div><div class='left-option'><p>Orange</p></div></div><div class='right-options'><div class='right-option'><p>Apple</p></div><div class='right-option'><p>Banana</p></div><div class='right-option'><p>Grapes</p></div><div class='right-option'><p>Orange</p></div></div></div>",
    "createdBy": "5a587cc1-e018-4859-a0a8-e842650b9d64",
    "board": "CBSE",
    "medium": [
        "English"
    ],
    "gradeLevel": [
        "Class 4"
    ],
    "subject": [
        "Hindi"
    ],
    "author": "Test User",
    "channel": "01309282781705830427",
    "framework": "inquiry_k-12",
    "copyright": "NIT123",
    "audience": [
        "Student"
    ],
    "license": "CC BY 4.0"
}
```
