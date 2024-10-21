---
icon: elementor
---

# ETB 2.0 - Upload TOC, Update TOC & Download TOC using CSV

**Overview :**

Textbook Creator can upload a pre-defined formatted csv file with details of TOC hierarchy against a Textbook id. System should:

* Generate the TOC hierarchy using csv file.
* Download complete textbook hierarchy in csv format.
* Update TOC unit metadata using downloaded file with property update.

\


**Problem Statement:**

&#x20;                  Process of creation of Textbook ToC (Table of Content) through portal is time consuming, requires training and continuous internet connectivity. ToCs are in tree like structures hence one chapter can have multiple sections and those sections can have multiple subsections. To simplify the process it requires a way where user can upload a csv file with input data and ToC can be created in one go after validation.

[Sample CSV data.](https://docs.google.com/spreadsheets/d/1oft6OHg5izonTqJ1CrcyqTltZ7b-L3QGGT-jE1sUjtY/)

There will be an API which will create and update the TOC hierarchy through csv upload, which will accept a csv file, validate the data, generate the TOC hierarchy or or update the TOC units metadata against the passed Textbook Id.

There will be an API which will download the TOC hierarchy in csv format.

\


### **Textbook Hierarchy CSV upload API:** <a href="#etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-textbookhierarchycsvuploadapi" id="etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-textbookhierarchycsvuploadapi"></a>

**POST - textbook/v1/toc/upload/{content\_id}**

#### **Validation Logic:** <a href="#etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-validationlogic" id="etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-validationlogic"></a>

| validation             | description                                                                                                        | type        | configurable |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------ | ----------- | ------------ |
| Textbook Name          | Textbook Name from the file should be validated against data fetched against content Id                            | Data        | N/A          |
| Textbook Creator       | Based on the authorisation, the API should validate if the user calling the API has "Textbook Creator" role or not | User        | N/A          |
| First Level Unit limit | There could be maximum 30 first level unit (i.e. Chapter)                                                          | Data        | Yes          |
| File Rows              | There should not be more than 2500 rows                                                                            | File        | Yes          |
| File Headers           | If the file contains the required headers or not                                                                   | Column      | Yes          |
| File exists and type   | If the API has been invoked with a file of valid extension or not                                                  | File        | N/A          |
| File contains data     | If the file contains data other than header                                                                        | Data        | N/A          |
| Duplicate data         | validation to verify if there is duplicate row (approach described in details below)                               | Data        | N/A          |
| <p><br></p>            | <p><br></p>                                                                                                        | <p><br></p> | <p><br></p>  |

Approach for duplicate row validation

1st Approach :

* In this approach first, we will get each row, concatenate each cell data together after trimming and create a hash of the string (ex. md5). Then we will be putting it in a hashset after verifying if it does not exists. In case hash of any row is already existing we will throw duplicate row error.

&#x20;2nd Approach:

* This approach is similar in concept to previous one however here we will validate the duplicate while creating a tree for the ToC. We can store the ToC info of Textbook as Map\<String,Map\<String,Set\<String>>>. While creating this structure if at any point we see a collision, we can throw duplicate row error.

**Comparison of above approaches**&#x20;

| Approach | pros                | cons                                             |
| -------- | ------------------- | ------------------------------------------------ |
| 1st      | simple to implement | concatenation                                    |
| 2nd      | no extra check      | would need treemap and treeset to maintain order |

#### **Request Header:** <a href="#etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-requestheader" id="etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-requestheader"></a>

Authorisation: //Authorisation key

Content-Type: multipart/form-data'

X-Channel-Id: //Channel for which Textbook has been created

X-Authenticated-User-Token: //User token for Authentication

#### **Request:** <a href="#etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-request" id="etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-request"></a>

```
file: [csv formatted file]
```

After the validations are successful we need to process data in the required format to make a post call to [update hirearchy](http://docs.sunbird.org/latest/apis/content/#operation/Hierarchy%20Update%20Content) for the toc to be created.

**Response : Success Response - OK (200)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": null,
        "status": "success",
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {
        "contentId": "content_id",
        "versionKey": "101010101010"
    }
}
```

**Response: Wrong Texbook Id - ERROR (400)**

```
{
   "id": "textbook.toc.upload",
   "ver": "v1",
   "ts": "2018-11-15 13:52:50:990+0530",
   "params": {
       "resmsgid": null,
       "msgid": null,
       "err": "TEXTBOOK_NOT_FOUND",
       "status": null,
       "errmsg": "Textbook not found."
   },
   "responseCode": "CLIENT_ERROR",
   "result": {}
}
```

**Response: Wrong contentType or mimetype - ERROR (400)**

```
 {
   "id": "textbook.toc.upload",
   "ver": "v1",
   "ts": "2018-11-15 13:52:50:990+0530",
   "params": {
       "resmsgid": null,
       "msgid": null,
       "err": "INVALID_TEXTBOOK",
       "status": null,
       "errmsg": "Not a valid Textbook content."
   },
   "responseCode": "CLIENT_ERROR",
   "result": {}
}
```

**Response: CSV file has more than specified number of rows - ERROR (400)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "CSV_ROWS_EXCEEDS",
        "status": null,
        "errmsg": "Number of rows in csv file is more than 2500."
    },
    "responseCode": "CLIENT_ERROR",
    "result": {}
}
```

**Response: Textbook name against parameter id and textbook name in csv not matching - ERROR (400)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "INVALID_TEXTBOOK_NAME",
        "status": null,
        "errmsg": "Textbook Name given in the file doesn’t match current Textbook name. Please check and upload again."
    },
    "responseCode": "CLIENT_ERROR",
    "result": {}
}
```

**Response: Duplicate set TOC hierarchy in csv file - ERROR (400)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "DUPLICATE_ROWS",
        "status": null,
        "errmsg": "Duplicate rows found in csv."
    },
    "responseCode": "CLIENT_ERROR",
    "result": {}
}
```

