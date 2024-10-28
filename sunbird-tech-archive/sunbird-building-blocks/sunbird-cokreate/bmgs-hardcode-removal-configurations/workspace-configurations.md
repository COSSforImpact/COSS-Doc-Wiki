---
icon: elementor
---

# Workspace Configurations

1.Digital TextBook Object category definition with new framework

1.Login as a creator and go to workspace

2.Open digital textbook

3.Make a read call

https://staging.sunbirded.org/action/object/category/definition/v1/read?fields=objectMetadata,forms,name,label

objectCategoryDefinition: {objectType: "Collection", name: "Digital Textbook", channel: "01269934121990553633"}

![](<../../../../.gitbook/assets/0 (12).png>)

2.Import that and minimiize the objectCategoryDefinition **and copy from result**

3.Paste it on Request

URL:

[https://staging.sunbirded.org/api/object/category/definition/v1/update/obj-cat:digital-textbook\_collection\_01269934121990553633](https://staging.sunbirded.org/api/object/category/definition/v1/update/obj-cat:digital-textbook\_collection\_01269934121990553633)

{

"request": {

"channel": "01269934121990553633",

"name": "Digital Textbook",

"objectType": "Collection",

"objectCategoryDefinition": {

"objectMetadata": {

"config": {

"sourcingSettings": {

"collection": {

"maxDepth": 4,

"objectType": "Collection",

"primaryCategory": "Digital Textbook",

"isRoot": true,

"iconClass": "fa fa-book",

"children": {},

"hierarchy": {

"level1": {

"name": "Textbook Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "TextBookUnit",

"primaryCategory": "Textbook Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[],

"Collection": \[]

}

},

"level2": {

"name": "Section",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "TextBookUnit",

"primaryCategory": "Textbook Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[],

"Collection": \[]

}

},

"level3": {

"name": "Section",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "TextBookUnit",

"primaryCategory": "Textbook Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[],

"Collection": \[]

}

},

"level4": {

"name": "Section",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "TextBookUnit",

"primaryCategory": "Textbook Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[],

"Collection": \[]

}

}

}

}

}

},

"schema": {

"properties": {

"generateDIALCodes": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

},

"trackable": {

"type": "object",

"properties": {

"enabled": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "No"

},

"autoBatch": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "No"

}

},

"default": {

"enabled": "No",

"autoBatch": "No"

},

"additionalProperties": false

},

"additionalCategories": {

"type": "array",

"items": {

"type": "string"

},

"default": \[

"Textbook"

]

},

"userConsent": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

}

}

}

},

"languageCode": \[],

"name": "Digital Textbook",

"forms": {

"childMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "name",

"editable": true,

"displayProperty": "Editable",

"dataType": "text",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "Name",

"index": 1,

"label": "Name",

"required": true,

"name": "Name",

"inputType": "text",

"placeholder": "Name",

"validations": \[

{

"type": "maxLength",

"value": "120",

"message": "Exceeded the limit of 120 characters"

},

{

"type": "required",

"message": "Name is required"

}

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "1000",

"message": "Exceeded the limit of 1000 characters"

}

]

},

{

"code": "primaryCategory",

"dataType": "text",

"description": "Type",

"editable": false,

"renderingHints": {},

"inputType": "select",

"label": "Category",

"name": "Type",

"placeholder": "",

"required": true,

"visible": true,

"validations": \[]

},

{

"code": "additionalCategories",

"visible": true,

"editable": true,

"displayProperty": "Editable",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Additional Categories",

"index": 7,

"label": "Additional Categories",

"required": false,

"name": "additionalCategories",

"inputType": "nestedselect",

"placeholder": "Additional Categories"

},

{

"code": "boardIds",

"visible": true,

"depends": \[],

"editable": false,

"dataType": "list",

"sourceCategory": "board",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Framework",

"required": true,

"name": "Framework",

"inputType": "nestedselect",

"placeholder": "Select Framework"

},

{

"code": "farmingTypeIds",

"visible": true,

"depends": \[],

"editable": false,

"dataType": "list",

"sourceCategory": "farmingtype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Farming Type(s)",

"required": true,

"name": "farmingtype",

"inputType": "nestedselect",

"placeholder": "Select farmingtype"

},

{

"code": "cropCategoryIds",

"visible": true,

"depends": \[],

"editable": false,

"dataType": "list",

"sourceCategory": "cropcategory",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Crop Category(ies)",

"required": true,

"name": "Crop Category",

"inputType": "nestedselect",

"placeholder": "Select Crop Category"

},

{

"code": "cropTypeIds",

"visible": true,

"depends": \[],

"editable": false,

"dataType": "list",

"sourceCategory": "croptype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Crop Type(s)",

"required": true,

"name": "croptype",

"inputType": "nestedselect",

"placeholder": "Select croptype"

},

{

"code": "cropNameIds",

"visible": true,

"depends": \[],

"editable": false,

"dataType": "list",

"sourceCategory": "cropName",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Crop Name(s)",

"required": true,

"name": "cropName",

"inputType": "nestedselect",

"placeholder": "Select cropName"

},

{

"code": "topicsIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"boardIds",

"farmingTypeIds",

"cropCategoryIds",

"cropTypeIds"

],

"sourceCategory": "topic",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"name": "Topic",

"description": "Choose Topics",

"inputType": "topicselector",

"label": "Topic(s)",

"placeholder": "Select Topic",

"required": false,

"output": "identifier"

},

{

"code": "copyright",

"dataType": "text",

"description": "Copyright",

"editable": true,

"index": 4,

"inputType": "text",

"label": "Copyright and Year:",

"name": "Copyright",

"placeholder": "Enter Copyright and Year",

"tooltip": "If you are an individual, creating original content, you are the copyright holder. If you are creating this content on behalf of an organisation, the organisation may be the copyright holder. ",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"validations": \[

{

"type": "required",

"message": "Copyright is required"

}

]

},

{

"code": "license",

"visible": true,

"editable": true,

"displayProperty": "Editable",

"dataType": "text",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "License",

"index": 6,

"label": "License",

"required": true,

"name": "license",

"inputType": "select",

"placeholder": "license",

"tooltip": "Choose the more appropriate Creative commons license for this Content. ",

"validations": \[

{

"type": "required",

"message": "License is required"

}

]

},

{

"code": "author",

"dataType": "text",

"description": "Author",

"editable": true,

"index": 5,

"inputType": "text",

"label": "Author",

"name": "Author",

"placeholder": "Author",

"tooltip": "Provide name of creator of this content.",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": true,

"validations": \[

{

"type": "required",

"message": "Author is required"

}

]

},

{

"code": "attributions",

"dataType": "list",

"description": "Attributions",

"editable": true,

"index": 3,

"inputType": "text",

"label": "Attributions",

"name": "attribution",

"placeholder": "",

"tooltip": "If you have relied on another work to create this content, provide the name of that creator and the source of that work.",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false

},

{

"code": "contentPolicyCheck",

"visible": true,

"editable": true,

"displayProperty": "Editable",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "Content Policy check",

"index": 7,

"labelHtml": "\<p class='font-italic'>I agree that by submitting / publishing this Content, I confirm that this Content complies with prescribed guidelines, including the Terms of Use and Content Policy and that I consent to publish it under the \<a class='link font-weight-bold' href='https://creativecommons.org/licenses' target='\_blank'>Creative Commons Framework in \</a> accordance with the \<a class='link font-weight-bold' href='/terms-of-use.html' target='\_blank'> Content Policy.\</a> I have made sure that I do not violate others' copyright or privacy rights.\</p>",

"required": true,

"name": "contentPolicyCheck",

"inputType": "checkbox",

"placeholder": "Content Policy Check",

"validations": \[

{

"type": "required",

"message": "Content Policy Check is required"

}

]

}

]

},

"create": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "First Section",

"fields": \[

{

"code": "appIcon",

"dataType": "text",

"description": "appIcon of the content",

"editable": true,

"inputType": "appIcon",

"label": "Icon",

"name": "Icon",

"placeholder": "Icon",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true

},

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Name",

"name": "Name",

"placeholder": "Name",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "120",

"message": "Exceeded the limit of 120 characters"

},

{

"type": "required",

"message": "Name is required"

},

{

"type": "pattern",

"value": "\[a-zA-Z0-9 \_/.'-]+$",

"message": "Special characters are not allowed"

}

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "1000",

"message": "Exceeded the limit of 1000 characters"

},

{

"type": "required",

"message": "Description is required"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Input the keyword and press enter",

"required": false,

"validations": \[

{

"message": "Keywords is required"

}

]

}

]

},

{

"name": "Second Section",

"fields": \[

{

"code": "dialcodeRequired",

"dataType": "text",

"description": "QR CODE REQUIRED",

"editable": true,

"default": "No",

"index": 5,

"inputType": "radio",

"label": "QR code required?",

"name": "dialcodeRequired",

"placeholder": "QR code required?",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"range": \[

"Yes",

"No"

],

"required": false,

"visible": true

},

{

"code": "dialcodes",

"depends": \[

"dialcodeRequired"

],

"dataType": "list",

"description": "Digital Infrastructure for Augmented Learning",

"editable": true,

"inputType": "dialcode",

"label": "QR code",

"name": "dialcode",

"placeholder": "Enter code here",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "minLength",

"value": "2"

},

{

"type": "maxLength",

"value": "20"

}

]

}

]

},

