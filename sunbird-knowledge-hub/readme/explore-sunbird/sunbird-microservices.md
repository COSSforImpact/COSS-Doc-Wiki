---
icon: elementor
---

# Sunbird Microservices

{% embed url="https://docs.google.com/presentation/d/1p8OOrmjdinrP6zNfYpNTYf5eleTKZyXXktsRh2l21v8/edit?usp=sharing" %}

### Overview:-

This page discusses the architecture and implementation of microservices in the Sunbird platform. Here's a summary of the key points:

1. Microservices Overview: A microservice serves a specific program function, such as content management, and is accessed through APIs. Each API has a defined contract, which is an agreement on its capabilities, ensuring clear communication between services.
2. Microservice Features:

* Microservices are loosely coupled, highly maintainable, and independently deployable.
* They are organized around business capabilities and can be owned by small, autonomous teams.
* Microservices are classified into various domains such as content management, taxonomy, assessments, learning management, and notifications.

3. Platform Microservices:

* Examples include services for content management, DIAL registry (for linking physical and digital resources via QR codes), and sourcing projects.
* The platform also includes a registry of users, organizations, and geographic locations, along with services for digital credentialing and notifications.

4. Infrastructure Microservices:

* These manage data services, device registries, API tokens, and reporting.
* They provide essential services such as collecting telemetry data, issuing API tokens, and

managing reports for the platform.

5. Consumption of Microservices:

* Microservices are used across different interfaces like mobile apps, desktop apps, and web portals.
* These interfaces consume services related to user management, content, assessments, data tracking, and notifications.

6. Collaboration and Interaction:

* Microservices facilitate collaboration, such as group management, discussion forums, and interaction through chatbots.

7. Administration and Setup Services:

* There are additional services to support administrative tasks like notifications, form management, and location setup.
* Bulk upload services and APIs for setting up forms are also part of the system.

8. Microservice Usage in Education:

* The document highlights that microservices are the backbone of the DIKSHA platform, supporting educational services for content delivery, credentialing, user management, and collaboration.
* APIs and microservices offer states and organizations the ability to integrate and extend the platform's capabilities.

9. Federated System:

* The document emphasizes the use of federated IDs and interoperable APIs, creating a

centralized system for authentication, attestation, and consent-based data access.

The overall theme revolves around the modularity, scalability, and interoperability of Sunbird's microservice architecture, ensuring that various educational and administrative tasks can be efficiently managed and extended across different ecosystems.

### Key Questions Answered:-

1. What is a microservice, and how is it defined in the Sunbird context?
2. What are the characteristics of microservices in the Sunbird architecture?
3. How are microservices organized in the Sunbird platform?
4. What are the primary microservices available in the Sunbird platform?
5. What APIs are associated with content management in Sunbird?
6. How does the Sunbird platform handle user and organization registries?
7. What is the DIAL registry, and how is it used in the Sunbird system?
8. What services are available for assessments in Sunbird?
9. How does the Sunbird platform manage digital credentials and certifications?
10. What APIs are available for sending notifications in Sunbird?
11. How are geographic locations managed within Sunbird?
12. What microservices are available for managing learning content and progress tracking?
13. What infrastructure microservices are included in the Sunbird platform?
14. What is the purpose of the API manager in Sunbird?
15. How does Sunbird facilitate group management and collaboration between users?
16. What tools and APIs does Sunbird provide for device registration and data services?
17. How does Sunbird's architecture support modularity and scalability?
18. What administrative services are available for managing Sunbird users and organizations?
19. What types of reports and dashboards are available in the Sunbird platform?
20. How can external applications interact with Sunbird's microservices and APIs?
21. What are the key consumption patterns for Sunbird microservices across different platforms (mobile, desktop, web)?
22. How does Sunbird support the reuse of content and contributions from different organizations?
23. What are the federation and authentication capabilities in the Sunbird platform?
24. How does Sunbird manage data export and import through its microservices?
25. How are learning interactions and administrative tasks handled by Sunbird microservices?
26. What is the role of federated IDs in the Sunbird ecosystem?
27. What collaboration features, such as discussion forums and chatbots, are available within Sunbird?
