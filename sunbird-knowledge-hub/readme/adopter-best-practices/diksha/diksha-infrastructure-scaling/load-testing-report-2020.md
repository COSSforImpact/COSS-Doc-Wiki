---
icon: elementor
---

# Load Testing Report (2020)

{% embed url="https://docs.google.com/presentation/d/1LZXiQ-4ZTjmBvhVodbKXhYm9__k7KOcz8_TjWpNezTM/edit?usp=sharing" %}

### Overview

The document provides the **load test results for the Diksha R4.9 platform**, covering several key performance metrics, configurations, and backend service utilizations. Below are the major sections and their details:

***

**1. List of APIs Tested**

The document lists a comprehensive set of APIs tested during the load tests. These APIs serve a wide range of functionalities, including:

* User profile retrieval (multiple versions).
* Course-related actions (e.g., hierarchy, enrollment, and batch search).
* Content-related operations (e.g., reading and updating content state).
* Device management (e.g., device registration and profiles).
* Authentication flows (e.g., login and token refresh).
* Miscellaneous features like telemetry, consent management, and notifications.

***

**2. HPA (Horizontal Pod Autoscaler) Configuration Details**

Key configurations and observed metrics for various services during the test:

* **Pod scaling**: Services dynamically scaled between predefined minimum and maximum pod counts.
* **CPU and Memory limits**: Each service had specific CPU and memory limits set, with actual usage observed during testing.
* **Key observations**:
  * **Learner Service**: Maximum CPU usage was 1.717 cores, and memory usage was 651 MiB.
  * **Telemetry Service**: Maximum CPU usage was close to its limit at 0.799 cores.
  * **Analytics Service**: High memory usage of 1.10 GiB.
  * **Admin Utility**: 1.0 core CPU usage and 722 MiB memory.
  * **Ingress services**: Low CPU and memory utilization for both private and public ingress controllers.

***

**3. Soak Test Results**

The soak test measured response times, throughput, and latencies for various APIs under sustained loads. Key highlights include:

* **Performance Metrics**:
  * Average, minimum, and maximum response times (in milliseconds).
  * 95th and 99th percentile response times to gauge high-latency outliers.
  * Throughput rates (requests per second) for each API.
* **Examples**:
  * `readContent`: Average response time of 11.46 ms, with a throughput of 282.08 requests/sec.
  * `sendTelemetry`: Average response time of 46.56 ms, with a high throughput of 6860.58 requests/sec.
  * `getUserProfileV5`: Average response time of 115.96 ms and throughput of 1726.71 requests/sec.
  * `login`: High average response time of 409.2 ms.
* **Peak Requests**:
  * Maximum requests per second reached: **24,037**.
  * Average requests per second: **16,265**.

***

**4. Backend Service Usage**

The backend infrastructure and resource usage were detailed, highlighting:

* **Database and search systems**:
  * **Cassandra**: 72.40% CPU usage, with 14.168 GB memory usage on 7 nodes.
  * **ElasticSearch (Learning and Knowledge)**: High memory utilization (28.557 GB and 19.695 GB, respectively).
* **Other services**:
  * **Redis**: Low CPU usage but significant memory usage (24.06 GB for one instance).
  * **Kafka**: Moderate CPU (58.47%) and memory (5.995 GB).
  * **Keycloak**: Nearly 100% CPU usage, indicating high stress.

***

#### **Conclusion**

The report offers a detailed overview of Diksha R4.9's load-handling capabilities. It identifies areas of high resource utilization (e.g., Keycloak and Cassandra) and provides critical insights into API performance under load. The results demonstrate the platform's scalability and potential bottlenecks for optimization in specific services.

### Key Questions Answered

#### **API Performance**

1. What APIs were tested as part of the Diksha R4.9 load test?
2. What is the average, minimum, and maximum response time for each API tested?
3. What are the 95th and 99th percentile response times for the APIs?
4. What is the throughput (requests per second) of each API?
5. Which APIs had the highest and lowest response times during the test?
6. What were the maximum and average requests per second achieved during the test?

***

#### **HPA Configuration and Resource Usage**

7. What are the Horizontal Pod Autoscaler (HPA) configurations for each service?
8. How many pods were allocated for each service, and how many were used during peak usage?
9. What were the CPU and memory limits set for each service?
10. What were the actual CPU and memory usages for each service during the load test?
11. Which services experienced the highest resource utilization (CPU and memory)?

***

#### **Backend Service Performance**

12. What backend systems were used in the test (e.g., Cassandra, ElasticSearch)?
13. What were the CPU and memory configurations of the backend nodes?
14. How much CPU and memory were utilized by backend systems like Cassandra, Redis, and Keycloak?
15. Which backend service had the highest CPU or memory utilization?

***

#### **Scalability and Stability**

16. What were the minimum and maximum pod counts for each service during the load test?
17. Did the system scale pods effectively based on demand during the test?
18. Were there any bottlenecks identified in service resource utilization?

***

#### **Specific Features and Scenarios**

19. How did the `login` and authentication flows perform under load?
20. How efficiently did the platform handle telemetry data (e.g., sendTelemetry API)?
21. What were the performance characteristics of user profile-related APIs (e.g., `getUserProfileV5`)?
22. How did the platform handle course-related actions like content reading and course batch searches?

***

#### **System Limits and Potential Bottlenecks**

23. What were the highest and average loads the system could handle in terms of requests per second?
24. Were there any services close to their CPU or memory limits during the test?
25. Are there specific APIs or services that require optimization based on the results?

***

These questions summarize what the document explicitly answers or provides insights into.&#x20;