{

"name": "Third Section",

"fields": \[

{

"code": "primaryCategory",

"dataType": "text",

"description": "Type",

"editable": false,

"renderingHints": {},

"inputType": "select",

"label": "Category",

"name": "Type",

"placeholder": "",

"required": true,

"visible": true,

"validations": \[]

},

{

"code": "additionalCategories",

"dataType": "list",

"description": "Additional Category of the Content",

"editable": true,

"inputType": "nestedselect",

"label": "Additional Category",

"name": "Additional Category",

"placeholder": "Select Additional Category",

"renderingHints": {},

"required": false,

"visible": true

}

]

},

{

"name": "Framework Terms",

"fields": \[

{

"code": "audience",

"dataType": "list",

"description": "Audience",

"editable": true,

"inputType": "nestedselect",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"label": "Audience Type",

"name": "Audience Type",

"placeholder": "Select Audience Type",

"required": false,

"visible": true,

"range": \[

"Administrator",

"Other"

]

},

{

"code": "boardIds",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "list",

"sourceCategory": "board",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "Board",

"label": "Framework",

"required": true,

"name": "Framework",

"inputType": "select",

"placeholder": "Select Framework",

"validations": \[

{

"type": "required",

"message": "Board is required"

}

]

},

{

"code": "farmingTypeIds",

"visible": true,

"depends": \[

"boardIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "farmingtype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Farming Type(s)",

"required": true,

"name": "farmingtype",

"inputType": "nestedselect",

"placeholder": "Select farmingtype",

"validations": \[

{

"type": "required",

"message": "farmingtype is required"

}

]

},

{

"code": "cropCategoryIds",

"visible": true,

"depends": \[

"boardIds",

"farmingTypeIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "cropcategory",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "Class",

"label": "Crop Category(ies)",

"required": true,

"name": "Class",

"inputType": "nestedselect",

"placeholder": "Select Crop Category",

"validations": \[

{

"type": "required",

"message": "cropcategory is required"

}

]

},

{

"code": "cropTypeIds",

"visible": true,

"depends": \[

"boardIds",

"farmingTypeIds",

"cropCategoryIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "croptype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Crop Type(s)",

"required": true,

"name": "croptype",

"inputType": "nestedselect",

"placeholder": "Select croptype",

"validations": \[

{

"type": "required",

"message": "croptype is required"

}

]

},

{

"code": "cropNameIds",

"visible": true,

"depends": \[

"boardIds",

"farmingTypeIds",

"cropCategoryIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "cropName",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Crop Name(s)",

"required": true,

"name": "Crop Name",

"inputType": "nestedselect",

"placeholder": "Select Crop Name",

"validations": \[

{

"type": "required",

"message": "Crop Name is required"

}

]

}

]

},

{

"name": "Fourth Section",

"fields": \[

{

"code": "author",

"dataType": "text",

"description": "Author of the content",

"editable": true,

"inputType": "text",

"label": "Author",

"name": "Author",

"placeholder": "Author",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "attributions",

"dataType": "list",

"description": "Attributions",

"editable": true,

"inputType": "text",

"label": "Attributions",

"name": "Attributions",

"placeholder": "Attributions",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "copyright",

"dataType": "text",

"description": "Copyright",

"editable": true,

"inputType": "text",

"label": "Copyright",

"name": "Copyright",

"placeholder": "Copyright",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "required",

"message": "Copyright is required"

}

]

},

{

"code": "copyrightYear",

"dataType": "number",

"description": "Year",

"editable": true,

"inputType": "text",

"label": "Copyright Year",

"name": "Copyright Year",

"placeholder": "Copyright Year",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "required",

"message": "Copyright Year is required"

},

{

"type": "minLength",

"message": "Year should be a 4 digit number",

"value": 4

},

{

"type": "maxLength",

"message": "Year should be a 4 digit number",

"value": 4

}

]

},

{

"code": "license",

"dataType": "text",

"description": "license",

"editable": true,

"inputType": "select",

"label": "License",

"name": "license",

"placeholder": "Select License",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"defaultValue": "CC BY 4.0",

"validations": \[

{

"type": "required",

"message": "License is required"

}

]

}

]

}

]

},

"delete": {},

"publish": {},

"publishchecklist": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "Appropriateness",

"renderingHints": {

"class": "d-grid-inline-3 display-sectionName"

},

"fields": \[

{

"code": "appropriatenessOne",

"name": "No Hate speech, Abuse, Violence, Profanity",

"label": "No Hate speech, Abuse, Violence, Profanity",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "appropriatenessTwo",

"name": "No Sexual content, Nudity or Vulgarity",

"label": "No Sexual content, Nudity or Vulgarity",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "appropriatenessThree",

"name": "No Discrimination or Defamation",

"label": "No Discrimination or Defamation",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "appropriatenessFour",

"name": "Is suitable for children",

"label": "Is suitable for children",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

},

{

"name": "Content details",

"renderingHints": {

"class": "d-grid-inline-3 display-sectionName"

},

"fields": \[

{

"code": "contentdetailsOne",

"name": "Appropriate Title, Description",

"label": "Appropriate Title, Description",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "contentdetailsTwo",

"name": "Correct Board, Grade, croptype, farmingtype",

"label": "Correct Board, Grade, croptype, farmingtype",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "contentdetailsThree",

"name": "Appropriate tags such as Resource Type, Concepts",

"label": "Appropriate tags such as Resource Type, Concepts",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "contentdetailsFour",

"name": "Relevant Keywords",

"label": "Relevant Keywords",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

},

{

"name": "Usability",

"renderingHints": {

"class": "d-grid-inline-3 display-sectionName"

},

"fields": \[

{

"code": "usabilityOne",

"name": "Content plays correctly",

"label": "Content plays correctly",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "usabilityTwo",

"name": "Can see the content clearly on Desktop and App",

"label": "Can see the content clearly on Desktop and App",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "usabilityThree",

"name": "Audio (if any) is clear and easy to understand",

"label": "Audio (if any) is clear and easy to understand",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "usabilityFour",

"name": "No Spelling mistakes in the text",

"label": "No Spelling mistakes in the text",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "usabilityFive",

"name": "Language is simple to understand",

"label": "Language is simple to understand",

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"validations": \[

{

"type": "required",

"message": ""

}

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

}

]

},

"relationalMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Name of the content",

"name": "Name of the content",

"placeholder": "Name of the content",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Name is required"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Input the keyword and PRESS enter",

"required": false,

"validations": \[]

},

{

"code": "optional",

"name": "Track in collection",

"label": "Track in collection",

"placeholder": "Track in collection",

"description": "",

"default": false,

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

},

"review": {},

"search": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "primaryCategory",

"dataType": "list",

"description": "Type",

"editable": true,

"default": \[],

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"inputType": "nestedselect",

"label": "Content Type(s)",

"name": "Type",

"placeholder": "Select ContentType",

"required": false,

"visible": true

},

{

"code": "board",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Board",

"label": "Framework",

"required": false,

"name": "Board",

"inputType": "select",

"placeholder": "Select Board",

"output": "name"

},

{

"code": "farmingtype",

"visible": true,

"depends": \[

"board"

],

"editable": true,

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "farmingtype(s)",

"required": false,

"name": "farmingtype",

"inputType": "nestedselect",

"placeholder": "Select farmingtype",

"output": "name"

},

{

"code": "cropcategory",

"visible": true,

"depends": \[

"board",

"farmingtype"

],

"editable": true,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Crop Category",

"label": "Crop Category(ies)",

"required": false,

"name": "Class",

"inputType": "nestedselect",

"placeholder": "Select Crop Category",

"output": "name"

},

{

"code": "croptype",

"visible": true,

"depends": \[

"board",

"farmingtype",

"cropcategory"

],

"editable": true,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "croptype(s)",

"required": false,

"name": "croptype",

"inputType": "nestedselect",

"placeholder": "Select croptype",

"output": "name"

},

{

"code": "cropName",

"visible": true,

"depends": \[

"board",

"farmingtype",

"cropcategory"

],

"editable": true,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Crop Name(s)",

"required": false,

"name": "cropName",

"inputType": "nestedselect",

"placeholder": "Select cropName",

"output": "name"

},

{

"code": "topic",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"board",

"farmingtype",

"cropcategory",

"croptype"

],

"default": "",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"name": "Topic",

"description": "Choose a Topics",

"inputType": "topicselector",

"label": "Topic(s)",

"placeholder": "Choose Topics",

"required": false

}

]

},

"unitMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "First Section",

"fields": \[

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Name",

"name": "Title",

"placeholder": "Name",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "120",

"message": "Exceeded the limit of 120 characters"

},

