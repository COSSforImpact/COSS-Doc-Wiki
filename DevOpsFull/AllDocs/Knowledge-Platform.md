

falseLog in to the Jenkins and do the following


## Build

* Switch to Build folder and run all jobs. Provide the value for  **github_release_tag**  as per the details mentioned in this page - [[Current Release Tags and Jenkins Jobs Reference|Current-Release-Tags-and-Jenkins-Jobs-Reference]]


## OpsAdministration

1. Bootstrap                                                                                                               # Creates Deployer User


## Provision

* Download neo4j enterprise 3.3.x version and keep it in your private repo under artifacts directory. The name of the file should be ending with neo4j\*.tar.gz
* Since the file size of neo4j will be larger than 100 MB, you need to use git lfs to store this artifact in your private repo. Refer this link to see for git lfs details - [https://git-lfs.github.com/](https://git-lfs.github.com/)
* Switch to Provision/<env>/KnowledgePlatform and run jobs in following order
    1. Cassandra
    1. CompositeSearch
    1. Neo4j
    1. Zookeeper
    1. Kafka
    1. Learning
    1. Redis
    1. Search

    

Deploy
* Switch to Deploy/dev/KnowledgePlatform and run all jobs in the following order
    1. CassandraDbUpdate
    1. Neo4j
    1. StartNeo4jCluster
    1. Learning
    1. Search
    1. Neo4jDefinitionUpdate
    1. Neo4jElasticSearchSyncTool
    1. KafkaSetup
    1. Yarn

    

    

Manual Run - Content retire API
* Login to the cassandra VM and run the below commands
*  **vi /etc/cassandra/cassandra.yaml** 
* Update the value as  **batch_size_fail_threshold_in_kb: 200** 
*  **service cassandra restart** 
*  **cd /tmp** 
*  **wget https://sunbirdpublic.blob.core.windows.net/installation/script_data.csv** 
* Run  **cqlsh** 
*  **COPY dev_script_store.script_data FROM '/tmp/script_data.csv';          ** (Here  **dev**  will be you env name)
*  **SELECT COUNT(*) FROM dev_script_store.script_data ;                         ** (Output should be 324 rows)
* Login to learning VM and restart tomcat
*  **sudo service tomcat restart** 
* Now you should be able to delete contents from workspace, drafts, contents which are published etc.



*****

[[category.storage-team]] 
[[category.confluence]] 
