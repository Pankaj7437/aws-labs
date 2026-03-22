# 🖥️ AWS EC2 Passwordless SSH Setup (GUI Method)

## 📌 Overview
This guide explains how to create an EC2 instance using the AWS Management Console (GUI) and configure **passwordless SSH login** using a manually generated SSH key.

---

## 🧠 Concepts
- **EC2** = Virtual Server  
- **Security Group** = Firewall (controls access like SSH on port 22)  
- **EC2 Instance Connect** = Temporary browser-based access  
- **SSH Keys**
  - Private Key → stays on your machine  
  - Public Key → stored on server  
- **Passwordless SSH** = Login without password  

---

## 🏗️ Workflow
AWS Console → EC2 Instance → EC2 Instance Connect → Add SSH Key → Passwordless SSH  

---

## ⚙️ Prerequisites
- AWS Console access (lab credentials)  
- Access to `aws-client`  

---

## 🧩 Step-by-Step Implementation

### 🔹 Step 1: Login to AWS Console
- Open provided **Console URL**  
- Login using username and password  

---

### 🔹 Step 2: Launch EC2 Instance
- Go to **EC2 Dashboard**
- Click **Launch Instance**
- Configure:
  - **Name** → `nautilus-ec2`
  - **AMI** → Amazon Linux
  - **Instance Type** → `t2.micro`

---

### 🔹 Step 3: Key Pair
- Select **Proceed without a key pair** (not required for EC2 Instance Connect)

---

### 🔹 Step 4: Configure Security Group
- Allow **SSH (Port 22)**
- Source → `0.0.0.0/0` (Anywhere)

---

### 🔹 Step 5: Launch Instance
- Click **Launch Instance**
- Wait until instance state = **Running**

---

### 🔹 Step 6: Connect to EC2
- Select instance `nautilus-ec2`
- Click **Connect**
- Choose **EC2 Instance Connect**
- Click **Connect**

📌 EC2 Instance Connect provides temporary access without requiring a key pair

---

### 🔹 Step 7: Generate SSH Key (on aws-client)

```bash
mkdir -p /root/.ssh
ssh-keygen -t rsa -f /root/.ssh/id_rsa -N ""
cat /root/.ssh/id_rsa.pub
````

---

### 🔹 Step 8: Add Public Key to EC2

Inside EC2 terminal:

```bash
sudo su -
mkdir -p /root/.ssh
nano /root/.ssh/authorized_keys
```

Paste the public key, then run:

```bash
chmod 700 /root/.ssh
chmod 600 /root/.ssh/authorized_keys
```

---

### 🔹 Step 9: Get Public IP

* Go to EC2 → Instances
* Copy **Public IPv4 address**

---

### 🔹 Step 10: Test Passwordless SSH

From aws-client:

```bash
ssh root@<PUBLIC_IP>
```

---

## ✅ Expected Result

* SSH login works without password
* Direct access to EC2 instance

---

## 🔥 Final Checklist

* [ ] Instance name = `nautilus-ec2`
* [ ] Instance type = `t2.micro`
* [ ] SSH (port 22) enabled
* [ ] Public key added to `/root/.ssh/authorized_keys`
* [ ] Passwordless SSH working

---

## ❌ Common Issues & Fixes

### SSH Connection Refused

* Check Security Group → Port 22 must be open

### Permission Denied

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### Wrong User

```bash
ssh root@<IP>
```

### Host Key Verification Error

```bash
ssh -o StrictHostKeyChecking=no root@<IP>
```

---

## 🧠 Key Learnings

* EC2 Instance Connect provides temporary access
* SSH keys provide permanent secure access
* Security Groups control network access
* GUI is beginner-friendly but CLI is preferred in DevOps

---

## 🚀 Conclusion

You successfully created an EC2 instance using AWS GUI and configured secure passwordless SSH login.

---

## 📎 Author

**Pankaj Sharma**
B.Tech CSE | DevOps Learner

```
```
