---
icon: elementor
---

# Sunbird Architecture

{% embed url="https://docs.google.com/presentation/d/1MQtwSdWxTPJQME0B1jPHyI4c8AK6cGwxTdICm5xdYuk/edit?usp=sharing" %}

### Overview:-

This page outlines the core components, approaches, and architectural design of the Sunbird platform. Here is a summary of the key points:

Core Architecture Principles:

1. Modular and API-Driven: Sunbird's architecture is built around modular, composable elements, often described as "Lego Architecture." It promotes minimalism, generalization, and a strong API-driven approach.
2. Ontology and Taxonomy-Driven: Content is organized through a graph-based ontology, with various resources like worksheets, textbooks, courses, and question banks being structured within a taxonomy graph for efficient retrieval and management.

Platform Approach: The platform is designed with several layers, including:

* User Applications: Apps tailored for different users such as learners, teachers, parents, and administrators.
* Functional Modules: These include data products, dashboards, content management, and recommendation engines.
* Core Infrastructure: Sunbird supports distributed systems through a "minimal digital spine" and telemetry services for data handling and analysis.

Knowledge Representation: Sunbird uses a Graph Engine as the core framework for knowledge representation, relying on technologies like Neo4j and ElasticSearch to manage relationships between various learning

content, such as courses and textbooks.

Sunbird LMS & OpenRAP:

* LMS: Sunbird integrates a Learning Management System (LMS) for content creation, delivery, and analytics.
* OpenRAP: Sunbird also emphasizes accessibility, allowing for offline access to content through its OpenRAP (Resource Access Point), which provides content even in low-connectivity or remote areas.

Content Framework: This section discusses the tools used to create and play content, including resource creation, textbook or course collection, and plugins for editing and playing content. The framework is built to be adaptable and modular for easy content management and sharing.

DevOps Practices:

* Infrastructure as Code: The document also touches on infrastructure automation, with automated provisioning, continuous integration, and deployment pipelines being part of its DevOps practices.
* Hands-on Installation: It provides a step-by-step guide for installing and deploying Sunbird, mentioning the requirements for cloud infrastructure, storage, and load balancers.

The document serves as both a high-level architectural overview and a practical guide to setting up the Sunbird platform for education or learning management solutions, emphasizing its open-source, modular, and highly adaptable nature.

### Key Questions Answered:-

1. What are the core principles of Sunbird's architecture?
2. How does Sunbird's modular and API-driven architecture function?
3. What is the role of ontology and taxonomy in organizing Sunbird's content?
4. How is the Sunbird platform structured in terms of layers and components?
5. What are the key functional modules and services provided by the Sunbird platform?
6. What technologies are used for Sunbird's knowledge representation and content management?
7. How does Sunbird's Learning Management System (LMS) work?
8. What is OpenRAP, and how does it enable offline content access?
9. How does Sunbird handle content creation, management, and sharing?
10. What are the main DevOps practices followed by Sunbird for infrastructure management?
11. What is the recommended hardware and infrastructure setup for deploying Sunbird?
12. How can Sunbird's platform be installed, and what are the key steps involved?
13. What tools and frameworks are available in Sunbird for creating and playing content?
14. How does Sunbird handle content distribution in low-connectivity or remote areas?
15. What data pipeline architecture is used for Sunbird's analytics platform?
16. What is the role of the Sunbird Mobile SDK in building mobile applications?
17. What are the prerequisites and steps for installing Sunbird on cloud infrastructure?
18. How does Sunbird handle continuous integration, build automation, and deployment?
19. What branching strategies are recommended for Sunbird deployments?
20. How does Sunbird manage roles, users, and organizational frameworks?
