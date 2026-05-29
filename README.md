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
  - Use it only for a few administrative tasks (e.g., billing setup,
    account closure).
  - Do **not** use the root account for daily operations.

- **IAM users**:  
  Individual identities created inside the account, each with its own
  credentials (password, access keys, etc.).  
  - Create one IAM user for yourself and use it for day-to-day work.
  - Grant only the permissions needed (principle of least privilege).

- **IAM groups**:  
  Collections of IAM users that share the same permissions.  
  - Instead of attaching policies directly to each user, create groups
    (e.g., `Administrators`, `Developers`, `ReadOnly`) and attach
    policies to the groups.
  - Add users to these groups to manage permissions more easily.

- **IAM policies**:  
  JSON documents that define **what actions** are allowed or denied,
  **on which resources**, and under **which conditions**.  
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
  Billed mainly by instance type, size, and running time (per second
  or per hour, depending on the type).
- **Storage (S3, EBS)**:  
  Billed by GB per month stored, plus possible request and data
  transfer costs.
- **Data transfer**:  
  Usually free into AWS, but outbound traffic (data going out of AWS)
  often incurs costs.

### EC2 Costs and Instance Choices

- **On-Demand Instances**:  
  Flexible, no long-term commitment, pay for what you use. Good for
  learning and variable workloads.
- **Reserved / Savings Plans**:  
  Lower prices in exchange for a time commitment (not always needed
  for study environments).
- **Spot Instances**:  
  Cheaper, but with lower availability guarantees. AWS can interrupt
  them when capacity is needed elsewhere.

When you notice that an instance is **underutilized** (for example,
CPU and memory are consistently very low), you can:

- **Right-size**: Move to a **smaller instance type** to reduce costs.
- **Change instance family**: Move to a cheaper family that matches
  your performance and availability needs.
- **Shut down when not in use**: Stop dev/test instances when you are
  not actively using them to avoid unnecessary charges.

### S3 and EBS Cost Behavior

- **Amazon S3**:  
  - You pay for the amount of data stored (GB/month), requests, and
    some data transfer operations.
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

#### What is an EC2 Instance?

An EC2 instance is a **virtual machine running in the AWS cloud**.
It behaves like a physical server: it has an operating system, CPU,
memory, storage, and network access. The key difference is that you
can provision it in seconds, scale it up or down, and pay only for
what you use.

Each instance runs inside a **VPC (Virtual Private Cloud)** and is
associated with a subnet, security groups, and optionally an IAM role.

---

#### Instance Types

AWS organizes instance types into **families**, each optimized for a
different purpose:

| Family | Optimized for | Examples |
|---|---|---|
| General Purpose | Balanced CPU/memory | `t3.micro`, `m6i.large` |
| Compute Optimized | High CPU | `c6i.large`, `c7g.xlarge` |
| Memory Optimized | Large in-memory workloads | `r6i.large`, `x2idn.32xlarge` |
| Storage Optimized | High I/O throughput | `i4i.large`, `d3.xlarge` |
| Accelerated Computing | GPU / ML workloads | `p4d.24xlarge`, `g5.xlarge` |

> For learning and dev environments, **t3.micro** or **t3.small** are
> great starting points and are often covered by the AWS Free Tier.

---

#### How to Create an EC2 Instance

You can create an instance via the **AWS Console**, **AWS CLI**, or
**Infrastructure as Code (IaC)** tools like CloudFormation or Terraform.

**Via AWS Console (step by step):**

1. Go to **EC2 → Instances → Launch Instances**.
2. Fill in the required parameters (detailed below).
3. Review and click **Launch Instance**.

**Key parameters to configure:**

- **Name and tags**:  
  Give your instance a meaningful name and add tags for organization
  (e.g., `Environment: dev`, `Project: aws-studies`).

