---
icon: folder-open
---

# Manual-configurations

With every new release of sunbird you will be able to experience new features, improved performance and bug squashes.

In this document, we will cover detailed steps on how to upgrade Sunbird 1.14.0 to 2.0.0. A lot has changed from 1.14.0 to 2.0.0 with respect to backend configurations. Below are the highlights of the changes:

1. Core Elasticsearch upgraded
2. Core Elasticsearch 6.x creation of indices with mapping
3. Migration of core elasticsearch data from old indices to new indices
4. Keycloak configuration
5. Run maskEmailPhoneMigration ETL Job for Core Cassandra
6. Run UserSync ETL Job for Core Cassandra
7. Run ETL job to delete user from Keycloak postgres DB
8. Run course batch sync job

You can click on the links which will take you to the respective pages. This page will have details on how to run the respective step

* \[\[Core Elasticsearch upgrade|Core-Elasticsearch-upgrade]]
* \[\[Keycloak Configuration|Keycloak-Configuration]]
* \[\[ETL jobs to run for upgrading to release-2.0.0|ETL-jobs-to-run-for-upgrading-to-release-2.0.0]]

***

\[\[category.storage-team]] \[\[category.confluence]]
