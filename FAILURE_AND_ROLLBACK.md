# Failure and Rollback

## 1. Overview

The application is deployed using GitHub Actions, Amazon ECR and Amazon EC2.

Each Docker image is tagged using the Git commit SHA so that a specific application version can be identified and redeployed if a deployment fails.

The deployment process includes a post-deployment health check.

---

## 2. Deployment Workflow

The normal deployment workflow is:

```text
Developer
    |
    v
GitHub Push
    |
    v
GitHub Actions
    |
    +--> Build Backend
    |
    +--> Run Tests
    |
    +--> Build Frontend
    |
    +--> Build Docker Images
    |
    v
Amazon ECR
    |
    v
EC2
    |
    +--> Pull New Image
    |
    +--> Stop Existing Container
    |
    +--> Start New Container
    |
    v
Health Check
    |
    +---- PASS ----> Deployment Successful
    |
    +---- FAIL ----> Failure / Rollback
