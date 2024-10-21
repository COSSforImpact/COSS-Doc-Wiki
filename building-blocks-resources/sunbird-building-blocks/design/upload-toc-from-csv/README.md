---
icon: folder-open
---

# Upload ToC from CSV

**Overview :**

&#x20;                  Provision for Textbook Creator to upload a csv in pre-defined format and system should be able to generate ToC based on that.

\


**Problem Statement:**

&#x20;                  Process of creation of Textbook ToC (Table of Content) through portal is time consuming, requires training and continuous internet connectivity. ToCs are in tree like structures hence one chapter can have multiple sections and those sections can have multiple subsections. To simplify the process it requires a way where user can upload a csv file with input data and ToC can be created in one go after validation.

[Sample CSV data.](https://docs.google.com/spreadsheets/d/1oft6OHg5izonTqJ1CrcyqTltZ7b-L3QGGT-jE1sUjtY/) Also, there should be a way to update the attributes of sections, to help user do that - we should be able to download the content as csv format.

\


**Proposed Solution:**

To facilitate the process of ToC creation through CSV an API needs to be exposed which will take csv file as a request .

&#x20;             &#x20;

&#x20;Once the file has been uploaded the system will do below **validations**

\


| validation             | description                                                                                                        | type   | configurable                                                                            |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------ | ------ | --------------------------------------------------------------------------------------- |
| Textbook Creator       | based on the authorization, the API should validate if the user calling the API has "Textbook Creator" role or not | User   | N/A                                                                                     |
| File exists and type   | if the API has been invoked with a file of valid extension or not                                                  | File   | N/A                                                                                     |
| File Size              | If the uploaded file size is more than set limit                                                                   | File   | Yes                                                                                     |
| File Headers           | If the file contains the required headers or not                                                                   | Column | <p>Yes </p><p>mandatory and allowed headers would be stored in db in system setting</p> |
| File contains data     | If the file contains data other than header                                                                        | Data   | N/A                                                                                     |
| Duplicate data         | validation to verify if there is duplicate row (approach described in details below)                               | Data   | N/A                                                                                     |
| Textbook Name          | Textbook Name from the file should be validated against data fetched with get hirearchy call with content Id       | Data   | N/A                                                                                     |
| First Level Unit limit | There could be maximum 30 first level unit (i.e. Chapter)                                                          | Data   | Yes                                                                                     |

\


Upload ToC API

**POST v1/toc/:contentId**    (where contentId is textbook id)

&#x20;**Header**&#x20;

{

\
Content-Type : "multipart/form-data",\
ts:"",\
X-msgid:"",\
Authorization:"",\
x-authenticated-user-token:"

}

**Request**

data : \[file]

**Response : 200 OK**\


```
					{

						"id": "api.toc.create",	

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

							"response": "SUCCESS"

						}

					}
```

&#x20;                       **ERROR 400 Bad Request**

&#x20;                    {\
&#x20;                             "id": "api.toc.create",\
&#x20;                             "ver": "v1",\
&#x20;                             "ts": "2018-11-15 13:52:50:990+0530"\
&#x20;                             "params": {\
&#x20;                                    "resmsgid": null,\
&#x20;                                    "msgid": null,\
&#x20;                                    "err": "UPLOAD\_TOC\_FAILED",\
&#x20;                                    "status": "UPLOAD\_TOC\_FAILED",\
&#x20;                                    "errmsg": "Table of Content could not be uploaded due to validation errors"\
&#x20;                                             },\
&#x20;                            "responseCode": "CLIENT\_ERROR",\
&#x20;                           "result": {}\
&#x20;                      }\
\
&#x20;                     **ERROR 404 Not Found**

&#x20;                    {\
&#x20;                             "id": "api.toc.create",\
&#x20;                             "ver": "v1",\
&#x20;                             "ts": "2018-11-15 13:52:50:990+0530"\
&#x20;                             "params": {\
&#x20;                                    "resmsgid": null,\
&#x20;                                    "msgid": null,\
&#x20;                                    "err": "RESOURCE\_NOT\_FOUND",\
&#x20;                                    "status": "RESOURCE\_NOT\_FOUND",\
&#x20;                                    "errmsg": "Resource not found"\
&#x20;                                             },\
&#x20;                            "responseCode": "CLIENT\_ERROR",\
&#x20;                           "result": {}\
&#x20;                      }

\


Update ToC Attributes

**PATCH     v1/toc/:contentId**    (where contentId is textbook id)

&#x20;**Header**&#x20;

{

Content-Type : "multipart/form-data",\
ts:"",\
X-msgid:"",\
Authorization:"",\
x-authenticated-user-token:"

}

**Request**

data : \[file]

**Response**

```
					{
						"id": "api.toc",	
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
							"response": "SUCCESS"
						}
					}

```

&#x20;                      **ERROR 400 Bad Request**

&#x20;                    {\
&#x20;                             "id": "api.toc.update",\
&#x20;                             "ver": "v1",\
&#x20;                             "ts": "2018-11-15 13:52:50:990+0530"\
&#x20;                             "params": {\
&#x20;                                    "resmsgid": null,\
&#x20;                                    "msgid": null,\
&#x20;                                    "err": "UPLOAD\_TOC\_FAILED",\
&#x20;                                    "status": "UPLOAD\_TOC\_FAILED",\
&#x20;                                    "errmsg": "Table of Content could not be uploaded due to validation errors"\
&#x20;                                             },\
&#x20;                            "responseCode": "CLIENT\_ERROR",\
&#x20;                           "result": {}\
&#x20;                      }\
\
&#x20;                     **ERROR 404 Not Found**

&#x20;                    {\
&#x20;                             "id": "api.toc.update",\
&#x20;                             "ver": "v1",\
&#x20;                             "ts": "2018-11-15 13:52:50:990+0530"\
&#x20;                             "params": {\
&#x20;                                    "resmsgid": null,\
&#x20;                                    "msgid": null,\
&#x20;                                    "err": "RESOURCE\_NOT\_FOUND",\
&#x20;                                    "status": "RESOURCE\_NOT\_FOUND",\
&#x20;                                    "errmsg": "Resource not found"\
&#x20;                                             },\
&#x20;                            "responseCode": "CLIENT\_ERROR",\
&#x20;                           "result": {}\
&#x20;                      }

\


Download ToC as CSV

**GET     v1/toc/:contentId**    (where contentId is textbook id)

&#x20;**Header**&#x20;

{

Content-Type : "multipart/form-data",\
ts:"",\
X-msgid:"",\
Authorization:"",\
x-authenticated-user-token:"

}

\


**Response**

```
			  {contentId}.csv -> downloaded as file, will contain the upload csv + attributes. 

```

&#x20;                           **ERROR 404 Not Found**

&#x20;                          {\
&#x20;                             "id": "api.toc.update",\
&#x20;                             "ver": "v1",\
&#x20;                             "ts": "2018-11-15 13:52:50:990+0530"\
&#x20;                             "params": {\
&#x20;                                    "resmsgid": null,\
&#x20;                                    "msgid": null,\
&#x20;                                    "err": "RESOURCE\_NOT\_FOUND",\
&#x20;                                    "status": "RESOURCE\_NOT\_FOUND",\
&#x20;                                    "errmsg": "Resource not found"\
&#x20;                                             },\
&#x20;                            "responseCode": "CLIENT\_ERROR",\
&#x20;                           "result": {}\
&#x20;                        }

\


**Approach for duplicate row validation**

1st Approach :

\


In this approach first, we will get each row, concatenate each cell data together after trimming and create a hash of the string (ex. md5). Then we will be putting it in a hashset after verifying if it does not exists.&#x20;

In case hash of any row is already existing we will throw duplicate row error.

&#x20;2nd Approach:

This approach is similar in concept to previous one however here we will validate the duplicate while creating a tree for the ToC. We can store the ToC info of Textbook as Map\<String,Map\<String,Set\<String>>>. While creating this structure if at any point we see a collision, we can throw duplicate row error.

3rd Approach:

We can use guava bloom filter library for finding out the duplicate.

**Comparison of above approaches**&#x20;

| Approach | pros                              | cons                                             | <p><br></p> |
| -------- | --------------------------------- | ------------------------------------------------ | ----------- |
| 1st      | simple to implement               | concatenation                                    | <p><br></p> |
| 2nd      | no extra check                    | would need treemap and treeset to maintain order | <p><br></p> |
| 3rd      | memory friendly for large dataset | probabilistic with chance of false positive      | <p><br></p> |

\


After the validations are successful we need to process data in the required format to make a post call to [update hirearchy](http://docs.sunbird.org/latest/apis/content/#operation/Hierarchy%20Update%20Content) for the toc to be created.

\


&#x20;&#x20;

&#x20;               &#x20;

\


\


\


&#x20;             &#x20;

.&#x20;
