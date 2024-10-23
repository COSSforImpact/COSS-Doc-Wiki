---
icon: elementor
---

# Adding-New-Cloud-Libraries-for-ml-analytics-service

This document details about integration points for any new CSP provider with ml-analytics platform

ml-analytics release-5.1.0, latest as on Dec, 2022

Few points to note:

* ml-analytics-service has integrated code with Azure, AWS, Oracle and GCP.
* ml-analytics-service uses cloud for pre-processed data to be pushed before ingesting into Druid datasources.

noteIn order to add support for any other cloud storage under ml-analytics components, below steps need to be followed:

In order to add support for any other cloud storage under ml-analytics components, below steps need to be followed:

#### Git repository:

[https://github.com/Sunbird-Ed/ml-analytics-service](https://github.com/Sunbird-Ed/ml-analytics-service)Latest Branch: release-5.1.0

#### Changes to the cloud\_storage folder:

1. Add a new blank file with the name of the cloud service provider with the name of the cloud provider (Eg: ms\_azure.py, oracle.py). Make sure the file is created inside the cloud\_storage folder in the same hierachy as other files such as ms\_azure.py, gcp.py
2. Import relavant and necessary libraries that can interact with the new cloud provider.
3. Define a Python Class Object .
4. Under the intilization method or **init**, construct and initlialize variables that identify the -
   1. Cloud account ID
   2. Cloud account Key
   3. Cloud account storage container/blob
   4. Any other necessary variable that need to be initiated to interact with the cloud storage (Eg: token, type)
5. Create a Class-method named upload\_files that has three (3) arguments -
   1. bucketPath - Accepts the cloud account storage container/blob
   2. localPath- Accept the local path of where the file is generated
   3. fileName- Accepts the name of the file
6. Then call the upload function from the library.

An example of the code is given below:

```py
### -----Step 2 ----- ###
import os
import boto3

### ---- Step 3 ---- ###
class Oracle:
    '''
    Class to inititate and upload data in Oracle
    '''

### ---- Step 4 ---- ###
    def __init__(self, regionName, accessKey, secretAccessKey, endpoint_url, bucketName):
        self.oracle = boto3.client(
            service_name = 's3',
            region_name = regionName,
            aws_access_key_id = accessKey,
            aws_secret_access_key = secretAccessKey,
            endpoint_url = endpoint_url
        )
        self.bucket = bucketName

### ---- Step 5 ---- ###        
    def upload_files(self, bucketPath, localPath, fileName):
    
### ---- Step 6 ---- ###        
        with open(f"{localPath}/{fileName}", "rb") as file:
            self.oracle.upload_fileobj(file, self.bucket, f"{bucketPath}/{fileName}")
```

#### Changes to the cloud.py file

1. Import the Library you created in the cloud.py file
2. Inside the MultiCloud Class - look for upload\_to\_cloud method
3. Add an elif statement that refer to the recently created cloud library-
   * Initialize the cloud library by passing in the necessary parameters
   * Call the upload\_files method and pass in these below values:

```py
<<name_of_service>>_service.upload_files(bucketPath = blob_Path, localPath = local_Path, fileName = file_Name)
```

An example of the code is shown below:

```py
### ---- Step 1 ---- ###
from from oracle import Oracle
...

### ---- Step 2 & 3 ---- ### 
elif elements == "ORACLE":
                oracle_service = Oracle(
                    regionName = config.get("ORACLE", "region_name"),
                    accessKey = config.get("ORACLE", "access_key"),
                    secretAccessKey = config.get("ORACLE", "secret_access_key"),
                    endpoint_url = config.get("ORACLE", "endpoint_url"),
                    bucketName = config.get("ORACLE", "bucket_name")
                )
                oracle_service.upload_files(bucketPath = blob_Path, localPath = local_Path, fileName = file_Name)
```

#### Changes to the config.sample file

For the config.sample file, append a section in the config file:

An example is provided below:

```
[ORACLE]

endpoint_url = {{ ml_ORACLE_endpoint_url }}

access_key = {{ ml_ORACLE_access_key }}

secret_access_key = {{ ml_ORACLE_secret_access_key }}

region_name = {{ ml_ORACLE_region_name }}

bucket_name = {{ ml_ORACLE_bucket_name }}
```

Post adding these changes - [this repository ](https://github.com/project-sunbird/sunbird-devops/blob/master/ansible/roles/ml-analytics-service/defaults/main.yml)needs to be updated with the relevant values of the the added configuration variables.

***

\[\[category.storage-team]] \[\[category.confluence]]
