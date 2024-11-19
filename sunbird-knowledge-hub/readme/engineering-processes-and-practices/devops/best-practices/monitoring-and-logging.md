---
icon: elementor
---

# Monitoring & Logging

{% embed url="https://drive.google.com/file/d/1tL4Fb9T5t9V65CPnDAafHVunp-LI8wlr/view?usp=sharing" %}

## **Overview**

* **Sunbird Subsystems:** Covers various functional areas like content management, collaboration tools, user authentication, data analytics, and DevOps automation.
* **Technology Stack:** Incorporates tools for monitoring, logging, data visualization, and insights generation.

#### **Monitoring Framework**

* Uses **Prometheus** for application monitoring and alerting.
* **Grafana** serves as the visualization tool for monitoring metrics.
* Persistent metric storage is achieved via Kubernetes volumes.
* Alert notifications can be configured for email or Slack.

#### **Logging Framework**

* Logs from microservices, system files, and VMs are processed through tools like FluentBit, FileBeat, and Logstash.
* ElasticSearch is used for log storage and indexing.
* Kibana facilitates log visualization and dashboard creation.

#### **Data Insights**

* Telemetry events are processed through a pipeline that extracts, deduplicates, validates, and enriches data.
* **Druid** is used for analytics storage, with visualization handled by Superset.
* Reports include trends and usage patterns like content plays, user sessions, and page views.

#### **Kubernetes Integration**

* Manages both containerized and non-containerized workloads.
* Features auto-scaling with Horizontal Pod Autoscaler and Cluster Autoscaler.
* Provides dashboards for monitoring API performance, resource usage, and scaling events.

#### **Dashboards**

* Dashboards monitor various metrics, such as system health, job availability, and log trends.
* Key exporters include Node, Redis, Kafka, and Elasticsearch.

#### **Deployment and Backup**

* Framework deployment involves Kubernetes-based monitoring and logging stacks.
* Database backup procedures include repositories for Elasticsearch, Cassandra, Redis, Neo4j, and others.

#### **Purpose**

* Enables comprehensive monitoring and logging for scalable and reliable infrastructure.
* Supports auditing, error tracking, and performance optimization across subsystems.

The document also provides repository links and emphasizes the community-driven nature of the project, encouraging contributions and reuse.

### Key Questions Answered

#### **General Overview**

1. What are the main subsystems of the Sunbird platform, and how do they interact?
2. What is the tech stack used for monitoring and logging in Sunbird?

***

#### **Monitoring**

3. What tools are used for monitoring Sunbird’s applications?
4. How are metrics stored and visualized in the monitoring framework?
5. How does Prometheus handle alerting and notifications?
6. What exporters are used in the monitoring framework (e.g., Node, Redis, Kafka)?
7. How is persistent metric storage achieved in the Kubernetes environment?

***

#### **Logging**

8. What tools are used for logging (e.g., FluentBit, FileBeat, Logstash)?
9. How are logs from containerized and non-containerized workloads collected and processed?
10. How are logs indexed and stored in Elasticsearch?
11. How does Kibana facilitate log visualization and dashboard creation?
12. What is the process for configuring log patterns and daily backups?

***

#### **Data Insights and Analytics**

13. How is telemetry data collected and processed in Sunbird?
14. What are the stages of the data pipeline for telemetry events?
15. How are reports and analytics generated using Druid and Superset?
16. What kinds of trends and patterns are visualized in the analytics framework (e.g., content plays, user sessions)?

***

#### **Kubernetes Integration**

17. How does Kubernetes handle containerized and non-containerized workloads?
18. What is the role of Horizontal Pod Autoscaler and Cluster Autoscaler in scaling services?
19. What metrics are used to trigger auto-scaling events in Kubernetes?
20. How are pending pods managed when new nodes are required?

***

#### **Dashboards and Reporting**

21. What key metrics are monitored in the dashboards?
22. How are errors and successes in API requests tracked and visualized?
23. What are the available reports for monitoring and alerts (e.g., Exhaust Reports, Collection Summary)?
24. How are job statuses (e.g., availability, success, failure) tracked in the pipeline?

***

#### **Deployment**

25. What are the steps for deploying the monitoring and logging stacks?
26. How is the monitoring stack integrated with Kubernetes nodes?
27. How is Elasticsearch provisioned for logging purposes?
28. What tools are used for log collection and visualization in non-containerized workloads?
29. How are dashboards set up in Grafana for monitoring?

***

#### **Backup and Data Management**

30. How are database backups managed for various components (e.g., Cassandra, Redis, Neo4j)?
31. What links are provided for accessing backup configurations?
32. How does the system ensure log rotation and backup?

***

#### **Additional Information**

33. How can users contribute to the Sunbird project?
34. What are the community resources for monitoring and logging frameworks?

***

These questions cover the technical implementation and operational insights into monitoring, logging, scaling, and infrastructure management for the Sunbird platform.
