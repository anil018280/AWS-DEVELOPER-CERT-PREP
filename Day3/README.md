
# 🔐 AWS IAM – Complete Guide for Developers

AWS Identity and Access Management (IAM) enables you to securely manage access to AWS services and resources. It’s a 
foundational service every AWS Developer must understand.

---

## ✅ What is IAM?

IAM is used to:

- **Authenticate**: Verify identity (who are you?).
- **Authorize**: Control what the identity is allowed to do.

It helps define **who can do what to which resource**.

---

## 🧱 IAM Building Blocks

| Component         | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| **Users**         | IAM identities for individuals or applications (long-term access).          |
| **Groups**        | Collection of users sharing the same policies.                              |
| **Roles**         | Temporary access for users/services assuming a role.                        |
| **Policies**      | JSON documents defining permissions.                                        |
| **Identity Providers** | External sources like Google, Facebook, or corporate directories.      |

---

## 🔑 IAM Users vs IAM Roles

| Feature          | IAM User                         | IAM Role                                  |
|------------------|-----------------------------------|--------------------------------------------|
| Usage            | For individuals/apps              | For AWS services or federated identities   |
| Credentials      | Username + password / Access Keys | No credentials; assumed dynamically        |
| Duration         | Long-lived                        | Short-lived (temporary sessions)           |
| Best Practice    | Use per developer                 | Use for EC2, Lambda, cross-account access  |

---

## 📜 IAM Policies

IAM Policies are **JSON** documents that grant **Allow** or **Deny** access to actions on resources.

### 🧾 Example Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-bucket"
    }
  ]
}
```

### Components:

- `"Effect"`: Allow or Deny
- `"Action"`: API calls like `s3:PutObject`, `ec2:StartInstances`
- `"Resource"`: ARN (Amazon Resource Name)
- `"Condition"`: Optional filters (e.g., IP, time, MFA)

---

## 📂 IAM Policy Types

| Type                   | Description                                              |
|------------------------|----------------------------------------------------------|
| **Identity-based**     | Attached to IAM users, groups, or roles                  |
| **Resource-based**     | Attached to AWS resources like S3 buckets                |
| **Permissions boundaries** | Limits maximum permissions a user/role can have     |
| **SCP (Service Control Policies)** | Applied at Org level in AWS Organizations   |
| **Session policies**   | Temporary policies passed when assuming roles            |

---

## 🔐 Security Best Practices

✅ Use **Least Privilege** principle  
✅ Use **Roles** for applications and services (never embed credentials)  
✅ Rotate access keys regularly  
✅ **Enable MFA** (Multi-Factor Authentication)  
✅ Avoid using the **root user**  
✅ Use **Groups** to manage user permissions

---

## ��️ Hands-On with IAM

### 📌 Create an IAM User

1. Go to AWS Console → IAM → Users → Add User
2. Enable "Programmatic access"
3. Attach existing policies (e.g., `AmazonS3ReadOnlyAccess`)
4. Download Access Key and Secret Key

### 📌 Configure User in AWS CLI

```bash
aws configure
# Provide Access Key, Secret Key, Default Region, Output Format
```

---

## 🧰 IAM Roles – Use Cases

- EC2 Instance accessing S3
- Lambda function writing to DynamoDB
- Cross-account access
- Temporary access for federated users

---

## 🔁 Role Assumption (STS)

Roles are assumed via the **AWS STS (Security Token Service)**.

```json
{
  "Effect": "Allow",
  "Action": "sts:AssumeRole",
  "Resource": "arn:aws:iam::ACCOUNT_ID:role/RoleName"
}
```

---

## 🛡️ Enable MFA (Multi-Factor Authentication)

1. Go to IAM → Users → Security credentials
2. Click “Manage MFA”
3. Choose a virtual MFA device (e.g., Google Authenticator)
4. Scan QR code and verify 2 codes
5. Done! You now have an extra layer of security

---

## 🔄 Identity Federation

You can federate with:

- **Social providers** (Google, Facebook)
- **Corporate directories** (SAML, AD)
- **AWS Cognito** (for apps)

Users log in with external identity, and IAM provides temporary roles.

---

## 📊 Diagram: IAM Role with EC2

```plaintext
 EC2 Instance
     |
     | (assumes role)
     v
IAM Role (e.g., S3AccessRole)
     |
     v
Policy: Allow s3:GetObject on arn:aws:s3:::my-bucket/*
```

---

## ✅ Summary

| Feature           | Description                                      |
|-------------------|--------------------------------------------------|
| Authentication    | IAM Users, Federation, Roles                     |
| Authorization     | IAM Policies (JSON-based access control)         |
| Security          | MFA, Least Privilege, Role-based Access          |
| Governance        | SCPs, Permissions Boundaries, Audit with CloudTrail |

---

## 📌 Practice Tasks

- [ ] Create a user with `AmazonS3FullAccess` and test with CLI
- [ ] Create a custom IAM policy and attach it to a group
- [ ] Create a role and attach it to an EC2 instance
- [ ] Enable MFA for your IAM user and root user

---

## 🧠 Interview Tip

> IAM is all about **who can do what on which resources under which conditions**.

---

