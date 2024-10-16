---
icon: elementor
---

# Challenges in QuML Spec and UI Design

### Introduction <a href="#challengesinqumlspecanduidesign-introduction" id="challengesinqumlspecanduidesign-introduction"></a>

There are some challenges which we face currently with the QuML Spec. Existing spec restricts how the Question will look in UI and lots of CSS is needed to manage the look and feel.

#### How Questions with Plain Text Get Stored in DB <a href="#challengesinqumlspecanduidesign-howquestionswithplaintextgetstoredindb" id="challengesinqumlspecanduidesign-howquestionswithplaintextgetstoredindb"></a>

If we want to add a question with simple text: **What is the Capital of India?**

It gets stored as:

```
<div class='question-body' tabindex='-1'>
    <div class='mcq-title' tabindex='0'>
        <p>What is the Capital of India?&nbsp;</p>
    </div>
    <div data-choice-interaction='response1' class='mcq-vertical'></div>
</div>
```

#### How Questions with Images Get Stored in DB <a href="#challengesinqumlspecanduidesign-howquestionswithimagesgetstoredindb" id="challengesinqumlspecanduidesign-howquestionswithimagesgetstoredindb"></a>

If we want to add a question with simple text + image: **What is the Capital of India? + IndiaGate.jpg**

It gets stored as:

```
<div class='question-body' tabindex='-1'>
    <div class='mcq-title' tabindex='0'>
        <p>What is the Capital of India?&nbsp;</p>
        <figure class="image"><img src="/assets/public/content/assets/do_21408871175179468812/indiagate.jpeg"
                alt="indiaGate" data-asset-variable="do_21408871175179468812"></figure>
    </div>
    <div data-choice-interaction='response1' class='mcq-vertical'></div>
</div>
```

Since the data in the database gets stored in the form of HTML markup, it creates a problem in UI handling images of different sizes and resolutions.

#### Storing Images in Options <a href="#challengesinqumlspecanduidesign-storingimagesinoptions" id="challengesinqumlspecanduidesign-storingimagesinoptions"></a>

Similar to questions, the images in options get stored in the form of HTML markup as:

**Option 1 - New Delhi + indiaGate.jpg** It gets stored as:

```
<p>New Delhi</p>
<figure class="image">
    <img src="/assets/public/content/assets/do_21408871212497305613/indiagate.jpeg" alt="indiaGate"
    data-asset-variable="do_21408871212497305613">
</figure>
```

**Option 2 - Mumbai + gateway-of-india.jpg** It gets stored as:

```
<p>Mumbai&nbsp;</p>
<figure class="image resize-25">
    <img src="/assets/public/content/assets/do_21408871227163443214/gateway-of-india.jpg" alt="gateway-of-india"
    data-asset-variable="do_21408871227163443214">
</figure>
```

MCQ metadata example:

MCQ Data

