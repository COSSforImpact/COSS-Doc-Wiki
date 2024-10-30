---
icon: elementor
---

# Sunbird Tech Architechture

{% embed url="https://docs.google.com/presentation/d/1Yg80oJxqA9SyI46FoSA9fFAu6PF_v7jbc-WQ7aa0Wkk/edit?usp=sharing" %}

### Overview:-

This page gives an overview of Sunbird's technical infrastructure, designed to facilitate knowledge sharing. Key elements of the architecture include:

1. Subsystems & Services: Sunbird operates using various subsystems such as microservices, a data pipeline, and a reporting architecture.
2. Layered Platform: It consists of several layers, including mobile apps, portals, content management, taxonomy, user and organization services, and recommendation systems. This layered structure allows flexibility for different types of users like learners, teachers, and administrators.
3. Microservices Architecture: Sunbird uses a microservices approach, with services for telemetry, workflows, and analytics. The telemetry system captures contextual information for various events, supporting extensibility for further processing.
4. Data Platform: The architecture is based on a Lambda model, handling batch and real-time processing of data. The data pipeline processes telemetry events using various stages and frameworks to ensure scalability and performance.
5. Reporting Architecture: Sunbird also has a robust reporting system that integrates analytics and data summarization. This architecture supports scalability and high throughput, processing up to 1.5 billion events per day across clusters managed with Apache Kafka, Flink, Spark, and Druid.

In essence, Sunbird's technical architecture is built around scalability, modular services, and a robust data pipeline to support large-scale data collection and analysis.

### Key Questions Answered:-

1. What is Sunbird's overall technical architecture for knowledge sharing?
2. What subsystems and services does Sunbird provide?
3. What are the main components of Sunbird's microservices architecture?
4. How is data processed and managed within Sunbird's platform?
5. What is the purpose and function of Sunbird's telemetry system?
6. How does Sunbird's Lambda architecture work for data handling?
7. What kind of data processing pipelines does Sunbird use?
8. How does Sunbird handle large-scale data events?
9. What is the capacity of the Sunbird data processing infrastructure?
10. What clusters and servers are used in Sunbird for data ingestion and processing?
11. What analytics and reporting capabilities are integrated within Sunbird?
12. What are the design elements of Sunbird's data platform?
13. How does Sunbird handle real-time and batch processing for large volumes of data?
14. What scalability features are built into the Sunbird architecture to handle billions of events daily?
15. What is the role of Kafka, Flink, Spark, and Druid in Sunbird's architecture?
16. How is data summarization and telemetry used in Sunbird to improve query performance?
17. What are the key challenges that Sunbird's technical architecture addresses in terms of data management and knowledge sharing?
18. How are specific use cases handled by Sunbird's infrastructure (e.g., learner, teacher, admin workflows)?
19. What functional modules are integrated within the Sunbird platform?
20. How does Sunbird ensure high reliability and performance in its data clusters?
