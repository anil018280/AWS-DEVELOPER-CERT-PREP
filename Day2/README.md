
# 🌩️ AWS S3 - Complete Guide

Amazon S3 (Simple Storage Service) is a highly scalable, durable, and secure object storage service from AWS. This guide 
covers everything from core concepts to advanced features with examples and CLI commands.

---

## ✅ What is Amazon S3?

Amazon S3 provides object storage through a web service interface.

- Store any amount of data.
- Access it from anywhere on the web.
- Designed for 99.999999999% (11 9’s) durability.
- Common use cases: backup, data lake, ML, static websites, logs.

---

## 🗂️ Core Concepts

| Term        | Description                                                  |
|-------------|--------------------------------------------------------------|
| **Bucket**  | A top-level container in S3. Globally unique.                |
| **Object**  | File stored in S3 (includes data + metadata).                |
| **Key**     | Unique identifier for each object in a bucket (like path).   |
| **Versioning** | Maintain multiple versions of objects.                    |
| **Region**  | Buckets reside in specific regions for compliance/performance. |
| **Storage Classes** | Tiers based on frequency of access.                  |

---

## 🏷️ S3 Storage Classes

| Class               | Use Case                            | Availability | Cost       |
|---------------------|-------------------------------------|--------------|------------|
| **Standard**        | General purpose                     | 99.99%       | $$$        |
| **Intelligent-Tiering** | Auto cost-optimization         | 99.9–99.99%  | $$         |
| **Standard-IA**     | Infrequent access                   | 99.9%        | $          |
| **One Zone-IA**     | One AZ storage                      | 99.5%        | $          |
| **Glacier**         | Archival (minutes–hours)            | Low          | Very Low   |
| **Glacier Deep Archive** | Long-term archive (12–48 hrs) | Very Low     | Very Low   |

---

## 🔒 Security in S3

### 🔐 Encryption Options

- **SSE-S3**: Server-side, AWS manages keys.
- **SSE-KMS**: Server-side with AWS KMS customer-managed keys.
- **SSE-C**: Customer-provided key.
- **Client-Side**: You encrypt before uploading.

### 🛡 Access Control

- **IAM Policies**
- **Bucket Policies**
- **ACLs** (legacy)
- **Block Public Access** settings

### 🔍 Monitoring & Audit

- **CloudTrail**: API call logs
- **S3 Access Logs**: Detailed request logs
- **AWS Config**: Compliance auditing

---

## 🌐 Static Website Hosting with S3

1. Upload files (HTML, CSS, JS).
2. Enable static website hosting in bucket settings.
3. Set `index.html` and `error.html`.
4. Update bucket policy for public access.
5. (Optional) Use **Route 53 + CloudFront** for CDN + custom domain.

---

## 🔁 Versioning & Lifecycle Rules

- **Versioning**: Keeps old versions of objects.
- **Lifecycle Rules**:
  - Transition to Glacier after 30 days.
  - Expire/delete objects automatically.

---

## 📥 AWS CLI Hands-on

### 🪣 Create Bucket
```bash
aws s3 mb s3://my-unique-bucket-name
```

### 📤 Upload File
```bash
aws s3 cp file.txt s3://my-unique-bucket-name/
```

### 📥 Download File
```bash
aws s3 cp s3://my-unique-bucket-name/file.txt .
```

### 📜 List Files
```bash
aws s3 ls s3://my-unique-bucket-name/
```

### 🧽 Delete File
```bash
aws s3 rm s3://my-unique-bucket-name/file.txt
```

---

## 🧠 Performance & Best Practices

- Use **multipart uploads** for large files.
- Enable **Transfer Acceleration** for global uploads.
- Use **Pre-signed URLs** for secure, time-bound object access.
- Organize with **prefixes** (like virtual folders).

---

## ��️ Data Protection & Compliance

- **Durability**: 11 9’s (replicated across AZs)
- **Availability**: Up to 99.99% (Standard)
- **Compliance**: HIPAA, PCI-DSS, FedRAMP, etc.
- **Object Lock**: WORM (Write Once, Read Many)

---

## 🧩 Integrations & Use Cases

| Use Case         | Tools / Services                       |
|------------------|----------------------------------------|
| Backup & Archive | S3 + Glacier                           |
| Data Lake        | S3 + Glue + Athena                     |
| Static Websites  | S3 + CloudFront + Route 53 + ACM       |
| ML Datasets      | S3 + SageMaker                         |
| Logging          | S3 + CloudTrail/VPC Flow Logs          |
| CI/CD Artifacts  | S3 for builds, packages, and logs      |

---

## 📊 Architecture Diagram

### Static Website Hosting with CloudFront

```plaintext
User Request
    ↓
  Route 53 (DNS)
    ↓
CloudFront (CDN)
    ↓
S3 Bucket (Static Website)
```

### Server-Side Encryption with SSE-KMS

```plaintext
Upload Object
    ↓
S3 encrypts with KMS Key
    ↓
Encrypted Object Stored in S3
```

---

## ✅ Summary

| Feature            | Description                                     |
|--------------------|-------------------------------------------------|
| Fully Managed      | No infrastructure to manage                     |
| Secure             | IAM, policies, KMS encryption                   |
| Durable            | 99.999999999% durability                        |
| Scalable           | Store petabytes without provisioning            |
| Flexible Pricing   | Based on storage class and usage                |
| Common Use Cases   | Backup, logs, ML data, static websites, etc.    |

---

## 📌 Next Steps

- [ ] Practice uploading/downloading with AWS CLI
- [ ] Enable versioning and lifecycle policy
- [ ] Try hosting a static site
- [ ] Explore S3 + CloudFront + ACM + Route 53 integration
- [ ] Learn about S3 Event Notifications and triggers (e.g., Lambda)

---