```
{
    "copyright": "tn",
    "code": "16752658-58f4-4c9a-be39-e7441aeba8ac",
    "subject": [
        "English"
    ],
    "qumlVersion": 1.1,
    "channel": "01269878797503692810",
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
    "language": [
        "English"
    ],
    "medium": [
        "English"
    ],
    "mimeType": "application/vnd.sunbird.question",
    "showHints": false,
    "media": [
        {
            "id": "do_21408871175179468812",
            "type": "image",
            "src": "/assets/public/content/assets/do_21408871175179468812/indiagate.jpeg",
            "baseUrl": "https://staging.sunbirded.org"
        },
        {
            "id": "do_21408871212497305613",
            "type": "image",
            "src": "/assets/public/content/assets/do_21408871212497305613/indiagate.jpeg",
            "baseUrl": "https://staging.sunbirded.org"
        },
        {
            "id": "do_21408871227163443214",
            "type": "image",
            "src": "/assets/public/content/assets/do_21408871227163443214/gateway-of-india.jpg",
            "baseUrl": "https://staging.sunbirded.org"
        }
    ],
    "body": "<div class='question-body' tabindex='-1'><div class='mcq-title' tabindex='0'><p>What is the Capital of India?&nbsp;</p><figure class=\"image\"><img src=\"/assets/public/content/assets/do_21408871175179468812/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_21408871175179468812\"></figure></div><div data-choice-interaction='response1' class='mcq-vertical'></div></div>",
    "editorState": {
        "options": [
            {
                "answer": true,
                "value": {
                    "body": "<p>New Delhi</p><figure class=\"image\"><img src=\"/assets/public/content/assets/do_21408871212497305613/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_21408871212497305613\"></figure>",
                    "value": 0
                }
            },
            {
                "answer": false,
                "value": {
                    "body": "<p>Mumbai&nbsp;</p><figure class=\"image resize-25\"><img src=\"/assets/public/content/assets/do_21408871227163443214/gateway-of-india.jpg\" alt=\"gateway-of-india\" data-asset-variable=\"do_21408871227163443214\"></figure>",
                    "value": 1
                }
            }
        ],
        "question": "<p>What is the Capital of India?&nbsp;</p><figure class=\"image\"><img src=\"/assets/public/content/assets/do_21408871175179468812/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_21408871175179468812\"></figure>"
    },
    "templateId": "mcq-vertical",
    "createdOn": "2024-07-01T05:59:45.514+0000",
    "objectType": "Question",
    "interactions": {
        "response1": {
            "type": "choice",
            "options": [
                {
                    "label": "<p>New Delhi</p><figure class=\"image\"><img src=\"/assets/public/content/assets/do_21408871212497305613/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_21408871212497305613\"></figure>",
                    "value": 0,
                    "hint": ""
                },
                {
                    "label": "<p>Mumbai&nbsp;</p><figure class=\"image resize-25\"><img src=\"/assets/public/content/assets/do_21408871227163443214/gateway-of-india.jpg\" alt=\"gateway-of-india\" data-asset-variable=\"do_21408871227163443214\"></figure>",
                    "value": 1,
                    "hint": ""
                }
            ],
            "validation": {
                "required": "Yes"
            }
        }
    },
    "gradeLevel": [
        "Class 5"
    ],
    "primaryCategory": "Multiple Choice Question",
    "contentDisposition": "inline",
    "lastUpdatedOn": "2024-07-01T05:59:45.671+0000",
    "contentEncoding": "gzip",
    "showSolutions": false,
    "allowAnonymousAccess": "Yes",
    "identifier": "do_21408871289253068814",
    "lastStatusChangedOn": "2024-07-01T05:59:45.514+0000",
    "audience": [
        "Student"
    ],
    "schemaVersion": "1.1",
    "visibility": "Parent",
    "showTimer": false,
    "author": "Guest new name",
    "solutions": {},
    "hints": {},
    "outcomeDeclaration": {
        "maxScore": {
            "cardinality": "single",
            "type": "integer",
            "defaultValue": 1
        },
        "hint": {
            "cardinality": "single",
            "type": "string",
            "defaultValue": "d97eab22-93bb-4044-aa15-7def03d549a5"
        }
    },
    "qType": "MCQ",
    "maxScore": 1,
    "languageCode": [
        "en"
    ],
    "versionKey": "1719813585671",
    "showFeedback": false,
    "license": "CC BY 4.0",
    "interactionTypes": [
        "choice"
    ],
    "framework": "tn_k-12_5",
    "answer": "<div class='answer-container'><div class='answer-body'><p>New Delhi</p><figure class=\"image\"><img src=\"/assets/public/content/assets/do_21408871212497305613/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_21408871212497305613\"></figure></div></div>",
    "createdBy": "fca2925f-1eee-4654-9177-fece3fd6afc9",
    "compatibilityLevel": 5,
    "name": "MCQ",
    "board": "State (Tamil Nadu)",
    "status": "Draft"
}
```

Editor UI

Questionset Editor



Player UI

QuML Player

QuML-MCQ.mp4

To address the challenges there are few proposed format in which we can store the question and options

**Format 1:**

Example JSON:

