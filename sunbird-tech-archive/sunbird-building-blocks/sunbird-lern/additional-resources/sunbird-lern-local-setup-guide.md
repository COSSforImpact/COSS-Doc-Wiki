---
icon: elementor
---

# Sunbird Lern Local Setup Guide

### **Context:** <a href="#leaf9kmbyhw0" id="leaf9kmbyhw0"></a>

This document helps in understanding the local setup, for one of the key microservice of the Sunbird Lern Building Block. This will enable the participants of the bootcamp to choose and work on the problem statements given below.

It has the details about setting up the **batch-service** from the scratch on your local machine.

![](<../../../../.gitbook/assets/0 (1).png>)**Prerequisite**

* Java 11
* Maven – Latest
* Docker – Latest
* Cassandra 3.11.6
* ES 6.8.11
* IntelliJ Editor
* Postman
* GIT

#### **Validate Prerequisites** <a href="#id-2spd1lv7p4xm" id="id-2spd1lv7p4xm"></a>

| **Service** | **Details to validate**                                |
| ----------- | ------------------------------------------------------ |
| Java 11     | _java -version_                                        |
| Maven       | _mvn -v_                                               |
| Docker      | _Check the docker process or “ps -ef \| grep docker”._ |

### **Prepare your machine** <a href="#id-2u9l8m6af6vg" id="id-2u9l8m6af6vg"></a>

#### **Create a folder structure to organize the data** <a href="#fn5wpirz44p2" id="fn5wpirz44p2"></a>

| **Command**      | <p><em>mkdir -p ~/sunbird-dbs/cassandra ~/sunbird-dbs/es</em></p><p><em>export sunbird_dbs_path=~/sunbird-dbs</em></p> |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Verification** | _echo $sunbird\_dbs\_path_                                                                                             |

#### **Setup Cassandra** <a href="#id-59f6rtjx1ypr" id="id-59f6rtjx1ypr"></a>

| **Pull Cassandra docker image**      | _docker pull cassandra:3.11.6_                                                                                                                                                                                                                                                  |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Create a docker network**          | _docker network create sunbird\_db\_network_                                                                                                                                                                                                                                    |
| **Start Cassandra docker container** | _docker run -p 9042:9042 --name sunbird\_cassandra -v $sunbird\_dbs\_path/cassandra/data:/var/lib/cassandra -v $sunbird\_dbs\_path/cassandra/logs:/opt/cassandra/logs -v $sunbird\_dbs\_path/cassandra/backups:/mnt/backups --network sunbird\_db\_network -d cassandra:3.11.6_ |
| **Validate**                         | _docker ps -a \| grep cassandra_                                                                                                                                                                                                                                                |

#### **Seed data to Cassandra** <a href="#wyzuyckn0a46" id="wyzuyckn0a46"></a>

| **Provide permission to the sunbird-dbs/cassandra folder**                                   | _chmod -R 777 sunbird-dbs/cassandra_                                                                                                                                     |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Copy the sunbird\_courses.cql file from github to /sunbird-dbs/cassandra/backups folder.** | _wget -O sunbird-dbs/cassandra/backups/sunbird\_courses.cql https://raw.githubusercontent.com/Sunbird-Lern/sunbird-course-service/bootcamp/scripts/sunbird\_courses.cql_ |
| **Start the Cassandra cypher shell**                                                         | _docker exec -it sunbird\_cassandra cqlsh_                                                                                                                               |
| **Load database schema**                                                                     | _source '/mnt/backups/sunbird\_courses.cql'_                                                                                                                             |

#### **Setup Elasticsearch** <a href="#hs24syyyku9h" id="hs24syyyku9h"></a>

