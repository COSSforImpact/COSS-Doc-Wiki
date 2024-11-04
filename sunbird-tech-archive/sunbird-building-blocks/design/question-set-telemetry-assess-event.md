---
icon: elementor
---

# Question-set telemetry ASSESS event

This document details about telemetry assess event structure for the different type of questions(like MCA, MTF, FTB, Sequence, Reorder etc..)

### Question Types <a href="#question-settelemetryassessevent-questiontypes" id="question-settelemetryassessevent-questiontypes"></a>

Find the below list of question types and its sample telemetry ASSESS event data.

### **1. MCQ Question Type** <a href="#question-settelemetryassessevent-1.mcqquestiontype" id="question-settelemetryassessevent-1.mcqquestiontype"></a>

The question of type MCQ will have multiple options to select for the right answer/option. These options will get shuffle(different order) when the content played by different users.

Telemetry Assess Event Expand source

```
{
  "eid": "ASSESS",
  "ets": 1549363253158,
  "ver": "3.0",
  "mid": "ASSESS:05832f80e6cca664e9e4a17d7c4ce5f9",
  "actor": {
    "id": "95e4942d-cbe8-477d-aebd-ad8e6de4bfc8",
    "type": "User"
  },
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.14.0",
      "pid": "sunbird-portal.contenteditor.contentplayer"
    },
    "env": "contentplayer",
    "sid": "yD79BBAExQCP3nZmR2Q9rO1jl8hDho0X",
    "did": "51a59362a5d4be51d9f83552f0b8c3e0",
    "cdata": [
      {
        "id": "8c12bdb10e98842175a3638660814c10",
        "type": "ContentSession"
      }
    ],
    "rollup": {}
  },
  "object": {
    "id": "do_112692350547279872110",
    "type": "Content",
    "ver": "1.0"
  },
  "tags": [],
  "edata": {
    "item": {
      "id": "044d8b91-42a1-4396-97a6-6b3d272d5ab9",
      "maxscore": 1,
      "exlength": 0,
      "params": [],
      "uri": "",
      "title": "सौरमंडल में कितने ग्रह हैं?",
      "mmc": [],
      "mc": [],
      "desc": "Solar system"
    },
    "index": 4,
    "pass": "Yes",
    "score": 1,
    "resvalues": [
      {
        "option0": "<p>आठ</p>\n"
      }
    ],
    "duration": 78
  }
}
```

\\

**Interpretation of Data:**

* edata.pass => User/Student is result after attempting the question (Yes/No)
* edata.index => Position/Order of the question in the question-set
* edata.score => User/Student score after attempting the question(For the questions which has partial answer enabled, edata.score will be < edata.item.maxscore if user/student answered partially).
* edata.resvalues => user selected option/answer of the question

edata.resvalues is an array of objects/maps \[ {}, {}, ..].

Each object/map will have only one key & value pair. With reference to the above in resvalues, "option0"(option{option index position}) is key & "\<p>आठ\</p>\n"(HTML Text) is value.

### **2. FTB Question Type** <a href="#question-settelemetryassessevent-2.ftbquestiontype" id="question-settelemetryassessevent-2.ftbquestiontype"></a>

The question of type FTB may have single/multiple blanks in the question. The user can answer using default mobile or custom keyboard depends on configuration set while creating the question.

Telemetry Assess Event Expand source

```
{
  "eid": "ASSESS",
  "ets": 1549363076856,
  "ver": "3.0",
  "mid": "ASSESS:4ce0f7193337f5fd8bacfe72823c766d",
  "actor": {
    "id": "95e4942d-cbe8-477d-aebd-ad8e6de4bfc8",
    "type": "User"
  },
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.14.0",
      "pid": "sunbird-portal.contenteditor.contentplayer"
    },
    "env": "contentplayer",
    "sid": "yD79BBAExQCP3nZmR2Q9rO1jl8hDho0X",
    "did": "51a59362a5d4be51d9f83552f0b8c3e0",
    "cdata": [
      {
        "id": "8c12bdb10e98842175a3638660814c10",
        "type": "ContentSession"
      }
    ],
    "rollup": {}
  },
  "object": {
    "id": "do_112692350547279872110",
    "type": "Content",
    "ver": "1.0"
  },
  "tags": [],
  "edata": {
    "item": {
      "id": "824732d3-78e1-4c89-a14c-5a7ea78eeb91",
      "maxscore": 2,
      "exlength": 0,
      "params": [],
      "uri": "",
      "title": "Solar system related questions",
      "mmc": [],
      "mc": [],
      "desc": ""
    },
    "index": 3,
    "pass": "Yes",
    "score": 2,
    "resvalues": [
      {
        "key": "JUPITER"
      },
      {
        "key": "Mercury"
      }
    ],
    "duration": 290
  }
}
```

\\

**Interpretation of Data :**

