---
icon: elementor
---

# How to define the schema and context for a DIAL?

### How to define the schema and context? <a href="#howtodefinetheschemaandcontextforadial-howtodefinetheschemaandcontext" id="howtodefinetheschemaandcontextforadial-howtodefinetheschemaandcontext"></a>

* There are two ways to define and upload the schema in blob.
  1. Fork [sunbird-dial-service](https://github.com/project-sunbird/sunbird-dial-service/schemas) repo
  2. Create the your own repo and follow the same structure of schemas folder as in sunbird-dial-service repo.

#### Steps: <a href="#howtodefinetheschemaandcontextforadial-steps" id="howtodefinetheschemaandcontextforadial-steps"></a>

1. Create the new folder inside _**schemas**_ folder with the _**context-name.**_ e.g. we have the context name content and collection.
2.  Create the file _**context.json**_ and _**schema.json**_ inside context folder.



    \
    **Sample schema.json**

    ```
    {
      "$id": "file:./schemas/<context_name>/schema.json",
      "$schema": "http://json-schema.org/draft-07/schema#",
      "title": "<context_name>",
      "type": "object",
      "properties": {
        "<attribute_1>" : {
          "type": "string"
        },
        "<attribute_2>" : {
          "type": "array"
        },
        "<attribute_3>" : {
          "type": "array"
        },
        "<attribute_4>" : {
          "type": "string"
        }
      }
    }
    ```

    **Sample context.json**

    ```
    {
      "@context": {
        "schema": "http://schema.org/",
        "<attribute_1>": {
          "@id": "schema:name#<attribute_1>",
          "@type": "schema:name"
        },
        "<attribute_4>": {
          "@id": "schema:name#<attribute_1>",
          "@type": "schema:name"
        },
        "<attribute_2>": {
          "@id": "schema:name#<attribute_2>",
          "@type": "@id",
          "@container": "@list"
        },
        "<attribute_3>": {
          "@id": "schema:name#<attribute_3>",
          "@type": "@id",
          "@container": "@list"
        }
      }
    }
    ```
3.  Upload schema and context in blob storage using jenkins job\
    _Deploy/Kubernetes/DialUploadSchemas_ - Configure the _**schemas**_ folder path in jenkins job to upload all the available schema and context to blob storage.\
    \
    Configure the _**dial\_plugin\_container\_name**_ in devops private repo. e.g.

    ```
    dial_plugin_container_name: "sunbird-dial-dev"
    ```

\
Configure the _**dial\_service\_schema\_base\_path**_ in devops private repo. e.g.

```
dial_service_schema_base_path: "https://{{sunbird_public_storage_account_name}}.blob.core.windows.net/{{dial_plugin_container_name}}/schemas/local"
```

1.  Verify the uploaded schema/context by accessing the following URL format

    ```
    <dial_service_schema_base_path>/<context_name>/schema.json
    <dial_service_schema_base_path>/<context_name>/context.json
    ```

    e.g. for collection

    ```
    https://sunbirddev.blob.core.windows.net/sunbird-dial-dev/schemas/local/collection/schema.json
    https://sunbirddev.blob.core.windows.net/sunbird-dial-dev/schemas/local/collection/context.json
    ```
2.  Set the schema path in **sunbird-dial-service** _application.config_ with the blob storage path and do the dial-service deployment.

    ```
    schema {
        basePath = "<dial_service_schema_base_path>"
    }
    ```

e.g.

```
schema {
    basePath = "https://sunbirddev.blob.core.windows.net/sunbird-dial-dev/schemas/local"
}
```

### **DIAL update API** <a href="#howtodefinetheschemaandcontextforadial-dialupdateapi" id="howtodefinetheschemaandcontextforadial-dialupdateapi"></a>

```
curl --location --request PATCH 'https://dev.sunbirded.org/api/dialcode/v2/update/5NZRAM' \
--header 'X-Channel-Id: channelTest' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{api_key}}' \
--data-raw '{
  "request": {
      "dialcode": {
        "contextInfo": {
          "type": "collection",
          "board": "CBSE",
          "medium": ["English"],
          "gradeLevel": ["Class 2"],
          "subject": ["Mathematics"]
        }
      }
  }
}'
```

\
**Request: Sample request with context**

```
Sample request:
{
  "request": {
    "dialcode": {
      "contextInfo": {
          "type": "<context_name>",
          "<attribute_1>": "<value>",
          "<attribute_2>": ["<value>"],
          "<attribute_3>": ["<value>"],
          "<attribute_4>": "<value>"
      }
    }
  }
}
```

### **DIAL read API** <a href="#howtodefinetheschemaandcontextforadial-dialreadapi" id="howtodefinetheschemaandcontextforadial-dialreadapi"></a>

```
curl --location --request POST 'https://dev.sunbirded.org/api/dialcode/v2/read' --header 'X-Channel-ID: in.ekstep' --header 'Content-Type: application/json' --data-raw '{"request": {"dialcode": {"identifier": "R4C1M2"}}}'
```

**Response:**

```
{
  "dialcode": {
    "@context": "https://sunbirddev.blob.core.windows.net/sunbird-dial-dev/schemas/local/dialcode/context.json",
    "@id": "https://dev.sunbirded.org/dial/<DIALCode>",
    "@type": "https://dev.sunbirded.org/ns/DIAL",
    "identifier": "<DIALCode>",
    "generatedOn": "2022-03-10T14:20:39.870+0530",
    "publisher": null,
    "status": "Draft",
    "batchCode": null,
    "channel": "testchannel",
    "publishedOn": null,
    "contextInfo": [{
      "@context": "https://sunbirddev.blob.core.windows.net/sunbird-dial-dev/schemas/local/<content_name>/context.json",
      "@type": "https://dev.sunbirded.org/ns/<content_name>",
      "<attribute_1>": "<some_value>",
      "<attribute_2>": ["<some_value>"],
      "<attribute_3>": ["<some_value>"],
      "<attribute_4>": "<some_value>"
    }]
  }
}

e.g.
{
  "dialcode": {
    "@context": "https://sunbirddev.blob.core.windows.net/sunbird-dial-dev/schemas/local/dialcode/context.json",
    "@id": "https://dev.sunbirded.org/dial/R4C1M2",
    "@type": "https://dev.sunbirded.org/ns/DIAL",
    "identifier": "R4C1M2",
    "generatedOn": "2022-03-10T14:20:39.870+0530",
    "publisher": null,
    "status": "Draft",
    "batchCode": null,
    "channel": "testchannel",
    "publishedOn": null,
    "contextInfo": [{
      "@context": "https://sunbirddev.blob.core.windows.net/sunbird-dial-dev/schemas/local/collection/context.json",
      "@type": "https://dev.sunbirded.org/ns/Collection",
      "medium": ["English"],
      "gradeLevel": ["Class 2"],
      "subject": ["Mathematics"],
      "board": "CBSE"
    }]
  }
}
```
