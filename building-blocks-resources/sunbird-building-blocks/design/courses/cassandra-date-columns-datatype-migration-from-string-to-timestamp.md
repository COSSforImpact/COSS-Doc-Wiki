---
icon: elementor
---

# Cassandra-date-columns-datatype-migration-from-string-to-timestamp

### Overview

In cassandra data store used by course progress monitoring, few columns which are having date in string format. This results in date and timestamp mismatches when comparing with timezones.

Thus, in order to maintain standards and to address the date comparison issue, datatype migration of these columns from string to timestamp is required.

This document details about the approach taken for migration.

### Assumption

* All the date timezones are in UTC, as per cassandra [doc](https://docs.datastax.com/en/drivers/python/3.4/dates\_and\_times.html), timestamps are preferred with UTC.

### Design

In order to avoid downtime and have backward compatibility, introducing new columns with type timestamp as below

| **Keypsace.Table name**                          | **Existing columns ( type text)**                           | **New columns (type timestamp)**                                      |
| ------------------------------------------------ | ----------------------------------------------------------- | --------------------------------------------------------------------- |
| sunbird\_courses. **course\_batch**              | createddate startdate enddate enrollmentenddate updateddate | created\_date start\_date end\_date enrollment\_enddate updated\_date |
| sunbird\_courses. **user\_enrolments**           | enrolleddate                                                | enrolled\_date                                                        |
| sunbird\_courses. **user\_content\_consumption** | lastaccesstimelastcompletedtimelastupdatedtime              | last\_access\_timelast\_completed\_timelast\_updated\_time            |
| sunbird. **page\_management**                    | createddate                                                 | created\_date                                                         |
| sunbird. **page\_section**                       | createddate updateddate                                     | created\_date updated\_date                                           |

* Any new creation or updation, will update only new columns.
* On updates, if new column is NULL, the corresponding older column value is taken and updated to new one.
* While reading the data, if new column is NULL, the corresponding older column value is read.

#### Impact Analysis

APIs

* CourseBatch - create and update APIs
* Enrolments - Enrol, Un-enrol, ContentStateUpdate, ReadContentStatus
* Page - PageCreate, PageUpdate, PageSectionCreate, PageSectionUpdate

Data Products - Read only

* Exhaust reports
* CollectionSummary V1 and V2
* CollectionReconciliation
* CourseBatchStatusUpdater
* UserCacheUpdater (Verification only, no changes required)

Adhoc Scripts

* No changes required as the data is being read from druid only.

***

\[\[category.storage-team]] \[\[category.confluence]]
