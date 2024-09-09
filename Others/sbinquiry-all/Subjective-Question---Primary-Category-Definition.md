Curl command to update Primary Category Definition


```
curl -L -X PATCH '{{host}}/object/category/definition/v4/update/obj-cat:subjective-question_question_all' \
-H 'Content-Type: application/json' \
--data-raw '{
  "request": {
    
  }
}'

```
Pass the below body into the request in the above curl command


```
{
  "request": {
    "objectCategoryDefinition": {
      "objectMetadata": {
        "config": {},
        "schema": {
          "properties": {
            "mimeType": {
              "type": "string",
              "enum": [
                "application/vnd.sunbird.question"
              ]
            }
          }
        }
      }
    }
  }
}
```




*****

[[category.storage-team]] 
[[category.confluence]] 
