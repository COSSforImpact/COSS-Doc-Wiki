---
icon: elementor
---

# Enable transcripts for video content

## Introduction <a href="#enabletranscriptsforvideocontent-introduction" id="enabletranscriptsforvideocontent-introduction"></a>

This wiki explains the design and implementation of the enable transcriptions for video content.

[https://project-sunbird.atlassian.net/browse/SB-26446](https://project-sunbird.atlassian.net/browse/SB-26446)

#### Key Design Problems: <a href="#enabletranscriptsforvideocontent-keydesignproblems" id="enabletranscriptsforvideocontent-keydesignproblems"></a>

1. How to store **transcripts** files in the system.
2. Support **configuration** for transcript file types.
3. Relation between **transcripts** files & **content**.

### **Solution:** <a href="#enabletranscriptsforvideocontent-solution" id="enabletranscriptsforvideocontent-solution"></a>

* We want to create transcript files as **assets** in our system. For that, we want to create a new asset primaryCategory with mime-types which are supported to create transcript files.

primary category: **Video Transcript**

tragetObjectType: **Asset**

mimeType Supported: `application/x-subrip`

Currently, we are supporting only a **single mimeType**. in future, if we want to support multiple mimeType just need to update the primary category definition.

```
{
  "objectCategoryDefinition": {
    "categoryId": "obj-cat:video-transcript",
    "targetObjectType": "Asset",
    "objectMetadata": {
      "config": {},
      "schema": {
        "properties": {
          "mimeType": {
            "type": "string",
            "enum": [
              "application/x-subrip"
            ],
            "default": "application/x-subrip"
          }
        }
      }
    }
  }
}
```

* We are introducing new metadata property **transcripts** in the content object. this property will have a list of `transcripts` files uploaded by users for specific content.

**Schema changes:**

```
{
  "transcripts": {
    "type": "array",
    "items": {
      "type": "object"
    }
  }
}
```

**Sample:** List of transcripts files uploaded by users for specific content

```
{
    "result": {
        "content": {
            "identifier": "do_12345678",
            "name": "Video Content",
            "author": "N118",,
            "transcripts": [
                {
                    "language": "English",
                    "languageCode": "en",
                    "identifier": "do_1234",
                    "artifactUrl": "https://dockstorage.blob.core.windows.net/sunbird-content-dock/content/do_11340589048704204811789/artifact/do_11340589048704204811789_1636461247932_sample.srt"
                },
                {
                    "language": "Hindi",
                    "languageCode": "hi",
                    "identifier": "do_5678",
                    "artifactUrl": "https://dockstorage.blob.core.windows.net/sunbird-content-dock/content/do_11340589048704204811789/artifact/do_11340589048704204811789_1636461247932_sample.srt"
                },
            ]
        }
    }
}
```

* We are **not maintaining any relations** between content & transcripts(assets). we are adding a list of transcripts as metadata to the content.
* Transcripts property we are **indexing into elastic search** as an object. So it will be easy to filter contents based on transcripts `language` & `identifier`
