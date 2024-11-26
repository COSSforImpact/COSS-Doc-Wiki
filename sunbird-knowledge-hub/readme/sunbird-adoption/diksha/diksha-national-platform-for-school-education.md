---
icon: elementor
---

# DIKSHA - National Platform for School Education

{% embed url="https://docs.google.com/presentation/d/1ltyI01hb4vf4-4B0MkVm1TuJRCddTx9JoVnp1NzKqng/edit?usp=sharing" %}

### Overview

The document, "DIKSHA Architecture and Infrastructure Overview," provides a detailed breakdown of DIKSHA, a national digital platform for school education in India, focusing on its architecture, scale, and technical specifications. Key points include:

1. **Overview and Purpose**: DIKSHA (Digital Infrastructure for Knowledge Sharing) is a digital platform for school education initiated by the Ministry of Education, designed for teacher and student engagement across India. It supports multiple languages and is widely adopted across states and central educational boards.
2. **Platform Scale and Impact**: DIKSHA has been accessed extensively, with billions of learning sessions, minutes, and page hits. The platform offers a vast repository of e-content, textbooks, and courses, including initiatives like NISHTHA and NIPUN Bharat for teacher training and foundational learning.
3. **Platform Design Principles**: DIKSHA operates as a digital public good, built on principles of privacy, security, scalability, and interoperability. It follows an API-driven, data-driven, and ontology-driven design, emphasizing automation, minimalism, and configurability for diverse educational needs.
4. **Technology Stack and Building Blocks**: The document details DIKSHA's modular architecture, including:
   * **DIKSHA Portal and Apps**: Accessible via web and mobile, supporting content sourcing, creation, and consumption.
   * **Knowledge Management**: Taxonomy-based organization for content, tracking, and analytics.
   * **Observability**: Telemetry and analytics for user engagement and performance tracking.
   * **Microservices**: Uses microservices architecture, REST APIs, and caching mechanisms for performance optimization.
5. **Cloud and Infrastructure**: DIKSHA's infrastructure includes virtual machines, Kubernetes clusters, Redis caching, and a content delivery network. The document outlines specific services used and third-party integrations, including SSL, SMS gateways, and WhatsApp for notifications.
6. **Deployment and Monitoring**: DIKSHA employs Ansible for service provisioning and uses Prometheus and Grafana for monitoring. Log aggregation and microservices monitoring are facilitated across virtual machines and containers.
7. **Future Directions**: The document mentions steps for setting up DIKSHA on cloud infrastructure, including community support and open-source resources for new implementations.

This document emphasizes DIKSHA's role as a scalable, secure, and flexible infrastructure tailored to support diverse educational needs across India’s states and user communities.

### Key Questions Answered

Here are some potential questions that could be answered by the "DIKSHA Architecture and Infrastructure Overview" document:

1. **General Overview**
   * What is DIKSHA, and what is its purpose?
   * How does DIKSHA support school education in India?
   * Who manages and maintains the DIKSHA platform?
2. **Platform Adoption and Reach**
   * How widely is DIKSHA adopted across India?
   * What impact has DIKSHA had in terms of learning sessions and user engagement?
   * Which states and educational boards are integrated with DIKSHA?
3. **Platform Design and Features**
   * What are the core design principles behind DIKSHA?
   * How does DIKSHA ensure scalability, privacy, and security?
   * What are the main features of DIKSHA, including API-driven, data-driven, and ontology-driven designs?
4. **Technology and Infrastructure**
   * What technology stack does DIKSHA use?
   * How are microservices, REST APIs, and caching mechanisms implemented in DIKSHA?
   * What types of databases and data storage solutions does DIKSHA utilize?
5. **Content and Learning Resources**
   * What types of content are available on DIKSHA?
   * How does DIKSHA support multiple languages and diverse educational content?
   * What initiatives, like NISHTHA and NIPUN Bharat, are available on DIKSHA?
6. **Telemetry and Analytics**
   * How does DIKSHA track user engagement and learning outcomes?
   * What telemetry data is collected on the platform, and how is it used?
   * How do analytics features help stakeholders understand DIKSHA's impact?
7. **Deployment and Monitoring**
   * How is DIKSHA deployed across cloud and server infrastructures?
   * What tools and frameworks are used for service provisioning and deployment?
   * How are monitoring and log aggregation managed within DIKSHA?
8. **Integration with Third-Party Services**
   * What third-party services are integrated with DIKSHA?
   * How does DIKSHA utilize SMS gateways, Google reCaptcha, and WhatsApp for user interactions?
   * How does DIKSHA handle data privacy and security in third-party integrations?
9. **Future Directions and Scalability**
   * What steps are suggested for new organizations looking to adopt DIKSHA?
   * How can DIKSHA be set up and configured on cloud infrastructure?
   * What is DIKSHA's approach for scalability and supporting new educational initiatives?
10. **Community and Support**
    * How can developers and organizations access DIKSHA's open-source resources?
    * What support is available for technical queries related to DIKSHA?
    * How does DIKSHA leverage the Sunbird community for ongoing development?

These questions cover the document's focus on DIKSHA's purpose, design, technical architecture, reach, analytics, integrations, and future directions.
