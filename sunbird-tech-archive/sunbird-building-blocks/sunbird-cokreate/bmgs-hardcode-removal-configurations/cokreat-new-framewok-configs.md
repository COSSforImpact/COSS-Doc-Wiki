---
icon: elementor
---

# coKreat New Framewok Configs

**Sourcing Portal:**

Filters:

1. Make a read call of

request: {context: "framework", context\_type: "filters", channel: "01269934121990553633", operation: "create"}

1. Copy the data drom result and add it on request and update

Form:

"data": {

"action": "create",

"properties": \[

{

"code": "board",

"name": "Board",

"label": "Framework",

"default": "",

"visible": **true**,

"dataType": "list",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "framework",

"placeholder": "Select framework",

"validations": \[

{

"type": "maxLength",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Title is required"

}

],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

}

},

{

"code": "farmingtype",

"name": "farmingtype",

"label": "Farming Type",

"default": "",

"visible": **true**,

"dataType": "list",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "farmingtype",

"placeholder": "Select farmingtype",

"validations": \[

{

"type": "maxLength",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Title is required"

}

],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

}

},

{

"code": "cropcategory",

"name": "cropcategory",

"label": "cropcategory",

"default": "",

"visible": **true**,

"dataType": "list",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "cropcategory",

"placeholder": "Select cropcategory",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "croptype",

"name": "croptype",

"label": "croptype",

"default": "",

"depends": "",

"visible": **true**,

"dataType": "list",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "",

"placeholder": "Select croptype",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

],

"templateName": "defaultTemplate"

}

To add content types and others:

Form:

* request: {context: "framework", context\_type: "filters", channel: "01269934121990553633", operation: "create"}
  * channel: "01269934121990553633"
  * context: "framework"
  * context\_type: "filters"
  * operation: "create"

Defects: Not added these in developer documentation

Data:

"data": {

"action": "create",

"properties": \[

{

"code": "content\_types",

"name": "Content Types",

"label": "Content Types",

"terms": \[

{

"code": "Course Assessment",

"name": "Course Assessment",

"index": 1,

"lable": "Content Types",

"status": "Live",

"category": "contentTypes",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "Exam Question",

"name": "Exam Question",

"index": 1,

"lable": "Content Types",

"status": "Live",

"category": "contentTypes",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "Explanation Content",

"name": "Explanation Content",

"index": 1,

"lable": "Content Types",

"status": "Live",

"category": "contentTypes",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "Learning Resource",

"name": "Learning Resource",

"index": 1,

"lable": "Content Types",

"status": "Live",

"category": "contentTypes",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "Teacher Resource",

"name": "Teacher Resource",

"index": 1,

"lable": "Content Types",

"status": "Live",

"category": "contentTypes",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "Practice Question Set",

"name": "Practice Question Set",

"index": 1,

"lable": "Content Types",

"status": "Live",

"category": "contentTypes",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "eTextbook",

"name": "eTextbook",

"index": 1,

"lable": "Content Types",

"status": "Live",

"category": "contentTypes",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

}

],

"default": "",

"visible": **true**,

"dataType": "list",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "Content Types",

"placeholder": "Select Content Types",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "content\_submission\_enddate",

"name": "Contribution Date",

"label": "Contributions",

"terms": \[

{

"code": "open",

"name": "open",

"index": 1,

"lable": "Contributions",

"status": "Live",

"category": "contributions",

"identifier": "agriculture\_frameeork\_select\_contributions",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "closed",

"name": "Closed",

"index": 1,

"lable": "Contributions",

"status": "Live",

"category": "contributions",

"identifier": "agriculture\_frameeork\_select\_contributions",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "any",

"name": "Any",

"index": 1,

"lable": "Contributions",

"status": "Live",

"category": "contributions",

"identifier": "agriculture\_frameeork\_select\_contributions",

"description": **null**,

"associations": \[],

"translations": **null**

}

],

"default": "",

"visible": **true**,

"dataType": "text",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "Contributions",

"placeholder": "Select Contributions",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "nomination\_enddate",

"name": "Nomination Date",

"label": "Nominations",

"terms": \[

{

"code": "open",

"name": "open",

"index": 1,

"lable": "nominations",

"status": "Live",

"category": "nominations",

"identifier": "agriculture\_frameeork\_select\_nominations",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "closed",

"name": "Closed",

"index": 1,

"lable": "nominations",

"status": "Live",

"category": "nominations",

"identifier": "agriculture\_frameeork\_select\_nominations",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "any",

"name": "Any",

"index": 1,

"lable": "nominations",

"status": "Live",

"category": "nominations",

"identifier": "agriculture\_frameeork\_select\_nominations",

"description": **null**,

"associations": \[],

"translations": **null**

}

],

"default": "",

"visible": **true**,

"dataType": "text",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "Nominations",

"placeholder": "Select Nominations",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "rootorg\_id",

"name": "Rootorg Id",

"label": "Rootorg Id",

"default": "",

"visible": **false**,

"dataType": "text",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "Rootorg Id",

"placeholder": "Select Rootorg Id",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "target\_collection\_category",

"name": "Target Collection Category",

"label": "Target Collection Category",

"terms": \[

{

"code": "Content Playlist",

"name": "Content Playlist",

"index": 1,

"lable": "Target Collection Category",

"status": "Live",

"category": "target\_collection\_category",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "Course",

"name": "Course",

"index": 1,

"lable": "Target Collection Category",

"status": "Live",

"category": "target\_collection\_category",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "Digital Textbook",

"name": "Digital Textbook",

"index": 1,

"lable": "Target Collection Category",

"status": "Live",

"category": "target\_collection\_category",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

},

{

"code": "Question paper",

"name": "Question paper",

"index": 1,

"lable": "Target Collection Category",

"status": "Live",

"category": "target\_collection\_category",

"identifier": "agriculture\_frameeork\_select\_content\_type",

"description": **null**,

"associations": \[],

"translations": **null**

}

],

"default": "",

"visible": **true**,

"dataType": "list",

"editable": **true**,

"required": **true**,

"inputType": "select",

"description": "Target Collection Category",

"placeholder": "Select Target Collection Category",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

],

"templateName": "defaultTemplate"

}
