---
icon: elementor
---

# Web Application Firewall

## Overview

* **Purpose**: WAF offers centralized protection for web applications against common vulnerabilities and exploits, such as SQL injection, cross-site scripting, and HTTP anomalies.
* **Deployment**: Compatible with **Azure Application Gateway**, **Azure Front Door**, and **Azure CDN**.
* **Protection Capabilities**:
  * Custom rules for specific needs.
  * Geo-filtering to block/allow traffic by regions.
  * Bot mitigation and inspection of JSON/XML in request bodies.

#### WAF Operating Modes

1. **Detection Mode**:
   * Logs and monitors threats without blocking traffic.
   * Suitable for diagnostics and testing phases.
2. **Prevention Mode**:
   * Blocks identified threats and records them in logs.
   * Displays "403 unauthorized" for blocked requests.

#### Rollout Plan

* Enable WAF in detection mode for initial environments (dev and staging).
* Test API throughput impacts during load testing.
* Benchmark WAF and DDoS configurations in production.

#### Performance Metrics

* **Testing Scenarios**: Compared various setups (with/without WAF, Azure Firewall, App Gateway).
* Results indicate trade-offs between throughput (TPS), resource usage (CPU, nodes), and infrastructure scalability.
* Example: Total Requests, Avg TPS, and CPU usage were highest when App Gateway autoscaling was enabled.

#### Costs

* **Application Gateway + WAF**:
  * Fixed cost: ₹26,487.
  * Additional charges based on capacity usage (₹790 per unit).
* **Azure Firewall**:
  * Fixed cost: ₹95,911.
  * Data processing costs: ₹1,230 per TB (307 GB processed in one test scenario).

#### Action Items and Observations

* Roll out WAF and DDoS gradually, starting with less critical environments.
* Evaluate how WAF handles outgoing traffic and client-side vulnerabilities.
* Conduct extensive load testing to identify throughput impacts and optimize configurations.

This document is a comprehensive guide to deploying and optimizing WAF in a scalable, cost-effective manner while ensuring robust web application security.

### Key Questions Answered

#### General Understanding of WAF

1. What is a Web Application Firewall (WAF)?
2. What types of vulnerabilities does WAF protect against?
3. What platforms and services can WAF be deployed with (e.g., Azure Application Gateway, Azure Front Door)?
4. What features does WAF offer (e.g., custom rules, geo-filtering, bot mitigation)?

#### Modes of Operation

5. What are the different modes of WAF operation (Detection vs. Prevention)?
6. What is the behavior of WAF in Detection mode?
7. How does WAF operate in Prevention mode, and what happens when a threat is detected?

#### Rollout and Testing

8. What is the rollout plan for implementing WAF across environments (e.g., dev, staging, production)?
9. How should load tests be conducted to benchmark API throughput with WAF enabled?
10. What are the steps to deploy WAF in detection mode and later switch to prevention mode?

#### Performance and Metrics

11. What are the performance impacts of enabling WAF, Azure Firewall, and App Gateway together?
12. How does autoscaling affect throughput, total requests, and resource usage?
13. How do different configurations (manual instance counts, autoscaling) impact average and maximum TPS?

#### Cost and Resource Usage

14. What are the fixed and variable costs of deploying WAF and Azure Firewall?
15. How does capacity usage and data processing affect the overall cost of the setup?

#### Security and Best Practices

16. Can WAF inspect outgoing traffic or address untrusted client-side content?
17. How does WAF help protect against common web vulnerabilities like SQL injection, cross-site scripting, and HTTP anomalies?
18. What best practices should be followed for enabling and testing WAF with Azure?

These questions cover the technical, operational, and financial aspects of deploying and optimizing WAF in a cloud-based environment.

{% embed url="https://docs.google.com/presentation/d/1xLtuhY-I5wcU4rW2DY3-6Z0co2MejJjm0BMRGOndybc/edit?usp=sharing" %}
