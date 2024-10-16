---
icon: elementor
---

# How to add a new column and migrate data in learner ( Cassandra, ES)

### Development: <a href="#howtoaddanewcolumnandmigratedatainlearner-cassandra-es-development" id="howtoaddanewcolumnandmigratedatainlearner-cassandra-es-development"></a>

1. Create PR in sunbird utils for new column
2. Create PR in devops for api changes and ES index, mapping and ingect-pipeline
3. Create PR in sunbird-documentaion for apis
4. Create PR in learner for api changes
5. Create PR for Ed-dataproducts changes if necessary
6. Create wiki documentation for data migration using scala script
7. Create wiki documentation for ES reindexing
   1. ES reindexing can be done if the data has to be populated in ES from new column after running scala script, that will be easier than syncing data using api
   2. If same column is changed only mapping need to be updated

### Dev deployment steps: <a href="#howtoaddanewcolumnandmigratedatainlearner-cassandra-es-devdeploymentsteps" id="howtoaddanewcolumnandmigratedatainlearner-cassandra-es-devdeploymentsteps"></a>

1. Run cassandra migration in dev using jenkins to create column\
   [http://10.20.0.14:8080/jenkins/job/Build/job/Core/job/Cassandra/](http://10.20.0.14:8080/jenkins/job/Build/job/Core/job/Cassandra/)
2. Do API on boarding using\
   [http://10.20.0.14:8080/jenkins/job/Build/job/Core/search/?q=Deploy+dev+OnboardAPIs](http://10.20.0.14:8080/jenkins/job/Build/job/Core/search/?q=Deploy+dev+OnboardAPIs)
3. Cassandra data migration
   1. Connect to spark using VPN and Bastion - > Run scala script
   2. Connect to Cassandra - Verify data
4. ES re-indexing
   1. Connect to ES
   2. Check indexes
   3. Merge devops PR with index, mapping and ingest-pipeline
   4. Run [http://10.20.0.14:8080/jenkins/job/Provision/job/dev/job/Core/job/ESMapping](http://10.20.0.14:8080/jenkins/job/Provision/job/dev/job/Core/job/ESMapping) job to create index, mapping and ingect-pipeline
   5. Check indexes
   6. Map index to alias if not already specified alias in index file
   7. if pipeline needed then only run the job with pipeline
   8. delete old index-alias mapping
5. Create tag & deploy learner
6. Test the changes using update read and search api for records with column data and without data

### Staging deployment steps: <a href="#howtoaddanewcolumnandmigratedatainlearner-cassandra-es-stagingdeploymentsteps" id="howtoaddanewcolumnandmigratedatainlearner-cassandra-es-stagingdeploymentsteps"></a>

1. Create staging tag for sunbird-utils, devops and ask devops for below deployment:\
   Share the same in deployment sheet [https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1197636720](https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1197636720)
2. Trigger cassandra-migration job in staging\
   Details mentioned in [https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951](https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951) line no: 28
3. Trigger OnboardingAPIs job in staging\
   Line number 29, [https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951](https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951)
4. Run Scala script for cassandra migration in staging :\
   [SB-26822 Cassandra data migration from userProfileType to userProfileTypes](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/2993618947/SB-26822+Cassandra+data+migration+from+userProfileType+to+userProfileTypes)\
   Line number 43 in deployment sheet [https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951](https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951)
5. Do ES re-indexing in stagingStaging deployment steps:\
   [https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951](https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951)\
   Line number 44 in deployment sheet [https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951](https://docs.google.com/spreadsheets/d/1xoOXNtDR7fnW9CU4mj8Q2xZr2mkdqpXdAfCOjD9BfrY/edit#gid=1898689951)
