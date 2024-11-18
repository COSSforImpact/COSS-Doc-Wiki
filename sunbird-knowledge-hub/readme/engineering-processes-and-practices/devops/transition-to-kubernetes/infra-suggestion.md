---
icon: elementor
---

# Infra Suggestions

### Overview

This diagram illustrates the infrastructure of Sunbird. It showcases an Istio Mesh with an API Gateway (Kong) handling API calls. Each service—Portal, Learner, Content, and Telemetry—has an Envoy proxy for communication. Monitoring tools like Grafana, Prometheus, and Jaeger are integrated, ensuring observability and scalability within the microservices architecture.

<figure><img src="../../../../../.gitbook/assets/infra-Kubernetes Infra.png" alt=""><figcaption></figcaption></figure>
