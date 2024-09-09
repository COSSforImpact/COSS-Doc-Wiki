
```
curl --location --request POST '<BASE_URL>/api/object/category/v1/create' \
--header 'Authorization: Bearer <AUTH_TOKEN>' \
--header 'Content-Type: application/json' \
--header 'x-authenticated-user-token: <USER_TOKEN>' \
--data-raw '{
    "request": {
        "objectCategory": {
            "name": "Text",
            "description":"Text"
        }
    }
}'
```
CATEGORY_ID is the response of the created API


```
curl --location --request POST '<BASE_URL>/api/object/category/definition/v1/create' \
--header 'Authorization: Bearer <AUTH_TOKEN>' \
--header 'Content-Type: application/json' \
--header 'x-authenticated-user-token: <USER_TOKEN>' \
--data-raw '{
  "request": {
    "objectCategoryDefinition": {
      "categoryId": "<CATEGORY_ID>",
      "targetObjectType": "Question",
      "objectMetadata": {
        "config": {
          "enforceCorrectAnswer": false,
          "showSolution": false,
          "showAddHints": true,
          "showAddScore": false,
          "showAddTips": true,
          "showAddTranslation": true,
          "showAddSecondaryQuestion": false
        },
        "schema": {
          "properties": {
            "interactionTypes": {
              "type": "array",
              "items": {
                "type": "string",
                "enum": [
                  "text"
                ]
              }
            },
            "mimeType": {
              "type": "string",
              "enum": [
                "application/vnd.sunbird.question"
              ]
            }
          }
        }
      },
      "languageCode": [],
      "forms": {
        "create": {
          "required": [],
          "templateName": "",
          "properties": [
            {
              "code": "name",
              "dataType": "text",
              "description": "Name of the content",
              "showInfo": true,
              "editable": true,
              "inputType": "text",
              "label": "Title",
              "name": "Title",
              "placeholder": "Title",
              "renderingHints": {
                "class": "sb-g-col-lg-2 required"
              },
              "required": true,
              "visible": true,
              "validations": [
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
              "code": "numberOnly",
              "name": "numberOnly",
              "label": "Number Only",
              "placeholder": "Number Only",
              "description": "If this validation is selected the user would only be able to input a number response for the text type questions.",
              "default": "Yes",
              "dataType": "text",
              "inputType": "checkbox",
              "showInfo": true,
              "editable": true,
              "required": false,
              "visible": true,
              "renderingHints": {
                "class": "sb-g-col-lg-1"
              }
            },
            {
              "code": "characterLimit",
              "dataType": "number",
              "description": "The character limit can be set to limit the characters that the user can enter in the response for the text question",
              "showInfo": true,
              "editable": true,
              "inputType": "text",
              "label": "Character Limit",
              "name": "characterLimit",
              "placeholder": "Add limit",
              "renderingHints": {
                "class": "sb-g-col-lg-1 required"
              },
              "required": true,
              "visible": true,
              "validations": [
                {
                  "type": "required",
                  "message": "Character limit is required"
                }
              ]
            },
            {
              "code": "showEvidence",
              "dataType": "text",
              "description": "Allow Evidence",
              "showInfo": true,
              "editable": true,
              "index": 5,
              "inputType": "checkbox",
              "label": "Allow Evidence",
              "name": "showEvidence",
              "placeholder": "showEvidence",
              "renderingHints": {
                "class": "sb-g-col-lg-1"
              },
              "required": false,
              "visible": true
            },
            {
              "code": "evidenceMimeType",
              "dataType": "list",
              "depends": [
                "showEvidence"
              ],
              "description": "Evidence",
              "showInfo": true,
              "editable": true,
              "inputType": "multiselect",
              "label": "evidence",
              "name": "evidenceMimeType",
              "placeholder": "evidence",
              "renderingHints": {
                "class": "sb-g-col-lg-1"
              },
              "required": false,
              "visible": true,
              "range": [
                {
                  "value": "image",
                  "label": "image"
                },
                {
                  "value": "audio",
                  "label": "audio"
                },
                {
                  "value": "video",
                  "label": "video"
                },
                {
                  "value": "document",
                  "label": "document"
                }
              ]
            },
            {
              "code": "showRemarks",
              "dataType": "text",
              "description": "Allow Remarks",
              "showInfo": true,
              "editable": true,
              "index": 5,
              "inputType": "checkbox",
              "label": "Allow Remarks",
              "name": "showRemarks",
              "placeholder": "showRemarks",
              "renderingHints": {
                "class": "sb-g-col-lg-1"
              },
              "required": false,
              "visible": true
            },
            {
              "code": "remarksLimit",
              "dataType": "number",
              "description": "The limit for the remark can be set to limit the maximum number of characters a user can add in the remark field for the question.",
              "depends": [
                "showRemarks"
              ],
              "showInfo": true,
              "editable": true,
              "inputType": "text",
              "label": "Remark limit",
              "name": "remarksLimit",
              "placeholder": "Add limit",
              "renderingHints": {
                "class": "sb-g-col-lg-1"
              },
              "required": false,
              "visible": true
            },
            {
              "code": "markAsNotMandatory",
              "dataType": "text",
              "description": "markAsNotMandatory",
              "showInfo": true,
              "editable": true,
              "index": 5,
              "inputType": "checkbox",
              "label": "Mark As Not Mandatory",
              "name": "markAsNotMandatory",
              "placeholder": "markAsNotMandatory",
              "renderingHints": {
                "class": "sb-g-col-lg-1"
              },
              "required": false,
              "visible": true
            }
          ]
        }
      }
    }
  }
}'
```


*****

[[category.storage-team]] 
[[category.confluence]] 