| **Pull Elasticsearch docker image**                    | _docker pull elasticsearch:6.8.11_                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Start Elasticsearch docker container**               | _docker run -p 9200:9200 --name sunbird\_es -v $sunbird\_dbs\_path/es/data:/usr/share/elasticsearch/data -v $sunbird\_dbs\_path/es/logs://usr/share/elasticsearch/logs -v $sunbird\_dbs\_path/es/backups:/opt/elasticsearch/backup -e "discovery.type=single-node" --network sunbird\_db\_network -d docker.elastic.co/elasticsearch/elasticsearch:6.8.11_ |
| **Validate**                                           | _docker ps -a \| grep es_                                                                                                                                                                                                                                                                                                                                  |
| **Change permissions for the folder**                  | _chmod -R 777 sunbird-dbs/es_                                                                                                                                                                                                                                                                                                                              |
| **Create “course-batch” index and update the mapping** | _Bootcamp postman collection in the link below has the API collection and environment json files, import it in Postman and create index and mapping._ [_https://github.com/Sunbird-Lern/sunbird-course-service/tree/bootcamp/scripts/postman_](https://github.com/Sunbird-Lern/sunbird-course-service/tree/bootcamp/scripts/postman)                       |

#### **Setup Redis** <a href="#dxhhszwv1dfq" id="dxhhszwv1dfq"></a>

| **Pull Redis docker image**       | _docker pull redis:4.0.0_                                      |
| --------------------------------- | -------------------------------------------------------------- |
| **Start Redis docker container**  | _docker run --name sunbird\_redis -d -p 6379:6379 redis:4.0.0_ |
| **Validate**                      | _docker ps -a \| grep redis_                                   |
| **SSH to Redis docker container** | _docker exec -it sunbird\_redis bash_                          |

#### **Batch Service Setup** <a href="#hz8livb5z7vs" id="hz8livb5z7vs"></a>

Please fork the repository to use and make modifications. Below are the steps to fork and clone the repository.

![](<../../../../.gitbook/assets/1 (1).png>)

| **Repository** | [https://github.com/Sunbird-Lern/sunbird-course-service](https://github.com/Sunbird-Lern/sunbird-course-service) |
| -------------- | ---------------------------------------------------------------------------------------------------------------- |

**🗒️ Note:** Please uncheck the “Copy the main branch only”. This will copy all the branches to the fork.

| **Clone Repository**                 | _git clone https://github.com/\<YOUR\_FORK>/sunbird-course-service.git_                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Branch**                           | _bootcamp_                                                                                                                                                                                                                                                                                                                                                                                               |
| **Checkout branch**                  | <p><em>cd sunbird-course-service</em></p><p><em>git remote -v</em></p><p><em>git remote remove origin</em></p><p><em>git remote add origin git@github.com:reshmi-nair/sunbird-course-service.git</em></p><p><em>git remote add upstream</em></p><p><em>git@github.com:sunbird-lern/sunbird-course-service.git</em></p><p><em>git checkout -b bootcamp</em></p><p><em>git pull upstream bootcamp</em></p> |
| **Export the configuration**         | _Update the **lms-service.sh** file in the **scripts** folder with configuration values to setup environment variables. Copy and run it to export the values_                                                                                                                                                                                                                                            |
| **Verify the configuration**         | _echo $sunbird\_es\_host_                                                                                                                                                                                                                                                                                                                                                                                |
| **Copy Keys for token verification** | <p><em>Copy the keys folder from below link to local sunbird-course-services root folder</em></p><p><a href="https://drive.google.com/drive/u/0/folders/1V1CxHKP3IKMHg4s-Q_CSgvpu9bYdugNj"><em>https://drive.google.com/drive/u/0/folders/1V1CxHKP3IKMHg4s-Q_CSgvpu9bYdugNj</em></a></p>                                                                                                                 |
| **Build the code base**              | <p><em>cd sunbird-course-service</em></p><p><em>mvn clean install -DskipTests</em></p>                                                                                                                                                                                                                                                                                                                   |
| **Run the service**                  | <p><em>cd service</em></p><p><em>mvn play2:run</em></p>                                                                                                                                                                                                                                                                                                                                                  |
| **Check the setup using health API** | _curl --location --request GET 'http://localhost:9000/health’_                                                                                                                                                                                                                                                                                                                                           |

### **Additional Details:** <a href="#id-6jvmkeu6po1z" id="id-6jvmkeu6po1z"></a>

Please consider using the below user credentials for you to play with the APIs and experience the batch-service capabilities.

| **Group**          | **Credentials and Other Details**                                                                                                                                                                                                                                                                                                           |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Table – 1          | <p><strong>Creator:</strong> bccreator_table1_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table1_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Table – 2          | <p><strong>Creator:</strong> bccreator_table2_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table2_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Table – 3          | <p><strong>Creator:</strong> bccreator_table3_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table3_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Table – 4          | <p><strong>Creator:</strong> bccreator_table4_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table4_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Table – 5          | <p><strong>Creator:</strong> bccreator_table5_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table5_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Table – 6          | <p><strong>Creator:</strong> bccreator_table6_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table6_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Table – 7          | <p><strong>Creator:</strong> bccreator_table7_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table7_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Table – 8          | <p><strong>Creator:</strong> bccreator_table8_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table8_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Table – 9          | <p><strong>Creator:</strong> bccreator_table9_mar2023/Password@1</p><p><strong>Reviewer:</strong> bcreviewer_table9_mar2023/Password@1</p>                                                                                                                                                                                                  |
| Common Credentials | <p>bcuser1_mar2023/Password@1</p><p>bcuser2_mar2023/Password@1</p><p>bcuser3_mar2023/Password@1</p><p>bcuser4_mar2023/Password@1</p><p>bcuser5_mar2023/Password@1</p><p>bcuser6_mar2023/Password@1</p><p>bcuser7_mar2023/Password@1</p><p>bcuser8_mar2023/Password@1</p><p>bcuser9_mar2023/Password@1</p><p>bcuser10_mar2023/Password@1</p> |

### &#x20;<a href="#jgyd5vyupyxl" id="jgyd5vyupyxl"></a>

### **Problem Statements:** <a href="#uu7nyigs3pde" id="uu7nyigs3pde"></a>

#### **Use case 1:** [**LR-374**](https://project-sunbird.atlassian.net/browse/LR-374) **Compute the number of days to start the batch** <a href="#yeh0wryvllp8" id="yeh0wryvllp8"></a>

Each batch has the metadata to explain the start date, end date, enrolment end date. Please introduce a new property in the batch read API to explain **how many days are left for the users to** consume the course.

* Compute the duration in days.
* The new property name should be “daysToGo”
* The value should be a string.
* If the start date is a future date, “x days to go”.
* If the start date is today, “the batch started today”.
* If the start date is old, “started x days ago”.

#### **Use case 2:** [**LR-375**](https://project-sunbird.atlassian.net/browse/LR-375) **Limit enrolments for the batch** <a href="#me3tf48gy3jv" id="me3tf48gy3jv"></a>

There is no limitation on the number of enrolments in a batch. Enhance the enrolment feature to control the number of enrolments.

* Define the limit for the batch
  * Option 1: Create a default configuration to control the number of enrolments for the batches.
  * Option 2: Create a new attribute (update the batch table) and accept the limit for each batch as part of create or update API.
* Compute the number of enrolments and control.
  * Each successful enrolment should update the predefined counter.
  * Use the predefined counter and the configuration from the first step to limit the enrolments.
* Enrolment API response.
  * When the enrolment limit exceeds, the API should return HTTP 406 Not Acceptable as response with proper error details.

#### **Use case 3:** [**LR-376**](https://project-sunbird.atlassian.net/browse/LR-376) **Control enrolment for a specific type of users** <a href="#u2jy0oifsr6t" id="u2jy0oifsr6t"></a>

For a batch, any user of the sunbird instance can enrol and consume the course. Please enhance the enrolment capability to allow users with specific role or tagging.

The course has “audience” attribute to understand the targeted users. Please consider using the value of the audience (teacher) and map it with the user's metadata (userType) to allow the enrolment.

* Accept the enrolment if the audience (from the course) and userType from the enrolling user metadata matches.
* Use the auth token to extract the user identifier.
* Make the user read API call to fetch the metadata of the user.
* If the enrolment is for an invalid user, the API should return an error code with a message.
