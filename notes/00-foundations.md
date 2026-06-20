# 00 – AWS Foundations

These notes summarize the core AWS fundamentals that support all other services studied in this repository.

---

## 1. What is AWS?

Amazon Web Services (AWS) is a cloud computing platform that provides on‑demand access to computing power, storage, databases, networking, analytics, security, and many other managed services.

Key ideas:

- **On-demand**: provision resources only when needed.
- **Pay-as-you-go**: pay based on usage instead of buying hardware.
- **Elastic**: scale up and down quickly as demand changes.
- **Global**: deploy applications in multiple geographic locations.

---

## 2. Regions and Availability Zones (AZs)

- **Region**  
  A physical geographical area (e.g., `us-east-1`, `eu-west-1`) that contains multiple Availability Zones.
  - You choose a region based on latency, legal requirements, cost, and service availability.

- **Availability Zone (AZ)**  
  One or more data centers with independent power, cooling, and networking inside a region.
  - Usually represented as `a`, `b`, `c` (e.g., `us-east-1a`).
  - Designing across multiple AZs improves availability and fault tolerance.

- **Best practice**  
  - Deploy production workloads across **at least two AZs** when possible.
  - Keep data residency and compliance in mind when choosing a region.

---

## 3. Shared Responsibility Model

AWS and the customer share security and operational responsibilities.

- **AWS is responsible for:**
  - Security **of** the cloud:
    - physical infrastructure
    - hardware
    - networking
    - facilities
    - managed service infrastructure (e.g., RDS, S3, EC2 host level)

- **Customer is responsible for:**
  - Security **in** the cloud:
    - IAM users, roles, and permissions
    - OS hardening and patching on EC2
    - application code and configuration
    - data protection and encryption choices
    - network configuration (VPC, security groups, NACLs)

Understanding this model is crucial when deciding where to configure security controls.

---

## 4. AWS Accounts and Root User

- An **AWS account** is the basic isolation boundary for billing and resources.
- The **root user**:
  - created with the email address used when opening the account
  - has full, unrestricted permissions by default
  - should be **protected with MFA** and **not used for daily work**

Instead:

- create **IAM users** for human access
- create **IAM roles** for services and automation
- grant only the permissions needed (least privilege)

(Details on IAM are extended in `01-iam-security.md`.)

---

## 5. Core Service Categories

Some core categories used throughout this notebook:

- **Compute**
  - EC2, Lambda, ECS, EKS
- **Storage**
  - S3, EBS, Glacier
- **Networking**
  - VPC, subnets, route tables, Internet Gateway, NAT Gateway, security groups
- **Databases**
  - RDS, DynamoDB
- **Management & Governance**
  - CloudWatch, CloudTrail, CloudFormation, IAM
- **Security**
  - Security groups, NACLs, KMS, WAF

---

## 6. Basic Cost Concepts

Even in a study environment, it is important to keep cost in mind.

Main cost drivers:

- **Compute (EC2, Lambda, containers)**
  - instance type and size
  - running time
  - provisioned capacity or requests

- **Storage (S3, EBS, databases)**
  - GB stored per month
  - storage class or volume type
  - number of requests (in some services)

- **Data transfer**
  - data **into** AWS is often free
  - data **out of** AWS usually has a cost

Practical rules while studying:

- stop or terminate instances not in use
- delete unused EBS volumes and snapshots
- avoid leaving high‑cost resources running by accident
- use free tier options when available (e.g., `t3.micro`, small S3 usage)

---