{

"type": "required",

"message": "Name is required"

}

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "1000",

"message": "Exceeded the limit of 120 characters"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"index": 3,

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Input the keyword and press enter",

"required": false,

"validations": \[]

},

{

"code": "topic",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"board",

"farmingtype",

"cropcategory",

"croptype"

],

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"name": "Topic",

"description": "Choose a Topics",

"inputType": "topicselector",

"label": "Topics covered in the course",

"placeholder": "Choose Topics",

"required": false

},

{

"code": "dialcodeRequired",

"dataType": "text",

"description": "QR CODE REQUIRED",

"editable": true,

"default": "No",

"index": 5,

"inputType": "radio",

"label": "QR code required?",

"name": "dialcodeRequired",

"placeholder": "QR code required?",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"range": \[

"Yes",

"No"

],

"required": false,

"visible": true

},

{

"code": "dialcodes",

"depends": \[

"dialcodeRequired"

],

"dataType": "list",

"description": "Digital Infrastructure for Augmented Learning",

"editable": true,

"inputType": "dialcode",

"label": "QR code",

"name": "dialcode",

"placeholder": "Enter code here",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "minLength",

"value": "2"

},

{

"type": "maxLength",

"value": "20"

}

]

}

]

}

]

},

"update": {}

}

}

}

}

**Course:**

1. Follow same steps like digital text book
2. Open course and make a read call

URL:\{{host\}}api/object/category/definition/v1/update/obj-cat:course\_collection\_01269934121990553633

**Object category:**

{

"request": {

"channel": "01269934121990553633",

"name": "Course",

"objectType": "Collection",

"objectCategoryDefinition": {

"objectMetadata": {

"config": {

"frameworkMetadata": {

"orgFWType": \[

"K-12",

"TPD"

],

"targetFWType": \[

"K-12"

]

},

"sourcingSettings": {

"collection": {

"maxDepth": 4,

"objectType": "Collection",

"primaryCategory": "Course",

"isRoot": true,

"iconClass": "fa fa-book",

"children": {},

"hierarchy": {

"level1": {

"name": "Course Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "CourseUnit",

"primaryCategory": "Course Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[]

}

},

"level2": {

"name": "Course Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "CourseUnit",

"primaryCategory": "Course Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[]

}

},

"level3": {

"name": "Course Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "CourseUnit",

"primaryCategory": "Course Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[]

}

},

"level4": {

"name": "Course Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "CourseUnit",

"primaryCategory": "Course Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[]

}

}

}

}

}

},

"forms": {

"create": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "First Section",

"fields": \[

{

"code": "appIcon",

"dataType": "text",

"description": "appIcon of the content",

"editable": true,

"inputType": "appIcon",

"label": "Icon",

"name": "Icon",

"placeholder": "Icon",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true

},

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "framework",

"label": "Title",

"name": "Name",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

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

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "512",

"message": "Input is Exceeded"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Input the keyword and PRESS enter",

"required": false,

"validations": \[]

},

{

"code": "dialcodeRequired",

"dataType": "list",

"description": "QR CODE REQUIRED",

"editable": true,

"default": "No",

"index": 5,

"inputType": "radio",

"label": "QR code required",

"name": "dialcodeRequired",

"placeholder": "QR code required",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"range": \[

"Yes",

"No"

],

"required": false,

"visible": true

},

{

"code": "dialcodes",

"depends": \[

"dialcodeRequired"

],

"dataType": "list",

"description": "Digital Infrastructure for Augmented Learning",

"editable": true,

"inputType": "dialcode",

"label": "QR code",

"name": "dialcode",

"placeholder": "Enter code here",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "minLength",

"value": "2"

},

{

"type": "maxLength",

"value": "20"

}

]

}

]

},

{

"name": "Second Section",

"fields": \[

{

"code": "primaryCategory",

"dataType": "text",

"description": "Type",

"editable": false,

"renderingHints": {},

"inputType": "select",

"label": "Category",

"name": "Type",

"placeholder": "",

"required": true,

"visible": true,

"validations": \[]

},

{

"code": "additionalCategories",

"dataType": "list",

"depends": \[

"primaryCategory"

],

"description": "Additonal Category of the Content",

"editable": true,

"inputType": "nestedselect",

"label": "Additional Category",

"name": "Additional Category",

"placeholder": "Select Additional Category",

"renderingHints": {},

"required": false,

"visible": true

}

]

},

{

"name": "Organisation Framework Terms",

"fields": \[

{

"code": "framework",

"visible": true,

"editable": true,

"dataType": "text",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Course Type",

"required": true,

"name": "Framework",

"inputType": "framework",

"placeholder": "Select Course Type",

"output": "identifier",

"validations": \[

{

"type": "required",

"message": "Course Type is required"

}

]

},

{

"code": "subjectIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"framework"

],

"sourceCategory": "subject",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Subjects covered in the course",

"required": true,

"name": "Subject",

"inputType": "frameworkCategorySelect",

"placeholder": "Select Subject(s)",

"output": "identifier",

"validations": \[

{

"type": "required",

"message": "Subjects Taught is required"

}

]

},

{

"code": "topicsIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"framework",

"subjectIds"

],

"sourceCategory": "topic",

"renderingHints": {},

"name": "Topic",

"description": "Choose a Topics",

"inputType": "topicselector",

"label": "Topics covered in the course",

"placeholder": "Choose Topics",

"required": false,

"output": "identifier"

}

]

},

{

"name": "Target Framework Terms",

"fields": \[

{

"code": "audience",

"dataType": "list",

"description": "Audience",

"editable": true,

"inputType": "nestedselect",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"label": "Audience Type",

"name": "Audience Type",

"placeholder": "Select Audience Type",

"required": false,

"visible": true,

"range": \[

"Student",

"Teacher",

"Parent",

"Administrator",

"Other"

]

},

{

"code": "targetfarmingtypeIds",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "text",

"sourceCategory": "armingtype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "FarmingTtype",

"label": "FarmingTtype",

"required": true,

"name": "FarmingTtype",

"inputType": "select",

"placeholder": "Select Farmingtype",

"validations": \[

{

"type": "required",

"message": "Farming Type is required"

}

]

},

{

"code": "targetMediumIds",

"visible": true,

"depends": \[

"targetfarmingtypeIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "medium",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Medium(s) of the audience",

"required": true,

"name": "Medium",

"inputType": "nestedselect",

"placeholder": "Select Medium",

"validations": \[

{

"type": "required",

"message": "Medium is required"

}

]

},

{

"code": "targetGradeLevelIds",

"visible": true,

"depends": \[

"targetBoardIds",

"targetMediumIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "gradeLevel",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "Class",

"label": "Class(es) of the audience",

"required": true,

"name": "Class",

"inputType": "nestedselect",

"placeholder": "Select Class",

"validations": \[

{

"type": "required",

"message": "Class is required"

}

]

},

{

"code": "targetSubjectIds",

"visible": true,

"depends": \[

"targetBoardIds",

"targetMediumIds",

"targetGradeLevelIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "subject",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Subject(s) of the audience",

"required": true,

"name": "Subject",

"inputType": "nestedselect",

"placeholder": "Select Subject",

"validations": \[

{

"type": "required",

"message": "Subject is required"

}

]

}

]

},

{

"name": "Fourth Section",

"fields": \[

{

"code": "author",

"dataType": "text",

"description": "Author of the content",

"editable": true,

"inputType": "text",

"label": "Author",

"name": "Author",

"placeholder": "Author",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "attributions",

"dataType": "text",

"description": "Attributions",

"editable": true,

"inputType": "text",

"label": "Attributions",

"name": "Attributions",

"placeholder": "Attributions",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "copyright",

"dataType": "text",

"description": "Copyright",

"editable": true,

"inputType": "text",

"label": "Copyright",

"name": "Copyright & year",

"placeholder": "Copyright",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "required",

"message": "Copyright is required"

}

]

},

{

"code": "showTimer",

"name": "Show Timer",

"label": "Show Timer",

"placeholder": "Show Timer",

"description": "Show Timer",

"default": "No",

"dataType": "text",

"inputType": "select",

"range": \[

"Yes",

"No"

],

"editable": true,

"required": true,

"visible": true,

"depends": \[

"maxTime"

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "license",

"dataType": "text",

"description": "license",

"editable": true,

"inputType": "select",

"label": "License",

"name": "license",

"placeholder": "Select License",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"defaultValue": "CC BY 4.0",

"validations": \[

{

"type": "required",

"message": "License is required"

}

]

}

]

}

]

}

},

"schema": {

"properties": {

"trackable": {

"type": "object",

"properties": {

"enabled": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

},

"autoBatch": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "No"

}

},

"default": {

"enabled": "Yes",

"autoBatch": "No"

},

"additionalProperties": false

},

"monitorable": {

"type": "array",

"items": {

"type": "string",

"enum": \[

"progress-report",

"score-report"

]

}

},

"credentials": {

"type": "object",

"properties": {

"enabled": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

}

},