**Response: Required set of headers are not available - ERROR (400)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "REQUIRED_HEADER_MISSING",
        "status": null,
        "errmsg": "Required set of header missing: <List of mandatory headers>"
    },
    "responseCode": "CLIENT_ERROR",
    "result": {}
}
```

**Response: Data in mandatory fields are missing - ERROR (400)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "REQUIRED_FIELD_MISSING",
        "status": null,
        "errmsg": "Data in mandatory fields is missing. Mandatory fields are: <List of mandatory headers>"
    },
    "responseCode": "CLIENT_ERROR",
    "result": {}
}
```

**Response: There are no rows in the CSV except the headers - ERROR (400)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "BLANK_CSV_DATA
        "status": null,
        "errmsg": "Did not find any TOC data. Please check and upload again."
    },
    "responseCode": "CLIENT_ERROR",
    "result": {}
}
```

**Response: Number of first level units is more than config value - ERROR (400)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "EXCEEDS_MAX_CHILDREN",
        "status": null,
        "errmsg": "Number of first level units is more than <config value>."
    },
    "responseCode": "CLIENT_ERROR",
    "result": {}
}
```

**Response: Textbook already have children - ERROR (400)**

```
{
   "id": "textbook.toc.upload",
   "ver": "v1",
   "ts": "2018-11-15 13:52:50:990+0530",
   "params": {
       "resmsgid": null,
       "msgid": null,
       "err": "TEXTBOOK_CHILDREN_EXISTS",
       "status": null,
       "errmsg": "Textbook is already having children."
   },
   "responseCode": "CLIENT_ERROR",
   "result": {}
}
```

**Response: Textbook can not be updated - transaction exception - ERROR (400)**

```
{
    "id": "textbook.toc.upload",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "TEXTBOOK_UPDATE_FAILURE
        "status": null,
        "errmsg": "Textbook could not be updated."
    },
    "responseCode": "CLIENT_ERROR",
    "result": {}
}
```

### **Textbook Hierarchy CSV download API:** <a href="#etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-textbookhierarchycsvdownloadapi" id="etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-textbookhierarchycsvdownloadapi"></a>

**GET - textbook/v1/toc/download/{content\_id}**

#### **Validation Logic:** <a href="#etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-validationlogic-.1" id="etb2.0-uploadtoc-updatetoc-and-downloadtocusingcsv-validationlogic-.1"></a>

| validation    | description                             | type | configurable |
| ------------- | --------------------------------------- | ---- | ------------ |
| Textbook Id   | Textbook Id should be valid             | Data | NA           |
| Textbook Unit | Textbook should have at least one child | Data | NA           |

After the validations are successful we need to get the Textbook hierarchy based on query parameter **mode=edit,** generate the csv file and return the file in response.

**Response : Success Response - OK (200)**

```
{
    "id": "textbook.toc.download",
    "ver": "v1",
    "ts": "2018-11-15 13:52:50:990+0530",
    "params": {
        "resmsgid": null,
        "msgid": null,
        "err": "null
        "status": "success",
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {
        "textbook": {
            "tocUrl": "<CLOUD_BASE_URL>/content/textbook/toc/<textbook_id>_<versionKey>.csv",
            "ttl": <time in seconds>
        }
    }
}
```
