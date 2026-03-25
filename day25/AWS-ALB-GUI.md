# 🌐 AWS Application Load Balancer (ALB) Setup using GUI (KodeKloud Lab)

## 📌 Overview
This guide explains how to create an **Application Load Balancer (ALB)** for an EC2 instance using the AWS Management Console (GUI).  
The ALB distributes incoming HTTP traffic to the EC2 instance for better availability and scalability.

---

## 🧠 Concepts
- **EC2** = Virtual Server  
- **ALB (Application Load Balancer)** = Distributes HTTP/HTTPS traffic  
- **Target Group** = Group of EC2 instances receiving traffic  
- **Listener** = Defines protocol & port (e.g., HTTP:80)  
- **Health Check** = Ensures instance is healthy before routing traffic  

---

## 🏗️ Workflow
Client → ALB → Target Group → EC2 Instance  

---

## ⚙️ Prerequisites
- AWS Console access  
- EC2 instance already created and running  
- Security group allowing HTTP (port 80)  

---

## 🧩 Step-by-Step Implementation

### 🔹 Step 1: Verify EC2 Instance
- Go to **EC2 Dashboard → Instances**  
- Ensure instance is **Running**  
- Note the **Instance ID**  

---

### 🔹 Step 2: Create Target Group
- Go to **EC2 Dashboard → Target Groups**  
- Click **Create Target Group**

Configure:
- Target type → **Instances**  
- Name → `nautilus-target-group`  
- Protocol → **HTTP**  
- Port → **80**  
- VPC → Select default VPC  

Health Check:
- Protocol → HTTP  
- Path → `/`  

Click **Next**

---

### 🔹 Step 3: Register Targets
- Select your EC2 instance  
- Click **Include as pending below**  
- Click **Create Target Group**

---

### 🔹 Step 4: Create Application Load Balancer
- Go to **EC2 Dashboard → Load Balancers**  
- Click **Create Load Balancer**  
- Select **Application Load Balancer**

Configure:
- Name → `nautilus-alb`  
- Scheme → **Internet-facing**  
- IP type → IPv4  

Network Mapping:
- Select at least **2 Availability Zones**

---

### 🔹 Step 5: Configure Security Group
- Create or select security group  
- Allow:
  - HTTP (Port 80) → Anywhere (0.0.0.0/0)

---

### 🔹 Step 6: Configure Listener & Routing
- Listener → HTTP : 80  
- Forward to → `nautilus-target-group`

---

### 🔹 Step 7: Create Load Balancer
- Review settings  
- Click **Create Load Balancer**

---

### 🔹 Step 8: Verify Target Health
- Go to **Target Groups → Targets**  
- Ensure status = **Healthy**

---

### 🔹 Step 9: Test Load Balancer
- Go to **Load Balancers**  
- Copy **DNS name**  
- Open in browser  

✅ Expected: EC2 instance response (web page)

---

## ✅ Final Checklist
- [ ] EC2 instance running  
- [ ] Target group created  
- [ ] Instance registered  
- [ ] ALB created  
- [ ] Listener configured (HTTP:80)  
- [ ] Security group allows HTTP  
- [ ] Target health = Healthy  
- [ ] ALB DNS working  

---

## ❌ Common Issues & Fixes

### Target Unhealthy
- Check EC2 security group allows port 80  
- Ensure web server is running on EC2  

---

### ALB Not Accessible
- Check ALB security group  
- Ensure internet-facing scheme selected  

---

### No Response in Browser
- Verify health check path `/`  
- Check instance status  

---

## 🧠 Key Learnings
- ALB distributes traffic across instances  
- Target Groups manage backend instances  
- Health checks ensure reliability  
- GUI setup is simple but CLI is preferred in DevOps  

---

## 🚀 Conclusion
You successfully created an Application Load Balancer and connected it to an EC2 instance using AWS GUI.

---

## 📎 Author
**Pankaj Sharma**  
B.Tech CSE | DevOps Learner
```