"default": {

"enabled": "Yes"

},

"additionalProperties": false

},

"userConsent": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

},

"mimeType": {

"type": "string",

"enum": \[

"application/vnd.ekstep.content-collection"

]

},

"discussionForum": {

"type": "object",

"properties": {

"enabled": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

}

},

"default": {

"enabled": "Yes"

},

"additionalProperties": false

}

}

}

},

"languageCode": \[],

"name": "Course",

"forms": {

"create": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "First Section",

"fields": \[

{

"code": "appIcon",

"dataType": "text",

"description": "appIcon of the content",

"editable": true,

"inputType": "appIcon",

"label": "Icon",

"name": "Icon",

"placeholder": "Icon",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true

},

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Title",

"name": "Name",

"placeholder": "Title",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "max",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Title is required"

}

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true,

"validations": \[

{

"type": "max",

"value": "256",

"message": "Input is Exceeded"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Enter Keywords",

"required": false,

"validations": \[]

}

]

},

{

"name": "Second Section",

"fields": \[

{

"code": "primaryCategory",

"dataType": "text",

"description": "Type",

"editable": false,

"renderingHints": {},

"inputType": "select",

"label": "Category",

"name": "Type",

"placeholder": "",

"required": true,

"visible": true,

"validations": \[]

},

{

"code": "additionalCategories",

"dataType": "list",

"depends": \[

"primaryCategory"

],

"description": "Additonal Category of the Content",

"editable": true,

"inputType": "nestedselect",

"label": "Additional Category",

"name": "Additional Category",

"placeholder": "Select Additional Category",

"renderingHints": {},

"required": false,

"visible": true

}

]

},

{

"name": "Organisation Framework Terms",

"fields": \[

{

"code": "framework",

"visible": true,

"editable": true,

"dataType": "text",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Course Type",

"required": true,

"name": "Framework",

"inputType": "framework",

"placeholder": "Select Course Type",

"output": "identifier",

"validations": \[

{

"type": "required",

"message": "Course Type is required"

}

]

},

{

"code": "cropnameIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"framework"

],

"sourceCategory": "cropname",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Crop Name",

"required": false,

"name": "Crop Name",

"inputType": "frameworkCategorySelect",

"placeholder": "Select Crop Name(s)",

"output": "identifier"

},

{

"code": "topicsIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"framework",

"cropnameIds"

],

"sourceCategory": "topic",

"renderingHints": {},

"name": "Topic",

"description": "Choose a Topics",

"inputType": "topicselector",

"label": "Crop Variety",

"placeholder": "Choose Topics",

"required": false,

"output": "identifier"

}

]

},

{

"name": "Target Framework Terms",

"fields": \[

{

"code": "audience",

"dataType": "list",

"description": "Audience",

"editable": true,

"inputType": "nestedselect",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"label": "Audience Type",

"name": "Audience Type",

"placeholder": "Select Audience Type",

"required": false,

"visible": true,

"range": \[

"Others",

"Administrator"

]

},

{

"code": "targetfarmingtypeIds",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "list",

"sourceCategory": "farmingtype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "Farming Type",

"label": "Farming Type",

"required": true,

"name": "Farming Type",

"inputType": "select",

"placeholder": "Select Farmingtype",

"validations": \[

{

"type": "required",

"message": "Farming Type is required"

}

]

},

{

"code": "targetcropcategoryIds",

"visible": true,

"depends": \[

"targetfarmingtypeIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "cropcategory",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Crop Category(s)",

"required": true,

"name": "cropcategory",

"inputType": "nestedselect",

"placeholder": "Select cropcategory",

"validations": \[

{

"type": "required",

"message": "cropcategory is required"

}

]

},

{

"code": "croptypeIds",

"visible": true,

"depends": \[

"targetfarmingtypeIds",

"targetcropcategoryIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "croptype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "croptype",

"label": "Crop Type(s)",

"required": true,

"name": "croptype",

"inputType": "nestedselect",

"placeholder": "Select Crop Type",

"validations": \[

{

"type": "required",

"message": "crop type is required"

}

]

},

{

"code": "targetCropnameIds",

"visible": true,

"depends": \[

"targetfarmingtypeIds",

"targetcropcategoryIds",

"targetcroptypeIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "cropname",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Crop Name(s)",

"required": true,

"name": "cropname",

"inputType": "nestedselect",

"placeholder": "Select cropname",

"validations": \[

{

"type": "required",

"message": "Cropname is required"

}

]

}

]

},

{

"name": "Fourth Section",

"fields": \[

{

"code": "author",

"dataType": "text",

"description": "Author of the content",

"editable": true,

"inputType": "text",

"label": "Author",

"name": "Author",

"placeholder": "Author",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "attributions",

"dataType": "text",

"description": "Attributions",

"editable": true,

"inputType": "text",

"label": "Attributions",

"name": "Attributions",

"placeholder": "Attributions",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "copyright",

"dataType": "text",

"description": "Copyright",

"editable": true,

"inputType": "text",

"label": "Copyright",

"name": "Copyright & year",

"placeholder": "Copyright",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "required",

"message": "Copyright is required"

}

]

},

{

"code": "copyrightYear",

"dataType": "number",

"description": "Year",

"editable": true,

"inputType": "text",

"label": "Copyright Year",

"name": "Copyright Year",

"placeholder": "Copyright Year",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "required",

"message": "Copyright Year is required"

}

]

},

{

"code": "license",

"dataType": "text",

"description": "license",

"editable": true,

"inputType": "select",

"label": "License",

"name": "license",

"placeholder": "Select License",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"defaultValue": "CC BY 4.0",

"validations": \[

{

"type": "required",

"message": "License is required"

}

]

}

]

}

]

},

"relationalMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Name of the content",

"name": "Name of the content",

"placeholder": "Name of the content",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Name is required"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Input the keyword and PRESS enter",

"required": false,

"validations": \[]

},

{

"code": "optional",

"name": "Track in collection",

"label": "Track in collection",

"placeholder": "Track in collection",

"description": "",

"default": false,

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

},

"search": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "primaryCategory",

"dataType": "list",

"description": "Type",

"editable": true,

"default": \[],

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"inputType": "nestedselect",

"label": "Content Type(s)",

"name": "Type",

"placeholder": "Select ContentType",

"required": false,

"visible": true

},

{

"code": "board",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Board",

"label": "Board",

"required": false,

"name": "Board",

"inputType": "select",

"placeholder": "Select Board",

"output": "name"

},

{

"code": "medium",

"visible": true,

"depends": \[

"board"

],

"editable": true,

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Medium(s)",

"required": false,

"name": "Medium",

"inputType": "nestedselect",

"placeholder": "Select Medium",

"output": "name"

},

{

"code": "gradeLevel",

"visible": true,

"depends": \[

"board",

"medium"

],

"editable": true,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Class",

"label": "Class(es)",

"required": false,

"name": "Class",

"inputType": "nestedselect",

"placeholder": "Select Class",

"output": "name"

},

{

"code": "subject",

"visible": true,

"depends": \[

"board",

"medium",

"gradeLevel"

],

"editable": true,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Subject(s)",

"required": false,

"name": "Subject",

"inputType": "nestedselect",

"placeholder": "Select Subject",

"output": "name"

},

{

"code": "topic",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"board",

"medium",

"gradeLevel",

"subject"

],

"default": "",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"name": "Topic",

"description": "Choose a Topics",

"inputType": "topicselector",

"label": "Topic(s)",

"placeholder": "Choose Topics",

"required": false

}

]

},

"unitMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "First Section",

"fields": \[

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Title",

"name": "Title",

"placeholder": "Title",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "max",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Title is required"

}

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true,

"validations": \[

{

"type": "max",

"value": "256",

"message": "Input is Exceeded"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"index": 3,

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Enter Keywords",

"required": false,

"validations": \[]

},

{

"code": "topic",

"visible": true,

"depends": \[],**Object category**

"editable": true,

"dataType": "list",

"renderingHints": {},

"name": "Topic",

"description": "Choose a Topics",

"index": 11,

"inputType": "topicselector",

"label": "Topics",

"placeholder": "Choose Topics",

"required": false,

"validations": \[]

}

]

}

]

}

}

}

}

}

**Content Playlist:**

URL:\{{host\}}api/object/category/definition/v1/update/obj-cat:course\_collection\_01269934121990553633

**"objectCategoryDefinition":**

