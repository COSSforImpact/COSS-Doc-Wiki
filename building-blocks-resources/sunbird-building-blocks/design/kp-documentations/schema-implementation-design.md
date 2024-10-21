---
icon: elementor
---

# Schema Implementation Design

### Problem Definition: <a href="#schemaimplementationdesign-problemdefinition" id="schemaimplementationdesign-problemdefinition"></a>

As part of Knowledge Platform 2.0, definition schema should give provision of implementing version support in future.

### Design: <a href="#schemaimplementationdesign-design" id="schemaimplementationdesign-design"></a>

\


\




### Definition Data Model: <a href="#schemaimplementationdesign-definitiondatamodel" id="schemaimplementationdesign-definitiondatamodel"></a>

* IL\_UNIQUE\_ID - DEFINITION\_NODE\_Content
* description - Schema definition object for Content
* status - Draft/Live
* createdOn - Date
* lastUpdatedOn - Date
* IL\_SYS\_NODE\_TYPE - DEFINITION\_NODE
* IL\_FUNC\_OBJECT\_TYPE - Content
* version - 1.0
* artifactUrl - Draft version URL link
* downloadUrl - Published version URL link

\


### Schema API Request Response: <a href="#schemaimplementationdesign-schemaapirequestresponse" id="schemaimplementationdesign-schemaapirequestresponse"></a>

**Schema Create API:**

* It will always expect object Type in request
* If there is no entry for IL\_SYS\_NODE\_TYPE: DEFINITION\_NODE and IL\_FUNC\_OBJECT\_TYPE: Content:\

  * It will create Content definition object with version 1.0
  * Identifier will be DEFINITION\_NODE\_Content
* If object present - will throw Client Error.
* Apart from objectType (IL\_FUNC\_OBJECT\_TYPE), no other field is expected.

```
{
	"request": {
		"schema": {
			"objectType": "Content"
		}
	}
}
```

\


**Schema Update API:**

* No other field apart from description can be updated.

```
{
	"request": {
		"schema": {
			"description": "Schema definition object for Content",
		}
	}
}
```

\


**Schema Upload API:**

* Zipped file containing 'schema.josn' and 'config.json' will be uploaded.
* If object status is Live:\

  * Upload and extract the zipped file in path schemas/content/snapshot.
  * It will create replica of published definition.
  * Identifier will be 'DEFINITION\_NODE\_Content.img'
  * VersionKey will be same of version key.
  * Status will be Draft
  * artifactUrl will be link of snapshot path link.
* If object status is Draft:\

  * Upload and extract the zipped file in path schemas/content/snapshot.

**Schema Publish API:**

* It will copy the snapshot files to the directory named 'schemas/content/1.0'
* DownloadUrl will be updated with new url.
* Status will be Live.

```
{
	"request": {
		"schema": {}
	}
}
```

\


\


\


\
