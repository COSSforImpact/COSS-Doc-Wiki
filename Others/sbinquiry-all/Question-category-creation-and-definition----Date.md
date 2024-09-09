
```
curl --location --request POST '<BASE_URL>/api/object/category/v1/create' \
--header 'Authorization: Bearer <AUTH_TOKEN>' \
--header 'Content-Type: application/json' \
--header 'x-authenticated-user-token: <USER_TOKEN>' \
--data-raw '{
    "request": {
        "objectCategory": {
            "name": "Date",
            "description":"Date"
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
                  "date"
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
                "class": "sb-g-col-lg-1 required"
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
              "code": "dateFormat",
              "dataType": "text",
              "description": "Select format",
              "showInfo": true,
              "editable": true,
              "index": 5,
              "inputType": "select",
              "label": "Select format",
              "name": "dateFormat",
              "placeholder": "Select format",
              "renderingHints": {
                "class": "sb-g-col-lg-1 required"
              },
              "required": true,
              "visible": true,
              "range": [
                "DD/MM/YYYY",
                "YYYY/MM/DD",
                "MMM, YYYY",
                "DD MMM, YYYY"
              ],
              "validations": [
                {
                  "type": "required",
                  "message": "Format is required"
                }
              ]
            },
            {
              "code": "autoCapture",
              "dataType": "text",
              "description": "If auto capture is selected, the user would get a button to directly capture (input) the current date or the date of that day.",
              "showInfo": true,
              "editable": true,
              "index": 5,
              "inputType": "checkbox",
              "label": "Auto capture",
              "name": "autoCapture",
              "placeholder": "Auto capture",
              "renderingHints": {
                "class": "sb-g-col-lg-1"
              },
              "range": [
                "Yes",
                "No"
              ],
              "required": true,
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