{

"request": {

"channel": "01269934121990553633",

"name": "Course",

"objectType": "Collection",

"objectCategoryDefinition": {

"objectMetadata": {

"config": {

"frameworkMetadata": {

"orgFWType": \[

"K-12",

"TPD"

],

"targetFWType": \[

"K-12"

]

},

"sourcingSettings": {

"collection": {

"maxDepth": 4,

"objectType": "Collection",

"primaryCategory": "Course",

"isRoot": true,

"iconClass": "fa fa-book",

"children": {},

"hierarchy": {

"level1": {

"name": "Course Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "CourseUnit",

"primaryCategory": "Course Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[]

}

},

"level2": {

"name": "Course Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "CourseUnit",

"primaryCategory": "Course Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[]

}

},

"level3": {

"name": "Course Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "CourseUnit",

"primaryCategory": "Course Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[]

}

},

"level4": {

"name": "Course Unit",

"type": "Unit",

"mimeType": "application/vnd.ekstep.content-collection",

"contentType": "CourseUnit",

"primaryCategory": "Course Unit",

"iconClass": "fa fa-folder-o",

"children": {

"Content": \[]

}

}

}

}

}

},

"forms": {

"create": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "First Section",

"fields": \[

{

"code": "appIcon",

"dataType": "text",

"description": "appIcon of the content",

"editable": true,

"inputType": "appIcon",

"label": "Icon",

"name": "Icon",

"placeholder": "Icon",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true

},

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "framework",

"label": "Title",

"name": "Name",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

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

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "512",

"message": "Input is Exceeded"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Input the keyword and PRESS enter",

"required": false,

"validations": \[]

},

{

"code": "dialcodeRequired",

"dataType": "list",

"description": "QR CODE REQUIRED",

"editable": true,

"default": "No",

"index": 5,

"inputType": "radio",

"label": "QR code required",

"name": "dialcodeRequired",

"placeholder": "QR code required",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"range": \[

"Yes",

"No"

],

"required": false,

"visible": true

},

{

"code": "dialcodes",

"depends": \[

"dialcodeRequired"

],

"dataType": "list",

"description": "Digital Infrastructure for Augmented Learning",

"editable": true,

"inputType": "dialcode",

"label": "QR code",

"name": "dialcode",

"placeholder": "Enter code here",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "minLength",

"value": "2"

},

{

"type": "maxLength",

"value": "20"

}

]

}

]

},

{

"name": "Second Section",

"fields": \[

{

"code": "primaryCategory",

"dataType": "text",

"description": "Type",

"editable": false,

"renderingHints": {},

"inputType": "select",

"label": "Category",

"name": "Type",

"placeholder": "",

"required": true,

"visible": true,

"validations": \[]

},

{

"code": "additionalCategories",

"dataType": "list",

"depends": \[

"primaryCategory"

],

"description": "Additonal Category of the Content",

"editable": true,

"inputType": "nestedselect",

"label": "Additional Category",

"name": "Additional Category",

"placeholder": "Select Additional Category",

"renderingHints": {},

"required": false,

"visible": true

}

]

},

{

"name": "Organisation Framework Terms",

"fields": \[

{

"code": "framework",

"visible": true,

"editable": true,

"dataType": "text",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Course Type",

"required": true,

"name": "Framework",

"inputType": "framework",

"placeholder": "Select Course Type",

"output": "identifier",

"validations": \[

{

"type": "required",

"message": "Course Type is required"

}

]

},

{

"code": "subjectIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"framework"

],

"sourceCategory": "subject",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Subjects covered in the course",

"required": true,

"name": "Subject",

"inputType": "frameworkCategorySelect",

"placeholder": "Select Subject(s)",

"output": "identifier",

"validations": \[

{

"type": "required",

"message": "Subjects Taught is required"

}

]

},

{

"code": "topicsIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"framework",

"subjectIds"

],

"sourceCategory": "topic",

"renderingHints": {},

"name": "Topic",

"description": "Choose a Topics",

"inputType": "topicselector",

"label": "Topics covered in the course",

"placeholder": "Choose Topics",

"required": false,

"output": "identifier"

}

]

},

{

"name": "Target Framework Terms",

"fields": \[

{

"code": "audience",

"dataType": "list",

"description": "Audience",

"editable": true,

"inputType": "nestedselect",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"label": "Audience Type",

"name": "Audience Type",

"placeholder": "Select Audience Type",

"required": false,

"visible": true,

"range": \[

"Student",

"Teacher",

"Parent",

"Administrator",

"Other"

]

},

{

"code": "targetfarmingtypeIds",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "text",

"sourceCategory": "armingtype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "FarmingTtype",

"label": "FarmingTtype",

"required": true,

"name": "FarmingTtype",

"inputType": "select",

"placeholder": "Select Farmingtype",

"validations": \[

{

"type": "required",

"message": "Farming Type is required"

}

]

},

{

"code": "targetMediumIds",

"visible": true,

"depends": \[

"targetfarmingtypeIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "medium",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Medium(s) of the audience",

"required": true,

"name": "Medium",

"inputType": "nestedselect",

"placeholder": "Select Medium",

"validations": \[

{

"type": "required",

"message": "Medium is required"

}

]

},

{

"code": "targetGradeLevelIds",

"visible": true,

"depends": \[

"targetBoardIds",

"targetMediumIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "gradeLevel",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "Class",

"label": "Class(es) of the audience",

"required": true,

"name": "Class",

"inputType": "nestedselect",

"placeholder": "Select Class",

"validations": \[

{

"type": "required",

"message": "Class is required"

}

]

},

{

"code": "targetSubjectIds",

"visible": true,

"depends": \[

"targetBoardIds",

"targetMediumIds",

"targetGradeLevelIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "subject",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Subject(s) of the audience",

"required": true,

"name": "Subject",

"inputType": "nestedselect",

"placeholder": "Select Subject",

"validations": \[

{

"type": "required",

"message": "Subject is required"

}

]

}

]

},

{

"name": "Fourth Section",

"fields": \[

{

"code": "author",

"dataType": "text",

"description": "Author of the content",

"editable": true,

"inputType": "text",

"label": "Author",

"name": "Author",

"placeholder": "Author",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "attributions",

"dataType": "text",

"description": "Attributions",

"editable": true,

"inputType": "text",

"label": "Attributions",

"name": "Attributions",

"placeholder": "Attributions",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "copyright",

"dataType": "text",

"description": "Copyright",

"editable": true,

"inputType": "text",

"label": "Copyright",

"name": "Copyright & year",

"placeholder": "Copyright",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "required",

"message": "Copyright is required"

}

]

},

{

"code": "showTimer",

"name": "Show Timer",

"label": "Show Timer",

"placeholder": "Show Timer",

"description": "Show Timer",

"default": "No",

"dataType": "text",

"inputType": "select",

"range": \[

"Yes",

"No"

],

"editable": true,

"required": true,

"visible": true,

"depends": \[

"maxTime"

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "license",

"dataType": "text",

"description": "license",

"editable": true,

"inputType": "select",

"label": "License",

"name": "license",

"placeholder": "Select License",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"defaultValue": "CC BY 4.0",

"validations": \[

{

"type": "required",

"message": "License is required"

}

]

}

]

}

]

}

},

"schema": {

"properties": {

"trackable": {

"type": "object",

"properties": {

"enabled": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

},

"autoBatch": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "No"

}

},

"default": {

"enabled": "Yes",

"autoBatch": "No"

},

"additionalProperties": false

},

"monitorable": {

"type": "array",

"items": {

"type": "string",

"enum": \[

"progress-report",

"score-report"

]

}

},

"credentials": {

"type": "object",

"properties": {

"enabled": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

}

},

"default": {

"enabled": "Yes"

},

"additionalProperties": false

},

"userConsent": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

},

"mimeType": {

"type": "string",

"enum": \[

"application/vnd.ekstep.content-collection"

]

},

"discussionForum": {

"type": "object",

"properties": {

"enabled": {

"type": "string",

"enum": \[

"Yes",

"No"

],

"default": "Yes"

}

},

"default": {

"enabled": "Yes"

},

"additionalProperties": false

}

}

}

},

"languageCode": \[],

"name": "Course",

"forms": {

"create": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "First Section",

"fields": \[

{

"code": "appIcon",

"dataType": "text",

"description": "appIcon of the content",

"editable": true,

"inputType": "appIcon",

"label": "Icon",

"name": "Icon",

"placeholder": "Icon",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true

},

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Title",

"name": "Name",

"placeholder": "Title",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "max",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Title is required"

}

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true,

"validations": \[

{

"type": "max",

"value": "256",

"message": "Input is Exceeded"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Enter Keywords",

"required": false,

"validations": \[]

}

]

},

{

"name": "Second Section",

"fields": \[

{

"code": "primaryCategory",

"dataType": "text",

"description": "Type",

"editable": false,

"renderingHints": {},

"inputType": "select",

"label": "Category",

"name": "Type",

"placeholder": "",

"required": true,

"visible": true,

"validations": \[]

},

{

"code": "additionalCategories",

"dataType": "list",

"depends": \[

"primaryCategory"

],

"description": "Additonal Category of the Content",

"editable": true,

"inputType": "nestedselect",

"label": "Additional Category",

"name": "Additional Category",

"placeholder": "Select Additional Category",

"renderingHints": {},

"required": false,

"visible": true

}

]

},