* edata.pass => User/Student is result after attempting the question (Yes/No)
* edata.index => Position/Order of the question in the question-set
* edata.score => User/Student score after attempting the question(For the questions which has partial answer enabled, edata.score will be < edata.item.maxscore if user/student answered partially).
* edata.resvalues => user entered answers using keyboard(native/custom)

edata.resvalues is an array of objects/maps \[ {}, {}, ..].

With reference to the above example in resvalues, "key"(common name used for all options) is key & "JUPITER" or "Mercury" is values entered by the User/Student.

\\

### **3. MTF Question Type** <a href="#question-settelemetryassessevent-3.mtfquestiontype" id="question-settelemetryassessevent-3.mtfquestiontype"></a>

The question of type MTF, will have LHS(left had side) & rhs(right had side) options. User/Student can drag & drop only RHS options to map to the respective LHS option.

Telemetry Assess Event Expand source

```
{
  "eid": "ASSESS",
  "ets": 1549359563577,
  "ver": "3.0",
  "mid": "ASSESS:9a5b2c8b2a41bbc25e12980b14161992",
  "actor": {
    "id": "95e4942d-cbe8-477d-aebd-ad8e6de4bfc8",
    "type": "User"
  },
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.14.0",
      "pid": "sunbird-portal.contenteditor.contentplayer"
    },
    "env": "contentplayer",
    "sid": "yD79BBAExQCP3nZmR2Q9rO1jl8hDho0X",
    "did": "51a59362a5d4be51d9f83552f0b8c3e0",
    "cdata": [
      {
        "id": "5d8807e749795a3712227f1d3d3c5daf",
        "type": "ContentSession"
      }
    ],
    "rollup": {}
  },
  "object": {
    "id": "do_112692350547279872110",
    "type": "Content",
    "ver": "1.0"
  },
  "tags": [],
  "edata": {
    "item": {
      "id": "c943d0a907274471a0572e593eab49c2",
      "maxscore": 1,
      "exlength": 0,
      "params": [],
      "uri": "",
      "title": "question title",
      "mmc": [],
      "mc": [],
      "desc": "question description"
    },
    "index": 1,
    "pass": "Yes",
    "score": 1,
    "resvalues": [
      {
        "LHS": [
          {
            "text": "",
            "image": "/assets/public/content/do_1122174111934709761139/artifact/share_1491383202557.jpg",
            "audio": "",
            "audioName": "",
            "hint": "",
            "index": 1,
          }
        ],
        "RHS": [
          {
            "text": "",
            "image": "/assets/public/content/1465367844162rabbit.png",
            "audio": "",
            "audioName": "",
            "hint": "",
            "mapIndex": 2
          }
        ]
      },
      {
        "LHS": [
          {
            "text": "Rabbit",
            "image": "",
            "audio": "",
            "audioName": "",
            "hint": "",
            "index": 2,
          }
        ],
        "RHS": [
          {
            "text": "",
            "image": "/assets/public/content/1465347630227fish.png",
            "audio": "/assets/public/content/1464861648182fish.mp3",
            "audioName": "",
            "hint": "",
            "mapIndex": 3
          }
        ]
      },
      {
        "LHS": [
          {
            "text": "Fish",
            "image": "",
            "audio": "",
            "audioName": "domain_58489_fish_audio",
            "hint": "",
            "index": 3,
          }
        ],
        "RHS": [
          {
            "text": "Lion",
            "image": "",
            "audio": "",
            "audioName": "",
            "hint": "",
            "mapIndex": 1
          }
        ]
      }
    ],
    "duration": 39
  }
}
```

\\

**Interpretation of Data :**

* edata.pass => User/Student is result after attempting the question (Yes/No)
* edata.index => Position/Order of the question in the question-set
* edata.score => User/Student score after attempting the question(For the questions which has partial answer enabled, edata.score will be < edata.item.maxscore if user/student answered partially).
* edata.resvalues => final reordered LHS & RHS options

edata.resvalues is an array of objects\[ {}, {}, ..].

The object structure inside resvalues is complex. This can be simplified(TBD).

With reference to the above example in resvalues, each object will have LHS & RHS array({ "LHS": \[], "RHS": \[] }).

LHS array has object structure.

{ "text": "Lion", "image": "", "audio": "", "audioName": "", "hint": "", **"index": 1** }

**"index": 1** => The position/index of the option in the LHS options array(rendered position)

\\

RHS array has below object stucture

{ "text": "", "image": "/assets/public/content/1465367844162rabbit.png", "audio": "", "audioName": "", "hint": "", **"mapIndex": 2** }

**"mapIndex": 2** => This option which is rendered in the first position(RHS side) is drag & drop(mapped) to 2 option of the LHS

\\

### **4. Sequence Question Type** <a href="#question-settelemetryassessevent-4.sequencequestiontype" id="question-settelemetryassessevent-4.sequencequestiontype"></a>

The question of type Sequence, will have a list of options. User/Student has to arrange(by drag & drop) the options in the proper/right order. For every drag & drop of the option, the RESPONSE event will trigger.

Telemetry Assess Event Expand source

