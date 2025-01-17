---
icon: elementor
---

# SC-2190 : ES scaling - reindexing Org index

### About <a href="#sc-2190-esscaling-reindexingorgindex-about" id="sc-2190-esscaling-reindexingorgindex-about"></a>

The org index mapping has been reviewed and optimised to reduce the index size without limiting any of the search capabilities.

### Steps to re-index the data with the new mapping: <a href="#sc-2190-esscaling-reindexingorgindex-stepstore-indexthedatawiththenewmapping" id="sc-2190-esscaling-reindexingorgindex-stepstore-indexthedatawiththenewmapping"></a>

1.  First check the number of **number\_of\_shards** & **number\_of\_replicas** from old org index by running below curl\


    ```
    curl --location --request GET 'http://localhost:9200/_cat/indices/%2A?v=&s=index:desc'
    ```

2\. Create new org index with name as orgv{x} // x is version number and update the org mapping using ES Mapping jenkins job {**OpsAdministration/job/dev/job/Core/job/ESMapping/**}

3\. After updating org mapping, run the reindex curl\


```
curl --location --request POST 'localhost:9200/_reindex?pretty' \
--header 'Content-Type: application/json' \
--data-raw '{
  "source": {
    "index": "{old_org_index_name}"
  },
  "dest": {
    "index": "{new_org_index_name}"
  }
}'
```

4\. After updating replica , add alias to the new index with alias name as **org\_alias** , by below curl\


```
curl --location --request PUT 'localhost:9200/{new_index_name}/_alias/org_alias?pretty'
```

Note : If alias name changed other than **org\_alias,** update the learner env for **org\_index\_alias**

To remove alias binding from old index run the below curl

```
curl --location --request DELETE 'localhost:9200/{old_index_name}/_alias/org_alias?pretty'
```

5\. Deploy the learner and check the disk usage , replica number for the new index by running the below curl\


```
curl --location --request GET 'http://localhost:9200/_cat/indices/%2A?v=&s=index:desc'
```