{

"name": "Organisation Framework Terms",

"fields": \[

{

"code": "framework",

"visible": true,

"editable": true,

"dataType": "text",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Course Type",

"required": true,

"name": "Framework",

"inputType": "framework",

"placeholder": "Select Course Type",

"output": "identifier",

"validations": \[

{

"type": "required",

"message": "Course Type is required"

}

]

},

{

"code": "cropnameIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"framework"

],

"sourceCategory": "cropname",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Crop Name",

"required": false,

"name": "Crop Name",

"inputType": "frameworkCategorySelect",

"placeholder": "Select Crop Name(s)",

"output": "identifier"

},

{

"code": "topicsIds",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"framework",

"cropnameIds"

],

"sourceCategory": "topic",

"renderingHints": {},

"name": "Topic",

"description": "Choose a Topics",

"inputType": "topicselector",

"label": "Crop Variety",

"placeholder": "Choose Topics",

"required": false,

"output": "identifier"

}

]

},

{

"name": "Target Framework Terms",

"fields": \[

{

"code": "audience",

"dataType": "list",

"description": "Audience",

"editable": true,

"inputType": "nestedselect",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"label": "Audience Type",

"name": "Audience Type",

"placeholder": "Select Audience Type",

"required": false,

"visible": true,

"range": \[

"Others",

"Administrator"

]

},

{

"code": "targetfarmingtypeIds",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "list",

"sourceCategory": "farmingtype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "Farming Type",

"label": "Farming Type",

"required": true,

"name": "Farming Type",

"inputType": "select",

"placeholder": "Select Farmingtype",

"validations": \[

{

"type": "required",

"message": "Farming Type is required"

}

]

},

{

"code": "targetcropcategoryIds",

"visible": true,

"depends": \[

"targetfarmingtypeIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "cropcategory",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Crop Category(s)",

"required": true,

"name": "cropcategory",

"inputType": "nestedselect",

"placeholder": "Select cropcategory",

"validations": \[

{

"type": "required",

"message": "cropcategory is required"

}

]

},

{

"code": "croptypeIds",

"visible": true,

"depends": \[

"targetfarmingtypeIds",

"targetcropcategoryIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "croptype",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "croptype",

"label": "Crop Type(s)",

"required": true,

"name": "croptype",

"inputType": "nestedselect",

"placeholder": "Select Crop Type",

"validations": \[

{

"type": "required",

"message": "crop type is required"

}

]

},

{

"code": "targetCropnameIds",

"visible": true,

"depends": \[

"targetfarmingtypeIds",

"targetcropcategoryIds",

"targetcroptypeIds"

],

"editable": true,

"dataType": "list",

"sourceCategory": "cropname",

"output": "identifier",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"description": "",

"label": "Crop Name(s)",

"required": true,

"name": "cropname",

"inputType": "nestedselect",

"placeholder": "Select cropname",

"validations": \[

{

"type": "required",

"message": "Cropname is required"

}

]

}

]

},

{

"name": "Fourth Section",

"fields": \[

{

"code": "author",

"dataType": "text",

"description": "Author of the content",

"editable": true,

"inputType": "text",

"label": "Author",

"name": "Author",

"placeholder": "Author",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "attributions",

"dataType": "text",

"description": "Attributions",

"editable": true,

"inputType": "text",

"label": "Attributions",

"name": "Attributions",

"placeholder": "Attributions",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true

},

{

"code": "copyright",

"dataType": "text",

"description": "Copyright",

"editable": true,

"inputType": "text",

"label": "Copyright",

"name": "Copyright & year",

"placeholder": "Copyright",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "required",

"message": "Copyright is required"

}

]

},

{

"code": "copyrightYear",

"dataType": "number",

"description": "Year",

"editable": true,

"inputType": "text",

"label": "Copyright Year",

"name": "Copyright Year",

"placeholder": "Copyright Year",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "required",

"message": "Copyright Year is required"

}

]

},

{

"code": "license",

"dataType": "text",

"description": "license",

"editable": true,

"inputType": "select",

"label": "License",

"name": "license",

"placeholder": "Select License",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"defaultValue": "CC BY 4.0",

"validations": \[

{

"type": "required",

"message": "License is required"

}

]

}

]

}

]

},

"relationalMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Name of the content",

"name": "Name of the content",

"placeholder": "Name of the content",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "maxLength",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Name is required"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Input the keyword and PRESS enter",

"required": false,

"validations": \[]

},

{

"code": "optional",

"name": "Track in collection",

"label": "Track in collection",

"placeholder": "Track in collection",

"description": "",

"default": false,

"dataType": "boolean",

"inputType": "checkbox",

"editable": true,

"required": false,

"visible": true,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

},

"search": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "primaryCategory",

"dataType": "list",

"description": "Type",

"editable": true,

"default": \[],

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"inputType": "nestedselect",

"label": "Content Type(s)",

"name": "Type",

"placeholder": "Select ContentType",

"required": false,

"visible": true

},

{

"code": "board",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Board",

"label": "Board",

"required": false,

"name": "Board",

"inputType": "select",

"placeholder": "Select Board",

"output": "name"

},

{

"code": "medium",

"visible": true,

"depends": \[

"board"

],

"editable": true,

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Medium(s)",

"required": false,

"name": "Medium",

"inputType": "nestedselect",

"placeholder": "Select Medium",

"output": "name"

},

{

"code": "gradeLevel",

"visible": true,

"depends": \[

"board",

"medium"

],

"editable": true,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "Class",

"label": "Class(es)",

"required": false,

"name": "Class",

"inputType": "nestedselect",

"placeholder": "Select Class",

"output": "name"

},

{

"code": "subject",

"visible": true,

"depends": \[

"board",

"medium",

"gradeLevel"

],

"editable": true,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Subject(s)",

"required": false,

"name": "Subject",

"inputType": "nestedselect",

"placeholder": "Select Subject",

"output": "name"

},

{

"code": "topic",

"visible": true,

"editable": true,

"dataType": "list",

"depends": \[

"board",

"medium",

"gradeLevel",

"subject"

],

"default": "",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"name": "Topic",

"description": "Choose a Topics",

"inputType": "topicselector",

"label": "Topic(s)",

"placeholder": "Choose Topics",

"required": false

}

]

},

"unitMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "First Section",

"fields": \[

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": true,

"inputType": "text",

"label": "Title",

"name": "Title",

"placeholder": "Title",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": true,

"visible": true,

"validations": \[

{

"type": "max",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Title is required"

}

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": true,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": false,

"visible": true,

"validations": \[

{

"type": "max",

"value": "256",

"message": "Input is Exceeded"

}

]

},

{

"code": "keywords",

"visible": true,

"editable": true,

"dataType": "list",

"name": "Keywords",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"index": 3,

"description": "Keywords for the content",

"inputType": "keywords",

"label": "Keywords",

"placeholder": "Enter Keywords",

"required": false,

"validations": \[]

},

{

"code": "topic",

"visible": true,

"depends": \[],

"editable": true,

"dataType": "list",

"renderingHints": {},

"name": "Topic",

"description": "Choose a Topics",

"index": 11,

"inputType": "topicselector",

"label": "Topics",

"placeholder": "Choose Topics",

"required": false,

"validations": \[]

}

]

}

]

}

}

}

}

}

**Question Set:**

URL:\{{host\}}/api/object/category/definition/v1/update/obj-cat:practice-question-set\_questionset\_01269934121990553633

"objectCategoryDefinition"

{

"request": {

"channel": "01269934121990553633",

"name": "Practice Question Set",

"objectType": "QuestionSet",

"objectCategoryDefinition": {

"objectMetadata": {

"config": {

"sourcingSettings": {

"collection": {

"maxDepth": 1,

"addFromLibraryEnabled": **true**,

"enableAddFromLibrary": **true**,

"objectType": "QuestionSet",

"primaryCategory": "Practice Question Set",

"isRoot": **true**,

"iconClass": "fa fa-book",

"children": {},

"hierarchy": {

"level1": {

"name": "Section",

"type": "Unit",

"mimeType": "application/vnd.sunbird.questionset",

"primaryCategory": "Practice Question Set",

"iconClass": "fa fa-folder-o",

"children": {

"Question": \[

"Multiple Choice Question",

"Subjective Question"

]

}

}

}

}

}

},

"schema": {

"properties": {

"mimeType": {

"type": "string",

"enum": \[

"application/vnd.sunbird.questionset"

]

},

"verticals": {

"type": "string",

"enum": \[

"Nipun Bharat",

"Adult Education",

"Vocational Education",

"CWSN",

"Virtual Labs"

]

},

"board": {

"type": "string"

},

"farmingtype": {

"type": "string"

},

"cropcategory": {

"type": "array"

},

"croptype": {

"type": "array"

},

"cropname": {

"type": "array"

},

"cropvariety": {

"type": "array"

},

"audience": {

"type": "array"

}

}

}

},

"languageCode": \[],

"name": "Practice Question Set",

"forms": {

"childMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": **true**,

"inputType": "text",

"label": "Title",

"name": "Title",

"placeholder": "Title",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": **true**,

"visible": **true**,

"validations": \[

{

"type": "max",

"value": "100",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Title is required"

}

]

},

{

"code": "complexityLevel",

"dataType": "list",

"description": "Learning level",

"editable": **true**,

"inputType": "nestedselect",

"label": "Learning level",

"name": "Learning level",

"placeholder": "Select Learning level",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"required": **false**,

"visible": **true**,

"range": \[

"remember",

"understand",

"apply",

"analyse",

"evaluate",

"create"

],

"validations": \[]

},

{

"code": "board",

"name": "Framework",

"label": "Framework",

"placeholder": "Select Framework",

"description": "Framework of the Question Set",

"default": "",

"dataType": "text",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"depends": \[],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "Framework is required"

}

]

},

{

"code": "farmingtype",

"name": "Farming Type",

"label": "Farming Type",

"placeholder": "Select Farming Type",

"description": "farmingtype of the Question Set",

"default": "",

"dataType": "text",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"depends": \[],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "farmingtype is required"

}

]

},

