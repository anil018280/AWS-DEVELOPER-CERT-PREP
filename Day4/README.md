
# 🖥️ Day 4: Amazon EC2 – Complete Deep Dive

Amazon EC2 (Elastic Compute Cloud) is one of the core services of AWS that allows you to launch and manage 
virtual machines in the cloud. This guide is both a theoretical and hands-on explanation of EC2 for 
absolute clarity and practical application.

---

## 🌐 What is Amazon EC2?

**Amazon EC2 (Elastic Compute Cloud)** is a web service that allows users to rent virtual servers (called 
**instances**) on demand to run applications, host websites, train models, and more.

Instead of managing physical hardware, you launch **instances** in the cloud and pay only for what you 
use.

---

## 🎯 Why EC2 Exists

- Traditional on-prem servers are expensive and inflexible.
- Developers need compute power that’s:
  - Scalable (scale up/down easily)
  - On-demand (pay-as-you-go)
  - Reliable (multiple regions/AZs)
  - Secure (isolated, encrypted)
- EC2 solves this by offering **resizable compute capacity** in the cloud.

---

## 🧠 EC2 Core Concepts

| Concept           | Explanation |
|-------------------|-------------|
| **AMI**           | Amazon Machine Image – a template with OS + pre-installed software |
| **Instance**      | A virtual machine launched from an AMI |
| **Instance Type** | Hardware config (vCPU, RAM, storage, bandwidth) e.g., `t2.micro`, `m5.large` |
| **Key Pair**      | Used for secure SSH access (public/private key) |
| **Security Group**| Virtual firewall for controlling traffic (inbound/outbound rules) |
| **Elastic IP**    | Static public IP address for EC2 |
| **User Data**     | Shell script that runs on first boot for automation |
| **EBS**           | Elastic Block Store – persistent disk attached to EC2 |
| **Auto Scaling**  | Automatically increases/decreases number of instances |
| **Load Balancer** | Distributes traffic across multiple instances |

---

## 🛠️ EC2 Hands-On: Launch and Configure

### 1. Launch EC2 Instance
- Go to EC2 Dashboard → Launch instance
- Choose AMI: Ubuntu 22.04 LTS (or Amazon Linux)
- Select Instance Type: `t2.micro` (free tier)
- Create or use an existing Key Pair (`.pem`)
- Create or use a VPC + subnet
- Create a Security Group with:
  - SSH (22) from your IP
  - HTTP (80) from anywhere
- Launch instance

---

### 2. Connect via SSH

On your local machine:
```bash
chmod 400 ~/Downloads/key.pem
ssh -i ~/Downloads/key.pem ubuntu@<EC2-PUBLIC-IP>
```

---

### 3. Install Web Server (Nginx)
```bash
sudo apt update && sudo apt install nginx -y
sudo systemctl status nginx
```

Visit: `http://<EC2-PUBLIC-IP>` — should show the Nginx welcome page.

---

### 4. Upload Your Website via SCP
From local machine:
```bash
scp -i ~/Downloads/key.pem index.html styles.css ubuntu@<EC2-PUBLIC-IP>:~
```

Then move inside EC2:
```bash
sudo mv ~/index.html ~/styles.css /var/www/html/
```

---

### 5. Enable Port 80 (Security Group)
- Go to EC2 → Instances → Select Instance
- Under "Security" → Click Security Group
- Edit inbound rules → Add rule:
  - Type: HTTP
  - Port: 80
  - Source: 0.0.0.0/0

---

## 🔐 Security in EC2

- Use **SSH keys** (never use passwords)
- Restrict SSH to “My IP”
- Regularly rotate keys
- Avoid `0.0.0.0/0` unless necessary
- Use Security Groups to define rules per port/protocol
- Use **IAM Roles** to let EC2 access AWS services securely

---

## 📦 EC2 Storage: EBS vs Instance Store

| Storage Type     | Description                                  |
|------------------|----------------------------------------------|
| **EBS**          | Persistent, survives stop/start              |
| **Instance Store**| Ephemeral, erased when instance stops       |

---

## 💡 User Data – Auto Bootstrap Server

You can run a script automatically at boot:

Example:
```bash
#!/bin/bash
apt update
apt install nginx -y
echo "<h1>Hello from EC2!</h1>" > /var/www/html/index.html
```

Paste this under **Advanced → User Data** when launching an instance.

---

## 📈 Monitoring and Troubleshooting

- **CloudWatch**: View CPU, disk, network metrics
- **EC2 Status Checks**:
  - System Status = AWS infra
  - Instance Status = OS-level
- Check logs:
```bash
cat /var/log/cloud-init.log
```

---

## 🔄 EC2 Lifecycle

| State        | Description                           |
|--------------|---------------------------------------|
| **Pending**  | Launching instance                    |
| **Running**  | Instance is live                      |
| **Stopping** | In the process of stopping            |
| **Stopped**  | Retains EBS but not compute resources |
| **Terminated**| Deleted permanently                  |

---

## 🧠 Real-World Use Cases

- Web app or API hosting
- Hosting Jenkins, Git servers
- ML model training
- Data processing pipelines
- Running Dockerized apps

---

## 📌 Summary

| Feature       | Value                          |
|---------------|--------------------------------|
| Compute Units | Virtual servers (instances)    |
| Scalability   | Launch 1 or 1000+ on demand    |
| Control       | Full root/admin access         |
| Flexibility   | Choose your OS, software, size |
| Pricing       | Pay-per-second or reserved     |

---

## 🚀 What’s Next?

- Attach an IAM role for secure S3 access
- Use Route 53 + CloudFront for domain + CDN
- Set up SSL using Let’s Encrypt or ACM
- Explore EC2 Image Builder or Launch Templates

---

