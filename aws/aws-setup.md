# AWS Setup

## Overview

The Todo Summary Assistant application is deployed on AWS using Amazon EC2, Amazon RDS, Amazon ECR and IAM.

The architecture separates application hosting from database hosting.

```text
GitHub
   |
   v
GitHub Actions
   |
   v
Amazon ECR
   |
   v
Amazon EC2
   |
   | MySQL :3306
   v
Amazon RDS