{

"code": "cropcategory",

"name": "cropcategory",

"label": "Crop Category",

"placeholder": "Select Crop Category",

"description": " cropcategory of for the Question Set",

"default": "",

"dataType": "list",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"depends": \[

"farmingtype"

],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "cropcategory is required"

}

]

},

{

"code": "croptype",

"name": "croptype",

"label": "Crop Type",

"placeholder": "Select Croptype",

"description": "croptype of the Question Set",

"default": "",

"dataType": "list",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"depends": \[

"farmingtype",

"cropcategory"

],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "croptype is required"

}

]

},

{

"code": "cropname",

"name": "cropname",

"label": "Crop Name",

"placeholder": "Choose cropname",

"description": "Choose cropname covered in the Question Set",

"default": "",

"dataType": "list",

"inputType": "topicselector",

"editable": **true**,

"required": **false**,

"visible": **true**,

"depends": \[

"farmingtype",

"cropcategory",

"croptype",

"cropname"

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "maxScore",

"dataType": "number",

"description": "Marks",

"editable": **true**,

"inputType": "text",

"label": "Marks:",

"name": "Marks",

"placeholder": "Marks",

"tooltip": "Provide marks of this question.",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "pattern",

"value": "^\[1-9]{1}\[0-9]\*$",

"message": "Input should be numeric"

},

{

"type": "required",

"message": "Marks is required"

}

]

}

]

},

"create": {

"templateName": "",

"required": \[],

"properties": \[

{

"name": "Basic details",

"fields": \[

{

"code": "appIcon",

"name": "Icon",

"label": "Icon",

"placeholder": "Icon",

"description": "Icon for the question set",

"dataType": "text",

"inputType": "appIcon",

"editable": **true**,

"required": **true**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1 required"

}

},

{

"code": "name",

"name": "Name",

"label": "Name",

"placeholder": "Name",

"description": "Name of the QuestionSet",

"dataType": "text",

"inputType": "text",

"editable": **true**,

"required": **true**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "max",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Name is required"

}

]

},

{

"code": "description",

"name": "Description",

"label": "Description",

"placeholder": "Description",

"description": "Description of the content",

"dataType": "text",

"inputType": "textarea",

"editable": **true**,

"required": **true**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "description is required"

}

]

},

{

"code": "keywords",

"name": "Keywords",

"label": "keywords",

"placeholder": "Enter Keywords",

"description": "Keywords for the Question Set",

"dataType": "list",

"inputType": "keywords",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "instructions",

"name": "Instructions",

"label": "Instructions",

"placeholder": "Enter Instructions",

"description": "Instructions for the question set",

"dataType": "text",

"inputType": "richtext",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-2 required"

},

"validations": \[

{

"type": "maxLength",

"value": "500",

"message": "Input is Exceeded"

}

]

},

{

"code": "primaryCategory",

"name": "Type",

"label": "Type",

"placeholder": "",

"description": "Type or Category of the Question Set",

"dataType": "text",

"inputType": "text",

"editable": **false**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "additionalCategories",

"name": "Additional Category",

"label": "Additional Category",

"placeholder": "Select Additional Category",

"description": "Additonal Category of the Question Set",

"default": "",

"dataType": "list",

"inputType": "nestedselect",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

},

{

"name": "Framework details",

"fields": \[

{

"code": "board",

"name": "Board",

"label": "Board",

"placeholder": "Select Board",

"description": "Board",

"default": "",

"dataType": "text",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"depends": \[],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "Board is required"

}

]

},

{

"code": "farmingtype",

"name": "Farming Type",

"label": "Farming Type",

"placeholder": "Select Farming Type",

"description": "farmingtype of the Question Set",

"default": "",

"dataType": "text",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"depends": \[],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "farmingtype is required"

}

]

},

{

"code": "cropcategory",

"name": "cropcategory",

"label": "Crop Category",

"placeholder": "Select Crop Category",

"description": " cropcategory of for the Question Set",

"default": "",

"dataType": "list",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"depends": \[

"farmingtype"

],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "cropcategory is required"

}

]

},

{

"code": "croptype",

"name": "croptype",

"label": "Crop Type",

"placeholder": "Select Croptype",

"description": "croptype of the Question Set",

"default": "",

"dataType": "list",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"depends": \[

"farmingtype",

"cropcategory"

],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "croptype is required"

}

]

},

{

"code": "cropname",

"name": "cropname",

"label": "Crop Name",

"placeholder": "Choose Name",

"description": "Choose Name covered in the Question Set",

"default": "",

"dataType": "list",

"inputType": "topicselector",

"editable": **true**,

"required": **false**,

"visible": **true**,

"depends": \[

"farmingtype",

"cropcategory",

"croptype",

"board"

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "audience",

"name": "Audience",

"label": "Audience",

"placeholder": "Select Audience",

"description": "Audience of the Question Set",

"dataType": "list",

"inputType": "select",

"editable": **true**,

"required": **true**,

"visible": **true**,

"range": \[

"Other",

"Administrator"

],

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "Audience is required"

}

]

}

]

},

{

"name": "Question set behaviour",

"fields": \[

{

"code": "maxTime",

"name": "MaxTimer",

"label": "Set Maximum Time",

"placeholder": "HH:mm:ss",

"description": "This is the maximum time allowed for the users to complete the assessment",

"default": "3600",

"dataType": "text",

"inputType": "timer",

"editable": **true**,

"required": **true**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"validations": \[

{

"type": "time",

"message": "Please enter in hh:mm:ss",

"value": "HH:mm:ss"

},

{

"type": "max",

"value": "05:59:59",

"message": "max time should be less than 05:59:59"

}

]

},

{

"code": "showTimer",

"name": "show Timer",

"label": "show Timer",

"placeholder": "show Timer",

"description": "show Timer",

"default": **false**,

"dataType": "boolean",

"inputType": "checkbox",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "requiresSubmit",

"name": "Submit Confirmation",

"label": "Submit Confirmation Page",

"placeholder": "Select Submit Confirmation",

"description": "Allows users to review and submit the assessment",

"dataType": "text",

"inputType": "select",

"output": "identifier",

"range": \[

{

"identifier": "Yes",

"label": "Enable"

},

{

"identifier": "No",

"label": "Disable"

}

],

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "summaryType",

"name": "summaryType",

"label": "Summary Type",

"placeholder": "Select Summary Type",

"description": "summaryType",

"dataType": "text",

"inputType": "select",

"editable": **true**,

"required": **false**,

"visible": **true**,

"range": \[

"Complete",

"Score",

"Duration",

"Score & Duration"

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

},

{

"name": "Question set behaviour",

"fields": \[

{

"code": "author",

"name": "Author",

"label": "Author",

"placeholder": "Author",

"description": "Author of the question set",

"dataType": "text",

"inputType": "text",

"editable": **true**,

"required": **true**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"validations": \[

{

"type": "required",

"message": "Author is required"

}

]

},

{

"code": "copyright",

"name": "Copyright & year",

"label": "Copyright & year",

"placeholder": "Copyright & year",

"description": "Copyright & year",

"dataType": "text",

"inputType": "text",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "license",

"name": "license",

"label": "license",

"placeholder": "Select license",

"description": "license",

"dataType": "text",

"inputType": "select",

"editable": **true**,

"required": **false**,

"visible": **true**,

"range": "",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

}

]

},

"publishchecklist": {

"templateName": "",

"required": \[],

"properties": \[]

},

"search": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "primaryCategory",

"dataType": "list",

"description": "Type",

"editable": **true**,

"default": \[],

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"inputType": "nestedselect",

"label": "Question Type(s)",

"name": "Type",

"placeholder": "Select QuestionType",

"required": **false**,

"visible": **true**

},

{

"code": "farmingtype",

"visible": **true**,

"depends": \[],

"editable": **true**,

"dataType": "list",

"description": "farmingtype",

"label": "farmingtype",

"required": **false**,

"name": "farmingtype",

"inputType": "select",

"placeholder": "Select farmingtype",

"output": "name",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "cropcategory",

"visible": **true**,

"editable": **true**,

"dataType": "list",

"description": "",

"label": "Crop Category(s)",

"required": **false**,

"name": "cropcategory",

"inputType": "nestedselect",

"placeholder": "Select cropcategory",

"output": "name",

"depends": \[

"farmingtype"

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "croptype",

"visible": **true**,

"depends": \[

"farmingtype",

"cropcategory"

],

"editable": **true**,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "croptype",

"label": "Crop Type(s)",

"required": **false**,

"name": "croptype",

"inputType": "nestedselect",

"placeholder": "Select croptype",

"output": "name"

},

{

"code": "cropname",

"visible": **true**,

"depends": \[

"farmingtype",

"cropcategory",

"croptype"

],

"editable": **true**,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Crop Name(s)",

"required": **false**,

"name": "cropname",

"inputType": "nestedselect",

"placeholder": "Select cropname",

"output": "name"

},

{

"code": "cropvariety",

"visible": **true**,

"editable": **true**,

"dataType": "list",

"depends": \[

"farmingtype",

"cropcategory",

"croptype",

"cropname"

],

"default": "",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"name": "cropvariety",

"description": "Choose a Chapters",

"inputType": "topicselector",

"label": "cropvariety(s)",

"placeholder": "Choose cropvariety",

"required": **false**

}

]

},

"searchConfig": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "primaryCategory",

"dataType": "list",

"description": "Type",

"editable": **true**,

"default": \[],

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"inputType": "nestedselect",

"label": "Question Type(s)",

"name": "Type",

"placeholder": "Select QuestionType",

"required": **false**,

"visible": **true**

},