```
{
  "eid": "ASSESS",
  "ets": 1549362785346,
  "ver": "3.0",
  "mid": "ASSESS:34b9203a6cc4378fc4e6cb6bb70fa2ea",
  "actor": {
    "id": "95e4942d-cbe8-477d-aebd-ad8e6de4bfc8",
    "type": "User"
  },
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.14.0",
      "pid": "sunbird-portal.contenteditor.contentplayer"
    },
    "env": "contentplayer",
    "sid": "yD79BBAExQCP3nZmR2Q9rO1jl8hDho0X",
    "did": "51a59362a5d4be51d9f83552f0b8c3e0",
    "cdata": [
      {
        "id": "8c12bdb10e98842175a3638660814c10",
        "type": "ContentSession"
      }
    ],
    "rollup": {}
  },
  "object": {
    "id": "do_112692350547279872110",
    "type": "Content",
    "ver": "1.0"
  },
  "tags": [],
  "edata": {
    "item": {
      "id": "7272c492-4d67-4ad4-837c-b2d9a6345335",
      "maxscore": 1,
      "exlength": 0,
      "params": [],
      "uri": "",
      "title": "Order of the planets in the solar system(Order starts from closest to sun)",
      "mmc": [],
      "mc": [],
      "desc": ""
    },
    "index": 2,
    "pass": "Yes",
    "score": 1,
    "resvalues": [
      {
        "SEQ": [
          {
            "text": "Venus",
            "image": "",
            "audio": "",
            "audioName": "",
            "hint": "",
            "sequenceOrder": 2
          }
        ]
      },
      {
        "SEQ": [
          {
            "text": "Mars",
            "image": "",
            "audio": "",
            "audioName": "",
            "hint": "",
            "sequenceOrder": 4
          }
        ]
      },
      {
        "SEQ": [
          {
            "text": "Earth",
            "image": "",
            "audio": "",
            "audioName": "",
            "hint": "",
            "sequenceOrder": 3
          }
        ]
      },
      {
        "SEQ": [
          {
            "text": "Mercury",
            "image": "",
            "audio": "",
            "audioName": "",
            "hint": "",
            "sequenceOrder": 1
          }
        ]
      }
    ],
    "duration": 262
  }
}
```

\\

**Interpretation of Data :**

* edata.pass => User/Student is result after attempting the question (Yes/No)
* edata.index => Position/Order of the question in the question-set
* edata.score => User/Student score after attempting the question(For the questions which has partial answer enabled, edata.score will be < edata.item.maxscore if user/student answered partially).
* edata.resvalues => Order of the options while evaluation

edata.resvalues is an array of objects\[ {}, {}, ..].

\\

### **5. ReOrder Question Type** <a href="#question-settelemetryassessevent-5.reorderquestiontype" id="question-settelemetryassessevent-5.reorderquestiontype"></a>

The question of type reorder

Telemetry Assess Event

```
{
  "eid": "ASSESS",
  "ets": 1549362273576,
  "ver": "3.0",
  "mid": "ASSESS:ef81a0500263337ef870790714b84097",
  "actor": {
    "id": "95e4942d-cbe8-477d-aebd-ad8e6de4bfc8",
    "type": "User"
  },
  "context": {
    "channel": "b00bc992ef25f1a9a8d63291e20efc8d",
    "pdata": {
      "id": "dev.sunbird.portal",
      "ver": "1.14.0",
      "pid": "sunbird-portal.contenteditor.contentplayer"
    },
    "env": "contentplayer",
    "sid": "yD79BBAExQCP3nZmR2Q9rO1jl8hDho0X",
    "did": "51a59362a5d4be51d9f83552f0b8c3e0",
    "cdata": [
      {
        "id": "8c12bdb10e98842175a3638660814c10",
        "type": "ContentSession"
      }
    ],
    "rollup": {}
  },
  "object": {
    "id": "do_112692350547279872110",
    "type": "Content",
    "ver": "1.0"
  },
  "tags": [],
  "edata": {
    "item": {
      "id": "c4be86dd-181d-49ee-9577-924ab6b4ab49",
      "maxscore": 1,
      "exlength": 0,
      "params": [],
      "uri": "",
      "title": "VSV Reorder Form the sentance using below words",
      "mmc": [],
      "mc": [],
      "desc": ""
    },
    "index": 1,
    "pass": "Yes",
    "score": 1,
    "resvalues": ["what", "are", "you", "looking", "for", "?"],
    "duration": 14
  }
}
```

\\

**Interpretation of Data :**

To Be Updated(TBU)\


\\

### Related articles <a href="#question-settelemetryassessevent-relatedarticles" id="question-settelemetryassessevent-relatedarticles"></a>

* Page:Discussion Forum: Telemetry Events
* Page:Certificate: Dynamic rules support
* Page:Changes to course progress calculation for videos/youtube and pdf content
* Page:Request traceability across multiple sub-systems
* Page:User onboarding for crowdsourcing

\\

\\
