---
icon: elementor
---

# Knowlg - Domain Agnostic Data

## Introduction <a href="#knowlg-domainagnosticdata-introduction" id="knowlg-domainagnosticdata-introduction"></a>

This wiki explains the current format of the absolute path stored in DBs (Neo4J, Cassandra, ES) and the proposed design to make it domain-agnostic.

## Background & Problem Statement <a href="#knowlg-domainagnosticdata-background-and-problemstatement" id="knowlg-domainagnosticdata-background-and-problemstatement"></a>

Knowlg uses URL storage in various scenarios to save and access URLs. The metadata of the functional objects stores the references (URLs) of the respective data.

For example, the content object in the Sunbird Knowlg building block stores the URLs of different files in its metadata to refer to the actual content.

#### Key Design Problems <a href="#knowlg-domainagnosticdata-keydesignproblems" id="knowlg-domainagnosticdata-keydesignproblems"></a>

1. Replace usage of absolute URLs in metadata with relative path while storing in DB.
2. While reading the data it should return the absolute path.

## Design <a href="#knowlg-domainagnosticdata-design" id="knowlg-domainagnosticdata-design"></a>

With the above problem statement, it is clear that we should not use the absolute path directly in our databases or any other places. Configure the base path, trim it while storing it, and prefix it while reading.

#### Solution 1: <a href="#knowlg-domainagnosticdata-solution1" id="knowlg-domainagnosticdata-solution1"></a>

Trim the URL as a relative path in [**EkStepTransactionEventHandler**](https://github.com/project-sunbird/knowledge-platform-db-extensions/blob/release-4.1.0/neo4j-extensions/transaction-event-handler/src/main/java/org/sunbird/kernel/extension/EkStepTransactionEventHandler.java) (in knowledge-platform-db-extentions) while storing after generating the logstash events (so ES will have the absolute path and no code changes will be required for ES).

For the returning the absolute path while reading the data from DB, prefix the base path in the following classes based on different repos:

* knowledge-platform: [**GraphService**](https://github.com/project-sunbird/knowledge-platform/blob/master/ontology-engine/graph-core\_2.11/src/main/scala/org/sunbird/graph/GraphService.scala) (in ontology-engine)
* knowledge-platform-jobs: [**CassandraUtil**](https://github.com/project-sunbird/knowledge-platform-jobs/blob/master/jobs-core/src/main/scala/org/sunbird/job/util/CassandraUtil.scala), [**Neo4JUtil**](https://github.com/project-sunbird/knowledge-platform-jobs/blob/master/jobs-core/src/main/scala/org/sunbird/job/util/Neo4JUtil.scala) (in jobs-core)



#### Solution 2: <a href="#knowlg-domainagnosticdata-solution2" id="knowlg-domainagnosticdata-solution2"></a>

Instead of trimming the relative path in [**EkStepTransactionEventHandler**](https://github.com/project-sunbird/knowledge-platform-db-extensions/blob/release-4.1.0/neo4j-extensions/transaction-event-handler/src/main/java/org/sunbird/kernel/extension/EkStepTransactionEventHandler.java), do it in GraphService only. But in this solution, ES data needs to be handled in the search-indexer job. Reading will be same as solution 1.



### Pros & Cons <a href="#knowlg-domainagnosticdata-pros-and-cons" id="knowlg-domainagnosticdata-pros-and-cons"></a>

| **Solution** | **Pros**                                                                                                                                                                                                               | **Cons**                                                                                                                                                                |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Solution 1   | <ul><li>Code changes will required only in DB layer. No other code/logic changes will be required.</li><li>Hence Trimming the data in TransactionEventHandler so no ES data handling is required separately.</li></ul> | <ul><li>If adopter later wanted to switch from Neo4J to other DB then he need to handle the data trimming part because it is part of TransactionEventHandler.</li></ul> |
| Solution 2   | <ul><li>Code changes will required only in DB layer. No other code/logic changes will be required.</li><li>If adopter later wanted to switch from Neo4J to other DB then he not need to do anything extra.</li></ul>   | <ul><li>ES data needs to handle in search-indexer while indexing the data.</li></ul>                                                                                    |
