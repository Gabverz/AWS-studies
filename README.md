# ☁️ AWS Studies

Personal repository dedicated to documenting my studies and hands-on
practice with Amazon Web Services (AWS).

---

## 📌 About This Repository

This repo covers key AWS services, concepts, and practical examples
explored throughout my learning journey. The focus is on understanding
core infrastructure and storage tools commonly used in real-world
cloud environments.

---

## 🔐 Initial AWS Setup & Security

Before using EC2, S3, EBS or any other AWS service, it is important to
configure your account with security and cost control in mind.

### IAM (Identity and Access Management)

AWS IAM is the service used to manage users, groups, roles and
permissions in your AWS account.

Key concepts:

- **Root account**:  
  The root user is the account owner (email used to create AWS). It has
  full, unrestricted access to everything.  
  - Use it only for a few administrative tasks (e.g., billing setup, account
    closure).
  - Do **not** use the root account for daily operations.

- **IAM users**:  
  Individual identities created inside the account, each with its own
  credentials (password, access keys, etc.).  
  - Create one IAM user for yourself and use it for day-to-day work.
  - Grant only the permissions needed (principle of least privilege).

- **IAM groups**:  
  Collections of IAM users that share the same permissions.  
  - Instead of attaching policies directly to each user, create groups
    (e.g., `Administrators`, `Developers`, `ReadOnly`) and attach policies
    to the groups.
  - Add users to these groups to manage permissions more easily.

- **IAM policies**:  
  JSON documents that define **what actions** are allowed or denied, **on
  which resources**, and under **which conditions**.  
  - You can use AWS managed policies (predefined by AWS) or create
    customer-managed policies.
  - Attach policies to users, groups, or roles.

### MFA (Multi-Factor Authentication)

Multi-Factor Authentication adds an extra layer of security by requiring
a second factor (like a code from an authenticator app) in addition to
your password.

- Always **enable MFA** on the **root account**.
- Enable MFA on IAM users that have console access, especially
  those with high privileges.
- This helps to protect your account even if your password is leaked.

### Best Practices for Account Setup

- Create an **IAM admin user** (or an `Administrators` group) with the
  necessary permissions.
- Use the root account only for:
  - Enabling MFA on the root user
  - Changing billing settings
  - A few rare, account-level tasks
- Use IAM users and roles for:
  - Daily management
  - Running applications and automation
- Regularly review permissions to avoid granting more access than needed.

---

## 💰 Cost Awareness & Optimization Basics

AWS uses a **pay-as-you-go** pricing model: you pay for what you
provision and consume. Understanding cost behavior is essential from
the beginning.

### General Cost Principles

- **Compute (EC2)**:  
  Billed mainly by instance type, size, and running time (per second or
  per hour, depending on the type).
- **Storage (S3, EBS)**:  
  Billed by GB per month stored, plus possible request and data transfer
  costs.
- **Data transfer**:  
  Usually free into AWS, but outbound traffic (data going out of AWS)
  often incurs costs.

### EC2 Costs and Instance Choices

- **On-Demand Instances**:  
  Flexible, no long-term commitment, pay for what you use. Good for
  learning and variable workloads.
- **Reserved / Savings Plans** (more advanced concept):  
  Lower prices in exchange for a time commitment (not always needed for
  study environments).
- **Spot Instances**:  
  Cheaper, but with lower availability guarantees. AWS can interrupt
  them when capacity is needed elsewhere.

When you notice that an instance is **underutilized** (for example, CPU
and memory are consistently very low), you can:

- **Right-size**:  
  Move to a **smaller instance type** to reduce costs.
- **Change instance family**:  
  Move to a cheaper family that matches your performance and availability
  needs.
- **Shut down when not in use**:  
  Stop dev/test instances when you are not actively using them to avoid
  unnecessary charges.

### S3 and EBS Cost Behavior

- **Amazon S3**:  
  - You pay for the amount of data stored (GB/month), requests, and some
    data transfer operations.
  - Different **storage classes** (e.g., Standard, Infrequent Access,
    Glacier) offer different prices and availability levels.
  - You can move rarely accessed data to a **cheaper storage class**
    to save costs, accepting higher access latency or retrieval fees.

- **Amazon EBS**:  
  - You pay for **provisioned storage** (size and type of the volume)
    and sometimes for provisioned IOPS.
  - Even if the attached EC2 instance is **stopped**, EBS volumes
    continue to generate costs as long as they exist.
  - You can reduce costs by:
    - Deleting unused volumes and snapshots.
    - Choosing the proper volume type (gp3, st1, etc.) based on
      performance needs.

---

## 🛠️ Services Covered

### 🖥️ Amazon EC2 (Elastic Compute Cloud)

Amazon EC2 is the compute service that allows you to create and manage
virtual servers (instances) in the AWS cloud. It offers a variety of
instance types optimized for CPU, memory, storage, or GPU workloads,
making it flexible enough to support different application needs.

**Common use cases:**
- Hosting applications and APIs  
- Running databases and test environments  
- Any workload that requires a configurable operating system

---

### 🗂️ Amazon S3 (Simple Storage Service)

Amazon S3 is an object storage service designed to store and retrieve
any amount of data from anywhere on the internet. Data is organized in
buckets and can be accessed via API, SDK, or the AWS Console, with
fine-grained permission control and support for versioning and lifecycle
policies.

**Common use cases:**
- Storing application data, logs, and backups  
- Hosting static websites and assets (images, CSS, JavaScript)  
- Data lakes and analytics pipelines

---

### 💾 Amazon EBS (Elastic Block Store)

Amazon EBS provides persistent block storage volumes that can be
attached to EC2 instances, working like virtual disks. Volumes remain
intact even after instance stops or reboots, and different volume types
are available depending on throughput and IOPS requirements.

**Common use cases:**
- File systems and relational databases  
- Low-latency storage for compute-intensive applications  
- Boot volumes for EC2 instances

---

*Studies in progress — more services, comments and examples will be added over time.*
