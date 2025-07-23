# ✅ Day 1 - Cloud Computing, AWS Basics & Core Services

Welcome to Day 1 of my AWS Developer Associate Certification Journey.

---

## ☁️ What is Cloud Computing?

Cloud computing is the **on-demand delivery of computing services** (like servers, storage, databases, networking, software) over the **internet** with **pay-as-you-go pricing**.

> You don’t need to buy or maintain physical servers—just rent what you need.

---

### ⚡ Analogy: Cloud = Electricity
- No power plant? No problem—you use electricity and pay for what you consume.
- Cloud is similar—you rent computing resources instead of owning hardware.

---

### 🧩 Cloud Service Models

| Model | Full Form | What It Offers | Examples |
|-------|-----------|----------------|----------|
| IaaS | Infrastructure as a Service | Virtual servers, networking | AWS EC2, Azure VM |
| PaaS | Platform as a Service | Platform to run/deploy code | AWS Elastic Beanstalk |
| SaaS | Software as a Service | Ready-to-use software | Gmail, Zoom, Dropbox |

---

### ☁️ Cloud Deployment Types

| Type | Description |
|------|-------------|
| **Public Cloud** | Provided by AWS, Azure, GCP |
| **Private Cloud** | Internal cloud for one org |
| **Hybrid Cloud** | Mix of public + private |
| **Multi-Cloud** | Using more than one cloud provider |

---

### ✅ Cloud Benefits
- Scalable
- Cost-efficient
- Fast deployments
- Global reach
- Secure & Compliant
- No hardware headaches

---

## 🔰 AWS Basics

### 🏗️ What is AWS?

**Amazon Web Services (AWS)** is the world’s leading cloud platform, offering over 200 services from data centers globally.

---

### 🌎 Key AWS Concepts (Detailed)

#### 🗺️ **Region**
A **Region** is a geographical area where AWS has clusters of data centers. Each region is isolated and independent.

- Example: `us-east-1` (N. Virginia), `ap-south-1` (Mumbai)
- Always choose a region close to your users for lower latency and compliance.

---

#### 🏢 **Availability Zone (AZ)**
An AZ is one or more **physically separate data centers** within a region.

- AZs are connected by high-speed, low-latency links.
- Distribute resources across AZs for fault tolerance.

---

#### 🪣 **S3 (Simple Storage Service)**
Object storage for any type of data.

- Store unlimited files as **objects** in **buckets**
- Use cases: backup, static website hosting, logs
- Features: versioning, lifecycle policies, encryption

---

#### 🖥️ **EC2 (Elastic Compute Cloud)**
Virtual machines to run applications.

- Choose OS, CPU, RAM, and storage
- Instance types like `t2.micro` are free tier eligible
- Supports autoscaling and load balancing

---

#### 🛡️ **IAM (Identity and Access Management)**
Manages secure access to AWS services.

- Use **users**, **groups**, **roles**, and **policies**
- Apply least-privilege principle
- Use IAM roles for EC2, Lambda instead of hardcoding credentials

---

#### ⚙️ **Lambda**
Serverless compute service to run code on-demand.

- Pay only for execution time
- Event-driven: triggered by S3, API Gateway, etc.
- No need to manage servers

---

#### 📊 **CloudWatch**
Monitors AWS resources and applications.

- Collects metrics like EC2 CPU usage
- Stores logs from Lambda, ECS, etc.
- Set alarms and automate responses

---

#### 🌐 **VPC (Virtual Private Cloud)**
Your private network in AWS.

- Define subnets, IP ranges, route tables
- Use NAT Gateway, Internet Gateway
- Protect traffic with Security Groups and NACLs

---

## 🚀 Core AWS Services (Quick Recap)

| Service | Type | Description |
|--------|------|-------------|
| EC2 | Compute | Virtual servers to host applications |
| S3 | Storage | Scalable object storage |
| Lambda | Serverless | Run code without managing servers |
| IAM | Security | Manage access with users, roles, policies |
| RDS | Database (SQL) | Managed relational databases |
| DynamoDB | Database (NoSQL) | Scalable NoSQL database |
| VPC | Networking | Isolated virtual networks |
| CloudWatch | Monitoring | Metrics, logs, and alarms |

---

## ✅ Day 1 Recap Checklist

| Task | Status |
|------|--------|
| Understood Cloud Computing basics | ✅ |
| Learned AWS Core Concepts | ✅ |
| Studied detailed services like EC2, S3, Lambda | ✅ |
| Practiced S3, IAM, EC2 setup | ✅ |

---
