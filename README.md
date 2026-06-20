# AWS Studies

![AWS](https://img.shields.io/badge/AWS-Studies-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![Documentation](https://img.shields.io/badge/Type-Study%20Notebook-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange?style=for-the-badge)
![Language](https://img.shields.io/badge/Docs-English-success?style=for-the-badge)

A personal repository dedicated to my AWS learning journey, organized as a digital notebook for class notes, summaries, and study progress.

---

## Overview

This repository is currently focused on documenting AWS classes in a clear, structured, and reusable way.

It is designed to:

- consolidate what I learn in each lesson
- keep a growing reference for future review
- organize concepts by topic
- build a strong foundation for future labs, exercises, and projects

At this stage, the repository is intentionally centered on **notes and study material**.

---

## What This Repository Covers

- AWS fundamentals
- IAM and security basics
- cost awareness and optimization
- EC2
- S3 and EBS
- VPC and networking
- RDS and DynamoDB
- CloudWatch and CloudTrail
- Lambda and Step Functions
- CloudFormation, Terraform, and DevOps concepts
- WAF, encryption, and other security topics

---

## Current Learning Focus

The study path in this repository follows the progression below:

1. understand the concept
2. write a clear summary
3. review the topic later
4. expand the notes with examples and best practices
5. add hands-on practice when the time comes

---

## Initial AWS Setup & Security

Before working with AWS services, it is important to understand account security and access management.

### IAM (Identity and Access Management)

IAM is the AWS service used to manage:

- users
- groups
- roles
- policies
- permissions

Best practices:

- do not use the root account for daily work
- create IAM users for regular access
- use groups to manage permissions efficiently
- apply the principle of least privilege
- prefer roles for services and automation whenever possible

### MFA (Multi-Factor Authentication)

MFA adds an extra layer of protection by requiring a second factor in addition to the password.

Best practices:

- enable MFA on the root account
- enable MFA on privileged IAM users
- use MFA whenever console access is required

### Cost Awareness

AWS follows a pay-as-you-go model, so cost control should be part of the study from the beginning.

General principles:

- stop unused EC2 instances
- right-size workloads whenever possible
- choose the appropriate storage class for the access pattern
- remove unused EBS volumes and snapshots
- monitor services that may generate unexpected charges

---

## Repository Structure

```text
aws-studies/
├── README.md
└── notes/
    ├── 00-foundations.md
    ├── 01-iam-security.md
    ├── 02-cost-management.md
    ├── 03-networking-vpc.md
    ├── 04-compute-ec2.md
    ├── 05-storage-s3-ebs.md
    ├── 06-databases-rds-dynamodb.md
    ├── 07-observability-cloudwatch-cloudtrail.md
    ├── 08-serverless-lambda-step-functions.md
    ├── 09-devops-automation.md
    └── 10-security-waf-encryption.md
```

---

## How to Use This Repository

- `README.md` works as the entry point
- `roadmap.md` shows the learning progression
- `notes/` contains the lesson summaries and explanations

The repository will evolve gradually as new AWS classes are completed.

---

## Why This Repository Exists

This repository is meant to serve two purposes:

- **Study notebook**: a clean and organized place to document AWS learning
- **Portfolio foundation**: a technical record that can later grow into labs, diagrams, and projects

---

## Roadmap

Planned next steps:

- complete the notes for the first AWS topics
- expand each file with practical examples
- add diagrams where useful
- introduce hands-on exercises later
- convert selected topics into portfolio-ready projects over time

---

*Studies in progress — more notes will be added over time.*
