# Todo Summary Assistant

A full-stack Todo application with an AI-powered summary workflow, deployed using Docker, AWS, and GitHub Actions CI/CD.

## Project Overview

Todo Summary Assistant is a full-stack application consisting of:

- React frontend
- Spring Boot backend
- MySQL database hosted on Amazon RDS
- Docker containers for frontend and backend
- Amazon EC2 for application hosting
- Amazon ECR for Docker image storage
- GitHub Actions for CI/CD
- Prometheus for metrics collection
- Grafana for monitoring and visualization
- cAdvisor for Docker container and host metrics

The application is deployed on AWS and automatically updated through the CI/CD pipeline.

---

## Architecture

```text
                         GitHub Repository
                                |
                                v
                        GitHub Actions
                                |
                    Build / Test / Docker
                                |
                                v
                         Amazon ECR
                       /             \
                      /               \
                     v                 v
          Backend Docker Image    Frontend Docker Image
                     \                 /
                      \               /
                       v             v
                         Amazon EC2
                  +-----------------------+
                  |                       |
                  |  Frontend :3001       |
                  |  Backend  :8080       |
                  |                       |
                  |  Prometheus :9090     |
                  |  Grafana :3000        |
                  |  cAdvisor :8081      |
                  |                       |
                  +-----------+-----------+
                              |
                              | MySQL :3306
                              v
                         Amazon RDS
                         MySQL Database
