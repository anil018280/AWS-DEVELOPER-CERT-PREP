
# Day 7 – AWS VPC: Theory + Hands-On Lab

## 🧠 What is VPC?

A **Virtual Private Cloud (VPC)** is your own logically isolated network within the AWS cloud. It gives 
you full control over your AWS networking setup, including:
- IP address ranges (CIDR)
- Subnets (public/private)
- Route tables
- Internet access (via gateways)
- Firewalls (Security Groups & NACLs)

---

## 🧱 VPC Core Components

| Component | Description | Analogy |
|----------|-------------|---------|
| **VPC (CIDR Block)** | IP range for your network (e.g. `10.0.0.0/16`) | Entire gated community |
| **Subnets** | IP range subsets inside VPC | Neighborhoods in the community |
| **Route Table** | Controls traffic routing | Road map |
| **Internet Gateway (IGW)** | Enables public internet access | Main gate to internet |
| **NAT Gateway** | Allows private instances to access internet | Guarded exit tunnel |
| **Security Groups (SG)** | Instance-level firewall | Door bouncer |
| **Network ACLs (NACL)** | Subnet-level firewall | Security gate on the street |

---

## 🔐 Security Groups vs NACLs

| Feature              | Security Groups (SG) | Network ACLs (NACL) |
|----------------------|----------------------|----------------------|
| Applies To           | EC2 instance         | Entire subnet        |
| Stateful             | ✅ Yes                | ❌ No                 |
| Rules                | Allow only           | Allow & Deny         |
| Evaluation           | All matched          | First match wins     |
| Use Case             | Instance protection  | Subnet-wide rules    |

---

## 🧪 Lab: Deploy EC2 in VPC and Control Traffic

### 🎯 Objective:
Create a custom VPC, launch EC2 inside it, run a Python web server, and control access using SGs and 
NACLs.

---

### ✅ Step-by-Step Lab Instructions

#### 1. **Create a VPC**
- Name: `MyCustomVPC`
- CIDR Block: `10.0.0.0/16`

#### 2. **Create 1 Public Subnet**
- Name: `PublicSubnet`
- CIDR Block: `10.0.1.0/24`
- Availability Zone: `us-east-1a`

#### 3. **Attach an Internet Gateway**
- Create IGW and attach it to `MyCustomVPC`

#### 4. **Update Route Table**
- Route Table → Add Route:
  - Destination: `0.0.0.0/0`
  - Target: IGW

#### 5. **Create EC2 Instance**
- Subnet: `PublicSubnet`
- OS: Ubuntu
- Key Pair: download `.pem` file
- Security Group: allow **port 22** and **port 8000**

#### 6. **SSH into EC2**
```bash
chmod 400 ~/Downloads/key.pem
ssh -i ~/Downloads/key.pem ubuntu@<EC2-PUBLIC-IP>
```

#### 7. **Start Python Web Server**
```bash
python3 -m http.server 8000
```

#### 8. **Test in Browser**
- Open `http://<EC2-PUBLIC-IP>:8000`
- 🔴 If blocked: check SG or NACL

---

### 🚧 NACL Experiment

#### Initial Setup:
- Inbound Rule 100: Allow ALL (`0.0.0.0/0`)
- Outbound Rule 100: Allow ALL

✅ Web app should be accessible

---

#### Step 1: **Block port 8000**

- Add Inbound Rule 200: Deny TCP port 8000

➡️ Result: ❗ Site still loads → why? Because rule 100 (Allow All) matched first.

---

#### Step 2: **Reorder Rules**
- Change:
  - Rule 100: **Deny TCP 8000**
  - Rule 200: **Allow ALL**

➡️ Result: ❌ Now site is blocked! ✅ NACL follows **first match wins** logic.

---

## 🧠 Key Learnings:

- SGs are **stateful**; NACLs are **stateless**
- SGs: instance-level; NACLs: subnet-level
- NACL rule **order matters**; first match wins
- VPC = the foundation of secure cloud architecture

---

✅ **You just built a real-world VPC network!**

