---
icon: elementor
---

# Design: Consumption and Sourcing Repos

### **Introduction:** <a href="#design-consumptionandsourcingrepos-introduction" id="design-consumptionandsourcingrepos-introduction"></a>

The sunbird platform built by assuming there will be a controlled sourcing environment (a group of known people) for the content creation process. Now, there is a need to enable external people to come and contribute content to the platform.

With Content **Contribution Projects**, we enabled anyone to come and contribute. But, this setup duplicates most of the knowledge-platform (KP) DB storage (like Neo4J, Cassandra, CloudStorage etc,.) for sourcing and consumption repositories.

![](../../../../../../.gitbook/assets/1911521295.png)

So, we need to make the required changes to the existing knowledge-platform architecture to optimise the usage of DB store for Sourcing and Consumption.

### **Key Design Problems:** <a href="#design-consumptionandsourcingrepos-keydesignproblems" id="design-consumptionandsourcingrepos-keydesignproblems"></a>

1. Optimise usage of DB storage for Sourcing and Consumption.
2. Ease of publishing the data from Creation to Consumption repository.
3. Migration - For existing sunbird installations.

### **Design:** <a href="#design-consumptionandsourcingrepos-design" id="design-consumptionandsourcingrepos-design"></a>

Between Sourcing and Consumption, Sourcing require the all the Data stores always and we can reuse them for consumption as well. So, making data storage at Consumption side configurable to reuse the Sourcing DB will optimise the usage of the infrastructure.

#### Configurable Consumption DB Storage <a href="#design-consumptionandsourcingrepos-configurableconsumptiondbstorage" id="design-consumptionandsourcingrepos-configurableconsumptiondbstorage"></a>

We use the below databases to save the metadata and the data of the knowledge-platform objects. We make only consumption DB storage configurable i.e enabled or disabled. When the DB is disabled, it uses the same DB storage for Sourcing and Consumption repositories.

1. Neo4J and Elasticsearch
2. Cassandra
3. Cloud Storage

![](../../../../../../.gitbook/assets/1911554081.png)

### **Conclusion:** <a href="#design-consumptionandsourcingrepos-conclusion" id="design-consumptionandsourcingrepos-conclusion"></a>