- **Amazon Machine Image (AMI)**:  
  The operating system and pre-installed software that your instance
  will run. Common choices:
  - Amazon Linux 2023 (AWS-optimized, free tier eligible)
  - Ubuntu 22.04 LTS
  - Windows Server

- **Instance type**:  
  Defines the CPU and memory available to your instance.
  Start with `t3.micro` for learning purposes.

- **Key pair (login)**:  
  A key pair is used to authenticate SSH access (Linux) or decrypt
  the administrator password (Windows).
  - Create a new key pair and **download the `.pem` file**.
  - Store it securely — AWS does not store your private key.

- **Network settings**:  
  - Select or create a **VPC** and a **subnet**.
  - Choose whether to assign a **public IP** (needed if you want to
    access the instance from the internet).
  - Assign one or more **Security Groups** (see below).

- **Storage (root volume)**:  
  The instance comes with a root EBS volume. You can adjust the size
  and volume type (gp3 is the default and recommended starting point).
  - Additional EBS volumes can be attached if needed.

- **Advanced details (optional)**:  
  - **IAM instance profile**: Attach an IAM role so the instance can
    interact with other AWS services (e.g., read from S3) without
    hardcoding credentials.
  - **User data**: A script that runs automatically when the instance
    starts. Useful for installing packages, configuring the environment,
    etc.

---

#### Security: Security Groups

A **Security Group** acts as a virtual firewall for your instance.
It controls **inbound** (incoming) and **outbound** (outgoing) traffic
at the instance level.

Key rules to know:

- Security groups are **stateful**: if you allow inbound traffic on a
  port, the response traffic is automatically allowed outbound.
- Rules are **allow-only**: you cannot create deny rules (use Network
  ACLs for that).
- You can reference other security groups in rules instead of IP
  ranges — useful for allowing EC2 instances to talk to RDS, for
  example.

**Common inbound rules for a Linux instance:**

| Type | Protocol | Port | Source | Purpose |
|---|---|---|---|---|
| SSH | TCP | 22 | Your IP | Remote terminal access |
| HTTP | TCP | 80 | 0.0.0.0/0 | Web traffic |
| HTTPS | TCP | 443 | 0.0.0.0/0 | Secure web traffic |

> Always restrict SSH access to **your IP only** (`My IP` option in
> the console). Never leave port 22 open to `0.0.0.0/0`.

---

#### How to Access an EC2 Instance

**Linux instances (SSH):**

```bash
# Make sure the .pem file has correct permissions
chmod 400 your-key.pem

# Connect via SSH
ssh -i "your-key.pem" ec2-user@<public-ip-or-dns>
```

> The default username depends on the AMI:
> - Amazon Linux → `ec2-user`
> - Ubuntu → `ubuntu`
> - Debian → `admin`

**Windows instances (RDP):**
- Download the Remote Desktop file from the console.
- Decrypt the password using your key pair.
- Connect using any RDP client.

**AWS Session Manager (recommended alternative):**  
Session Manager allows you to access instances **without opening
port 22** and without managing key pairs, using only IAM permissions.
It is the most secure way to access instances in production
environments.

---

#### EC2 Instance Lifecycle

Understanding instance states helps avoid unnecessary costs:

| State | Description | Billed? |
|---|---|---|
| **Pending** | Instance is starting up | No |
| **Running** | Instance is active and usable | Yes |
| **Stopping** | Instance is shutting down (gracefully) | No |
| **Stopped** | Instance is off (EBS data is preserved) | Partial (EBS) |
| **Terminated** | Instance is permanently deleted | No |

> **Tip:** Stop instances when not in use. Terminate them (and
> delete associated EBS volumes) when they are no longer needed.

---

### 🗂️ Amazon S3 (Simple Storage Service)

Amazon S3 is an object storage service designed to store and retrieve
any amount of data from anywhere on the internet. Data is organized
in buckets and can be accessed via API, SDK, or the AWS Console,
with fine-grained permission control and support for versioning and
lifecycle policies.

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