{

"code": "farmingtype",

"visible": **true**,

"depends": \[],

"editable": **true**,

"dataType": "list",

"description": "farmingtype",

"label": "farmingtype",

"required": **false**,

"name": "farmingtype",

"inputType": "select",

"placeholder": "Select farmingtype",

"output": "name",

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "cropcategory",

"visible": **true**,

"editable": **true**,

"dataType": "list",

"description": "",

"label": "Crop Category(s)",

"required": **false**,

"name": "cropcategory",

"inputType": "nestedselect",

"placeholder": "Select cropcategory",

"output": "name",

"depends": \[

"farmingtype"

],

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "croptype",

"visible": **true**,

"depends": \[

"farmingtype",

"cropcategory"

],

"editable": **true**,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "croptype",

"label": "Crop Type(s)",

"required": **false**,

"name": "croptype",

"inputType": "nestedselect",

"placeholder": "Select croptype",

"output": "name"

},

{

"code": "cropname",

"visible": **true**,

"depends": \[

"farmingtype",

"cropcategory",

"croptype"

],

"editable": **true**,

"default": "",

"dataType": "list",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"description": "",

"label": "Crop Name(s)",

"required": **false**,

"name": "cropname",

"inputType": "nestedselect",

"placeholder": "Select cropname",

"output": "name"

},

{

"code": "cropvariety",

"visible": **true**,

"editable": **true**,

"dataType": "list",

"depends": \[

"farmingtype",

"cropcategory",

"croptype",

"cropname"

],

"default": "",

"renderingHints": {

"class": "sb-g-col-lg-1"

},

"name": "cropvariety",

"description": "Choose a Chapters",

"inputType": "topicselector",

"label": "cropvariety(s)",

"placeholder": "Choose cropvariety",

"required": **false**

}

]

},

"unitMetadata": {

"templateName": "",

"required": \[],

"properties": \[

{

"code": "name",

"dataType": "text",

"description": "Name of the content",

"editable": **true**,

"inputType": "text",

"label": "Title",

"name": "Title",

"placeholder": "Title",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": **true**,

"visible": **true**,

"validations": \[

{

"type": "max",

"value": "120",

"message": "Input is Exceeded"

},

{

"type": "required",

"message": "Title is required"

}

]

},

{

"code": "description",

"dataType": "text",

"description": "Description of the content",

"editable": **true**,

"inputType": "textarea",

"label": "Description",

"name": "Description",

"placeholder": "Description",

"renderingHints": {

"class": "sb-g-col-lg-1 required"

},

"required": **true**,

"visible": **true**,

"validations": \[

{

"type": "max",

"value": "500",

"message": "Input is Exceeded"

}

]

},

{

"code": "instructions",

"name": "Instructions",

"label": "Instructions",

"placeholder": "Enter Instructions",

"description": "Instructions for the section",

"dataType": "text",

"inputType": "richtext",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-2"

},

"validations": \[

{

"type": "maxLength",

"value": "500",

"message": "Input is Exceeded"

}

]

},

{

"code": "maxQuestions",

"name": "Show Questions",

"label": "Count of questions to be displayed in this section",

"placeholder": "Input count of questions to be displayed",

"description": "By default all questions are shown unless specific count is entered.",

"default": "",

"dataType": "number",

"inputType": "select",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "shuffle",

"name": "Shuffle Questions",

"label": "Shuffle Questions",

"placeholder": "Shuffle Questions",

"description": "If shuffle questions is selected, users are presented with questions in a random order whenever they attempt the assessment",

"default": "false",

"dataType": "boolean",

"inputType": "checkbox",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "showFeedback",

"name": "Show Feedback",

"label": "Show Question Feedback",

"placeholder": "Select Option",

"description": "If feedback is selected, users are informed whether they have correctly answered question or not",

"dataType": "boolean",

"inputType": "checkbox",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

},

{

"code": "showSolutions",

"name": "Show Solution",

"label": "Show Solution",

"placeholder": "Select Option",

"description": "If show solution is selected then solutions for each question will be shown to the user",

"dataType": "boolean",

"inputType": "checkbox",

"editable": **true**,

"required": **false**,

"visible": **true**,

"renderingHints": {

"class": "sb-g-col-lg-1"

}

}

]

}

}

}

}

}

**MCQ Question:**

**Filter configuration in the buckets in workspace: This configuration enables user to update the filter in all the buckets in workspace with the framework details**

**Form:**

**type: "content"**

**action: "search"**

**subType: "draft" (depends on which bucket user is configuring, this can be “All my content”, “published” etc)**

**Steps:**

1.Open the portal, login with book creator / content creator credentials

2.Open the network tab

3.Open workspace -> select any bucket which has filters (“all my content”, “drafts” etc)

4.Take the read form call with below payload

1. {request: {type: "content", action: "search", subType: "draft", rootOrgId: "01269878797503692810",…\}}
   1. request: {type: "content", action: "search", subType: "draft", rootOrgId: "01269878797503692810",…}

1\. action: "search"

2\. framework: "tn\_k-12\_5"

3\. rootOrgId: "01269878797503692810"

4\. subType: "draft"

5\. type: "content"

5.Copy the curl and import it to postman and read the form

6.copy the “data” field from response and copy it in the request body and update the read word in the API end point and update to “update”

7.Update the the request body with below data

"data": {

"templateName": "defaultTemplate",

"action": "search",

"fields": \[

{

"code": "primaryCategory",

"dataType": "text",

"name": "Content Type",

"label": "Content Type",

"description": "Content Type",

"editable": true,

"inputType": "select",

"required": false,

"displayProperty": "Editable",

"visible": true,

"range": \[

{

"name": "Course"

},

{

"name": "Digital Textbook"

},

{

"name": "Content Playlist"

},

{

"name": "Explanation Content"

},

{

"name": "Learning Resource"

},

{

"name": "Practice Question Set"

},

{

"name": "eTextbook"

},

{

"name": "Teacher Resource"

}

],

"renderingHints": {

"semanticColumnWidth": "four"

},

"index": 5

},

{

"code": "farmingtype",

"visible": true,

"editable": true,

"displayProperty": "Editable",

"dataType": "text",

"renderingHints": {

"semanticColumnWidth": "four"

},

"name": "farmingtype",

"description": "farmingtype",

"index": 1,

"inputType": "select",

"label": "Farming Type",

"tooltip": "farmingtype",

"required": false

},

{

"code": "croptype",

"visible": true,

"editable": true,

"displayProperty": "Editable",

"dataType": "text",

"renderingHints": {

"semanticColumnWidth": "four"

},

"name": "croptype",

"description": "croptype",

"index": 3,

"inputType": "select",

"label": "Crop Type",

"required": false

},

{

"code": "cropcategory",

"visible": true,

"editable": true,

"displayProperty": "Editable",

"dataType": "text",

"renderingHints": {

"semanticColumnWidth": "four"

},

"name": "cropcategory",

"description": "Crop category",

"index": 2,

"inputType": "select",

"label": "Crop Category",

"required": false

},

{

"code": "cropname",

"visible": true,

"editable": true,

"displayProperty": "Editable",

"dataType": "text",

"renderingHints": {

"semanticColumnWidth": "four"

},

"name": "cropname",

"description": "Name of the crops",

"index": 4,

"inputType": "select",

"label": "Crop Name",

"required": false

}

]

}

Note: Request body “data” field is same for the filters across all the buckets on workspace with difference in the type and subtype
