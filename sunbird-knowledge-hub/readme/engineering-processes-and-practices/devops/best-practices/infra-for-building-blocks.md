---
icon: elementor
---

# Infra for Building Blocks

### Overview

#### Shared Resource Model

1. **Features**:
   * Multi-tenancy with isolated Kubernetes namespaces for each BB.
   * Shared databases with configurable keyspaces, indices, and clusters.
   * Centralized services:
     * Shared Keycloak for authentication.
     * Shared data pipeline with dedicated Kafka topics.
     * Common CI/CD infrastructure and monitoring tools (Grafana, logging).
   * Simplifies hotfix development and integration into existing systems.
   * Enhances configurability, aiding adoption.
2. **Disadvantages**:
   * Precise usage costs are challenging to calculate.
   * Maintenance or failures in shared infrastructure can impact all BBs.

#### Transition Approach

* Use current infrastructure until dependency on specific BB versions arises.
* Introduce namespace-specific configurations for diverging versions.

#### Next Steps

* **DevOps Team**:
  * Facilitate CI/CD migration to Kubernetes.
  * Implement namespace-specific setups and enhance security.
  * Manage shared infrastructure and monitoring tools.
* **Development Team**:
  * Ensure service configurability for namespaces, keyspaces, and APIs.
  * Segregate codebases, deployment, and monitoring tools for each BB.

#### Performance Benchmarking

* Leverage existing environments for load testing.
* Establish separate, cost-efficient environments for benchmarking as needed.

#### Independent Environments

* Increased resource and maintenance costs.
* Independent setups for monitoring, logging, and best-practice infrastructure provisioning.

This proposal emphasizes scalability, configurability, and operational efficiency through shared resources while addressing the challenges of cost and maintenance in shared and independent setups.

### Key Questions Answered

#### Shared Resource Model

1. What is the proposed shared infrastructure model for Sunbird BB?
2. How does the shared resource model use Kubernetes for multi-tenancy?
3. What are the advantages of using a shared database and data pipeline infrastructure?
4. How can individual BBs configure their services within the shared model?
5. What are the challenges or disadvantages of a shared resource model?

#### Transition from Current to Proposed State

6. How can BBs transition from the current infrastructure to the proposed shared model?
7. What should be done if BB versions become incompatible in the shared infrastructure?
8. How can teams enable configurability for shared resources like keyspaces and topics?

#### DevOps and Development Responsibilities

9. What are the responsibilities of the DevOps team in implementing the shared resource model?
10. What are the specific configurations required for namespaces, builds, and deployments?
11. What role does the Development team play in ensuring service configurability?
12. How should monitoring and logging configurations be implemented for each BB?

#### Performance and Benchmarking

13. How can the DIKSHA Loadtest environment be utilized for performance testing?
14. What are cost-efficient methods for creating performance benchmarking environments?

#### Independent Environments

15. What are the implications of using independent environments instead of shared ones?
16. How do maintenance, operations, and resource requirements differ for independent environments?
17. What are the best practices for provisioning independent infrastructure?





{% embed url="https://docs.google.com/presentation/d/1nksdEkD32n2kCRPOXiAOCA6YgxgXGLRu9S6OxrsHY5k/edit?usp=sharing" %}
