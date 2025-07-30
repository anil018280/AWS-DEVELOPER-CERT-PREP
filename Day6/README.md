# AWS Lab: Load Balanced EC2 Instances with VPC, NAT Gateway, ASG, Launch Template, and Elastic IP

## Overview

This lab demonstrates deploying a static website on EC2 instances behind an Application Load Balancer 
(ALB) using Auto Scaling Groups, Launch Templates, and a custom VPC with public/private subnets. Health 
checks and routing are configured to distribute traffic between instances.

---

## ✅ Services and Concepts Involved

### 1. **VPC (Virtual Private Cloud)**

* *Purpose*: Isolate network resources with custom IP ranges, route tables, and gateways.
* *Why it's needed*: Provides networking backbone. Avoids using default VPC for better control.

### 2. **Subnets**

* Public Subnet: Hosts web servers accessible via internet.
* Private Subnet: Optional, for backend components.

### 3. **Internet Gateway (IGW)**

* *Purpose*: Enables outbound access to the internet for instances in public subnets.

### 4. **Route Tables**

* *Purpose*: Control routing rules for subnets (e.g., 0.0.0.0/0 to IGW).

### 5. **Elastic IP (EIP)**

* *Purpose*: Provides a static public IP to attach to NAT Gateway or instances.

### 6. **NAT Gateway**

* *Purpose*: Enables instances in private subnet to access the internet without having a public IP.

### 7. **Security Groups**

* *Purpose*: Acts as virtual firewalls. Allow ports: 22 (SSH), 80 (HTTP), 8000 (custom).

### 8. **Launch Template**

* *Purpose*: Blueprint to launch EC2 instances with preconfigured settings like AMI, key pair, and 
userdata.

### 9. **Auto Scaling Group (ASG)**

* *Purpose*: Automatically maintains instance count and replaces unhealthy ones.
* *Why used*: Ensures high availability and scalability.

### 10. **Application Load Balancer (ALB)**

* *Purpose*: Distributes traffic across instances using listeners and target groups.
* Listener Port: 8000 (custom)

### 11. **Target Group**

* *Purpose*: ALB routes traffic to registered EC2 instances.
* Health Check: Configured to check HTTP:8000/index.html

### 12. **Static Website Hosting**

* Python HTTP Server running on port 8000 using:

  ```bash
  nohup python3 -m http.server 8000 > server.log 2>&1 &
  ```

---

## 🛠️ Step-by-Step Lab Instructions

### Step 1: Create a VPC

* CIDR: 10.0.0.0/16

### Step 2: Create Two Subnets (Public)

* Subnet A: 10.0.1.0/24 (AZ1)
* Subnet B: 10.0.2.0/24 (AZ2)

### Step 3: Attach an Internet Gateway

* Attach to the custom VPC

### Step 4: Update Route Table

* Associate public subnets with route table
* Add route to IGW: `0.0.0.0/0 → igw-xxxxxxxx`

### Step 5: Create and Associate Security Group

* Allow inbound:

  * TCP 22 from 0.0.0.0/0 (SSH)
  * TCP 80 from 0.0.0.0/0 (HTTP)
  * TCP 8000 from 0.0.0.0/0 (custom web server)

### Step 6: Allocate Elastic IP (optional, used for NAT if needed)

### Step 7: Create Launch Template

* AMI: Ubuntu 24.04
* Instance type: t2.micro
* Key pair: `key.pem`
* User data (optional): setup index.html and run Python server

### Step 8: Create Auto Scaling Group

* Use Launch Template
* Attach to public subnets
* Desired capacity: 2
* Target group: `my-target`

### Step 9: Create Target Group

* Target type: Instance
* Protocol: HTTP
* Port: 8000
* Health check path: `/`

### Step 10: Create Application Load Balancer

* Type: Application
* Scheme: Internet-facing
* Listener: Port 8000
* Forward to: `my-target` target group

### Step 11: Deploy Web Servers

* SSH into each EC2
* Add custom HTML file as `index.html`
* Start server:

  ```bash
  nohup python3 -m http.server 8000 > server.log 2>&1 &
  ```

---

## �� Testing

* Access ALB DNS: `http://<ALB-DNS>:8000`
* Refresh multiple times to see traffic switch between EC2 1A and 1B

---

## 🧹 Cleanup Guide

### Step 1: Delete Auto Scaling Group

* Choose "Delete" and confirm.

### Step 2: Delete Launch Template

### Step 3: Delete Target Group

### Step 4: Delete Load Balancer

### Step 5: Terminate EC2 Instances (if not already done by ASG)

### Step 6: Release Elastic IP (if created)

### Step 7: Delete NAT Gateway (if used)

### Step 8: Delete Route Tables and Subnets

### Step 9: Detach and Delete Internet Gateway

### Step 10: Delete VPC

---

## ⚠️ Troubleshooting

| Issue                  | Possible Cause                                |
| ---------------------- | --------------------------------------------- |
| 502 Bad Gateway        | Web server not running, health checks failing |
| Target group unhealthy | Wrong health check path or port               |
| ALB not responding     | Listener port misconfigured                   |

---

## ✅ Lab Complete!

This lab simulated a production-grade EC2 setup behind an ALB with scalability and fault tolerance using 
ASG and custom networking.

