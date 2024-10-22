---
icon: elementor
---

# Data-Pipeline

falseLog in to the Jenkins and do the following

### Build

* Switch to Build folder and run all jobs. Provide the tag as **release-1.14.0** in the build job parameter **github\_release\_tag**

### Provision

* Switch to Provision//DataPipeline and run all jobs
  1. AnalyticsApi
  2. AnalyticsSecor
  3. AnalyticsSpark
  4. Influxdb
  5. Kibana
  6. Postgress
  7. Yarn

Deploy

* Switch to Deploy/dev/DataPipeline and run all jobs in following order
  1. CassandraDbUpdate
  2. KafkaSetup
  3. AnalyticsApi
  4. DataProducts
  5. Secor
  6. KafkaIndexer
  7. SamzaTelemertySchemas
  8. Yarn

***

\[\[category.storage-team]] \[\[category.confluence]]
