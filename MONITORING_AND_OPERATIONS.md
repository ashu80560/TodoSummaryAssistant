# Monitoring and Operations

## 1. Overview

The Todo Summary Assistant application uses Prometheus, Grafana, cAdvisor and Spring Boot Actuator for monitoring.

The monitoring stack runs on the EC2 instance.

```text
Todo Backend
     |
     | /actuator/prometheus
     v
 Prometheus
     |
     v
 Grafana

Docker Containers
     |
     v
 cAdvisor
     |
     v
 Prometheus