```
{
    "question": {
        "text": "<p>2*5 = ?</p>",
        "image": "/assets/image.png",
        "audio": "/assets/audio.mp3",
        "audioName": "audio file",
        "hint": ""
    },
    "options": [
        {
            "text": "<p>5</p>",
            "image": "",
            "audio": "",
            "audioName": "",
            "hint": "",
            "isCorrect": false
        },
        {
            "text": "<p>10</p>",
            "image": "",
            "audio": "",
            "audioName": "",
            "hint": "",
            "isCorrect": true
        }
    ]
}
```

Pros:

* **Simplicity:** Each content type is stored in dedicated fields, ensuring straightforward data management.
* **Readability:** Clear field names make parsing and understanding easy.
* **Efficiency:** Direct access to content without needing to iterate through arrays.

Cons:

* **Scalability:** Adding new content types requires modifying the schema and related code.
* **Redundancy:** Options include all fields, potentially leading to empty or redundant data.
* **Flexibility:** Limited in handling multiple instances of the same content type efficiently.

**Format 2:**

Example JSON:

```
{
    "question": {
        "content": [
            {
                "type": "text",
                "value": "<p>2*5 is ?</p>"
            },
            {
                "type": "image",
                "src": "/assets/image.png",
                "alt": "Image"
            },
            {
                "type": "audio",
                "src": "/assets/audio.mp3",
                "name": "audio file"
            },
            {
                "type": "hint",
                "value": ""
            }
        ]
    },
    "options": [
        {
            "id": "option1",
            "content": [
                {
                    "type": "text",
                    "value": "<p>5</p>"
                },
                {
                    "type": "image",
                    "src": "",
                    "alt": ""
                },
                {
                    "type": "audio",
                    "src": "",
                    "name": ""
                },
                {
                    "type": "hint",
                    "value": ""
                }
            ],
            "isCorrect": false
        },
        {
            "id": "option2",
            "content": [
                {
                    "type": "text",
                    "value": "<p>10</p>"
                },
                {
                    "type": "image",
                    "src": "",
                    "alt": ""
                },
                {
                    "type": "audio",
                    "src": "",
                    "name": ""
                },
                {
                    "type": "hint",
                    "value": ""
                }
            ],
            "isCorrect": true
        }
    ]
}
```

Pros:

* **Flexibility:** Supports multiple instances of the same content type with an array-based structure.
* **Scalability:** Easily accommodates new content types by adding objects to the content array.
* **Consistency:** All content types are handled uniformly, aiding in processing and rendering.

Cons:

* **Complexity:** Requires iterating over arrays to process different content types, adding parsing overhead.
* **Readability:** Nested structure and type-checking can reduce immediate readability.

**Format 3 (Recommended):**

Example JSON:

```
{
    "question": {
        "id": "q1",
        "text": "What is the Capital of India?",
        "media": [
            {
                "type": "image",
                "src": "/assets/indiagate.jpeg",
                "alt": "India Gate"
            },
            {
                "type": "audio",
                "src": "/assets/question-audio.mp3",
                "alt": "Question Audio"
            },
            {
                "type": "video",
                "src": "/assets/question-video.mp4",
                "alt": "Question Video"
            }
        ]
    },
    "options": [
        {
            "id": "option1",
            "text": "New Delhi",
            "media": [
                {
                    "type": "image",
                    "src": "/assets/indiagate.jpeg",
                    "alt": "India Gate"
                }
            ]
        },
        {
            "id": "option2",
            "text": "Mumbai",
            "media": [
                {
                    "type": "image",
                    "src": "/assets/gateway-of-india.jpg",
                    "alt": "Gateway of India"
                }
            ]
        }
    ]
}
```

Pros:

* **Simplicity:** Clearly separates text and media, enhancing clarity and ease of handling.
* **Readability:** Explicit fields for text and media improve understanding.
* **Flexibility:** Supports various content types within a structured format.

Cons:

* **Scalability:** Introducing new content types may necessitate schema and code adjustments.
* **Redundancy:** Potential for empty fields depending on the question's media requirements.
* **Specificity:** Structured format may be less adaptable for multiple instances of the same content type.

**Summary:** Format 3 stands out as the preferred choice due to its balanced approach in terms of simplicity, readability, and flexibility. It efficiently manages different content types while maintaining a structured format suitable for question data storage and rendering.
