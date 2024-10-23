---
icon: elementor
---

# Design for a lightweight healthcheck api in portal and content service.

**Problem Statement**

Currently, the health check API is checking that the dependent service is healthier or not to determine that this service is healthy

ex:

* In the portal, the health check is trying to determine that the following service is up and running.\
  1\. Cassandra DB\
  2\. Learner Service\
  3\. Content Service
* In the Content Service, the health check is trying to determine that the following service is up and running.\
  1\. Cassandra DB\
  2\. KnowledgePlatform Service\
  3\. Learner ServiceProposed
