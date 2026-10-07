# AWS Setup

## 1. AWS Region
- AWS Region: `ap-south-1` (Mumbai)
- RDS Availability Zone: `ap-south-1b`

## 2. EC2 Instance
- EC2 is used to host the application and monitoring stack.
- Docker is installed on EC2.
- Frontend, backend, Prometheus, Grafana and cAdvisor run on EC2.

## 3. Amazon RDS MySQL
- RDS DB Identifier: `task-database`
- Engine: MySQL Community
- Instance Class: `db.t4g.micro`
- Database Name: `todo_db`
- Port: `3306`
- Backend connects to RDS using environment variables.

## 4. EC2 to RDS Connectivity
- The backend running on EC2 connects to the RDS MySQL database.
- RDS MySQL traffic uses TCP port `3306`.
- RDS security group is configured to allow database access from the EC2 environment.
- Database credentials are externalized and are not committed to Git.

## 5. Docker Containers
The application is deployed using separate containers:

- `todo-backend` → port `8080`
- `todo-frontend` → port `3001`
- `prometheus` → port `9090`
- `grafana` → port `3000`
- `cadvisor` → port `8081`

## 6. Amazon ECR
Two ECR repositories were created:

- `todo-summary-assistant-backend`
- `todo-summary-assistant-frontend`

ECR Registry:

`190512372294.dkr.ecr.ap-south-1.amazonaws.com`

Docker images are built by GitHub Actions and pushed to ECR before deployment to EC2.

## 7. EC2 IAM Role
IAM role created for the EC2 instance:

`TodoSummaryAssistant-EC2-Role`

- The role is attached to the EC2 instance.
- EC2 uses the IAM role instead of storing AWS access keys on the server.
- The trust relationship allows the EC2 service to assume the role.

## 8. GitHub Actions IAM Role and OIDC
IAM role created for GitHub Actions:

`TodoSummaryAssistant-GitHubActions-Role`

GitHub OIDC provider:

`token.actions.githubusercontent.com`

Repository:

`ashu80560/TodoSummaryAssistant`

The trust policy restricts the role to the required GitHub repository/branch.

GitHub Actions uses OIDC to authenticate with AWS without storing long-lived AWS access keys.

## 9. CI/CD Deployment
The deployment flow is:

```text
GitHub Push
     ↓
GitHub Actions
     ↓
Build + Test
     ↓
Docker Image Build
     ↓
Amazon ECR
     ↓
EC2
     ↓
Docker Container Deployment
     ↓
Health Check
