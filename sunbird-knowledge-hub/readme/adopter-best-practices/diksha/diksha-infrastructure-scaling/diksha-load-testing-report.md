---
icon: elementor
---

# DIKSHA Load Testing Report

{% embed url="https://docs.google.com/document/d/1Z6lY2zYMxbqsVvStdqogbD8XHRH9_GMM1VTWWAJ-YUc/edit?usp=sharing" %}

### Overview

**Load Test Report** details the testing and optimization of APIs in a production-like environment. Here is a comprehensive summary:

#### **1. Environment Setup**

* A production-like environment was created using 3 JMeter clusters (1 master + 4 slaves each) for API testing.
* Optimization strategies were implemented to ensure performance under scaling and varying conditions.

***

#### **2. Test Results**

**2.1 Individual API Benchmarks**

* Benchmarked performance for individual APIs with 1, 2, and 3 servers.
* Optimizations included:
  * **Caching:** Redis was used for read API optimization.
  * Horizontal scaling: Tests confirmed scalability for different server counts.
  * Direct API invocation bypassing proxies.

**Highlights:**

* Response times and throughput varied significantly across APIs.
* Example: `content/v1/read` achieved 4444 requests/second on 2 servers with 106ms average response time.

***

**2.2 Sequential Invocation via Proxy**

* Simulated 600 threads invoking APIs via the proxy and API manager.
* Issues identified:
  * Use of HTTP 1.0 instead of 1.1.
  * Lack of keep-alive connections.
  * Inefficient handling of `OPTIONS` calls.
  * Excessive logging.

***

**2.3 Post-Optimization Performance**

After implementing optimizations:

* Improved response times and throughput:
  * `ContentRead` improved from 981ms to 421ms (95th percentile).
  * `PageAssemble` and other APIs saw similar enhancements.
* Major changes:
  * Upgraded API manager (Kong) to version 0.10 for keep-alive connections.
  * Addressed connection timeout issues with inter-service communications.

***

**2.4 Comparison: Direct vs. Proxy Access**

* Direct API invocation outperformed proxied access.
  * Example: `ContentRead` throughput was 4600 requests/second (direct) vs. 2100 requests/second (proxied).

***

**2.5 Production-like Benchmarks**

* Conducted with production ratios (proxy, content service, and API manager replicas adjusted).
* Results indicated significant improvements in handling high loads over long durations.

***

**2.6 Long-Running Tests**

* A 9-hour test confirmed system stability and consistent throughput (\~353.94 requests/second) across APIs.

***

**2.7 Internet-Based Testing**

* Load tests were conducted from AWS and Azure environments.
* Azure and AWS yielded comparable performance with slight variations in response times.

***

**2.8 Static Content Proxy Testing**

* Benchmarked static content calls to blob storage.
* Proposed optimizations improved throughput significantly:
  * From \~1046 requests/second to 2300 requests/second using HTTP instead of HTTPS.

***

#### **Key Findings**

* Initial testing exposed issues such as inefficient connection handling and suboptimal logging.
* Optimizations led to:
  * Faster response times.
  * Higher throughput.
  * Better resource utilization.
* Remaining challenges include fine-tuning for internet-based scenarios and static content handling.

***

#### **Conclusions**

The optimizations significantly improved API performance, stability, and scalability, paving the way for robust production readiness.

### Key Questions Answered

Here are the key questions addressed by the **DIKSHA** **Load Testing Report**:

#### Environment Setup

1. What kind of environment was used for the load testing?
2. How were the JMeter clusters configured for testing?
3. What tools and configurations were used to optimize the API performance?

***

#### Individual API Performance

4. What were the performance benchmarks for individual APIs (response time, throughput)?
5. How does the throughput vary with the number of servers (1, 2, 3)?
6. What optimization strategies were applied to individual APIs (e.g., caching)?

***

#### Proxy Performance

7. How do APIs perform when invoked through a proxy and API manager?
8. What issues were identified in the proxy setup (e.g., HTTP version, keep-alive connections)?
9. What changes were made to resolve proxy-related issues?

***

#### Post-Optimization Performance

10. How did optimizations impact API response times and throughput?
11. Which specific code or configuration changes improved performance?
12. How did upgrading the API manager (Kong) affect the system?

***

#### Direct vs. Proxy API Access

13. How does direct API invocation compare to using proxies in terms of performance?
14. What are the trade-offs between direct and proxied API calls?

***

#### Production-Like Testing

15. How do APIs perform under a production-like environment and load?
16. What was the impact of increasing replicas of proxies, API managers, and content services?

***

#### Long-Running Tests

17. Is the system stable under prolonged load testing?
18. How consistent is throughput and response time over extended durations?

***

#### Internet-Based Testing

19. How do APIs perform when accessed via the internet using AWS and Azure load generators?
20. What were the differences in performance between AWS and Azure environments?

***

#### Static Content Handling

21. How does proxying static content to blob storage perform?
22. What improvements were achieved by switching from HTTPS to HTTP for static content?

***

#### General Analysis

23. What were the main bottlenecks identified during testing?
24. How did specific optimizations (e.g., reducing logging, connection management) resolve issues?
25. What are the recommendations for further improvements before production deployment?

These questions cover a broad range of performance metrics, configurations, optimizations, and findings detailed in the report.
