---
icon: elementor
---

# Restricting Metadata as per Definition

#### **Overview** <a href="#restrictingmetadataasperdefinition-overview" id="restrictingmetadataasperdefinition-overview"></a>

The metadata properties/relations created or updated are validated with their respective definition schema. Any property which is not part of the definition has to be restricted.

\


#### **Problem Statement** <a href="#restrictingmetadataasperdefinition-problemstatement" id="restrictingmetadataasperdefinition-problemstatement"></a>

As per the current implementation, properties which are part of the definition are validated for their schema. But those properties which are not present in definition, are getting updated as is.

Because of this, there are redundant metadata, metadata with incorrect names or incorrect data/dataType. This also affects the number of fields increasing in elastic search indices.

Thus, by restricting the metadata properties to those defined in definition, solves the data inconsistency during create and update.

\


#### **Implementation Design** <a href="#restrictingmetadataasperdefinition-implementationdesign" id="restrictingmetadataasperdefinition-implementationdesign"></a>

**Option 1:**

Restricting the metadata as per the definition is as follows:

**Changes in Graph engine :**&#x20;

* `node.metadata.filter` : Is a configuration, if **`true`** graph engine restricts the properties to the ones defined in metadata, else restriction is not applied. This configuration is defaulted to `false`.
*   if restriction is applied, and the metadata getting updated is not part of the definition, a CLIENT ERROR(400 - BAD REQUEST) is sent as API response. Below is a response body.

    ```
    {
        "id": "ekstep.learning.content.create",
        "ver": "3.0",
        "ts": "2018-11-23T14:38:23Z+05:30",
        "params": {
            "resmsgid": "",
            "msgid": null,
            "err": "ERR_GRAPH_ADD_NODE_VALIDATION_FAILED",
            "status": "failed",
            "errmsg": "Validation Errors"
        },
        "responseCode": "CLIENT_ERROR",
        "result": {
            "messages": [
                "Invalid Property : <Property_Name 1>",
                "Invalid Property : <Property_Name 2>",
                ...
            ]
        }
    } 
    ```

**APIs for partial definition update :**

New APIs to partially update the definition with new properties/relations.

**PATCH - /taxonomy/{graph\_id}/definition/update/{object\_type}**

**Request :**

```
{
    "request": {
        "definition" : {
            "properties" : [
                    {
                    "propertyName": "{property_name}",
                    "title": "{title}",
                    "description": "{description}",
                    "category": "{category - General/External}",
                    "dataType": "{data_type}",
                    "required": {mandatory - true/false},
                    "displayProperty": "Editable",
                    "defaultValue": "",
                    "renderingHints": "{hints}",
                    "indexed": {indexed - true/false}
                }
            ],
            "inRelations" : [
                {
                    "relationName": "{relation_name}",
                    "objectTypes": [
                        "{object_type}"
                    ],
                    "title": "{relation_title}",
                    "description": "{description}",
                    "required": {mandatory - true/false}
                }
            ],
            "outRelations" : [
                {
                        "relationName": "{relation_name}",
                    "objectTypes": [
                        "{object_type}"
                    ],
                    "title": "{relation_title}",
                    "description": "{description}",
                    "required": {mandatory - true/false}
                }
            ]
        }
    }
}
```

\


**Response: OK (200)**

```
{
    "id": "ekstep.definition.update",
    "ver": "1.0",
    "ts": "2018-11-23T15:14:24Z+05:30",
    "params": {
        "resmsgid": "b26ab632-9c4f-4c3d-86b2-a5bc95863397",
        "msgid": null,
        "err": null,
        "status": "successful",
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {}
}
```

\


If a relation/property which is already present in definition is updated, client error is sent as response.

**Response: ERROR (400 - Bad Request)**

```
{
    "id": "ekstep.definition.update",
    "ver": "1.0",
    "ts": "2018-11-23T11:48:00Z+05:30",
    "params": {
        "resmsgid": "cf96060b-ba62-430b-8856-66707345ae66",
        "msgid": null,
        "err": "ERR_GRAPH_SAVE_DEF_NODE_VALIDATION_FAILED",
        "status": "failed",
        "errmsg": "Definition nodes validation error"
    },
    "responseCode": "CLIENT_ERROR",
    "result": {
        "messages": {
            "DEFINITION_NODE_Content": [
                "Duplicate Relation Definition: hasSequenceMember, with object type: Content"
            ]
        }
    }
}
```

\


\


#### Conclusion <a href="#restrictingmetadataasperdefinition-conclusion" id="restrictingmetadataasperdefinition-conclusion"></a>
