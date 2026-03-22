# 🚀 AWS EC2 Passwordless SSH Setup (CLI Method)

## 📌 Overview
This guide demonstrates how to create an AWS EC2 instance using AWS CLI and configure **passwordless SSH authentication**.

---

## 🧠 Concepts
- **EC2** = Virtual Server  
- **Security Group** = Firewall (controls access like port 22 for SSH)  
- **SSH Key Authentication**
  - Private Key → stored on client  
  - Public Key → stored on server  
- **Passwordless SSH** = Secure login without password  

---

## 🏗️ Workflow
aws-client → AWS CLI → EC2 Instance → SSH Key → authorized_keys → Passwordless Login  

---

## ⚙️ Prerequisites
- Access to `aws-client`
- AWS CLI installed
- AWS CLI configured (lab environment)

---

## 🧩 Step-by-Step Implementation

### 🔹 Step 1: Verify AWS CLI Configuration

```bash
aws sts get-caller-identity
````

---

### 🔹 Step 2: Generate SSH Key Pair

```bash
mkdir -p /root/.ssh
ssh-keygen -t rsa -f /root/.ssh/id_rsa -N ""
```

---

### 🔹 Step 3: Launch EC2 Instance

```bash
aws ec2 run-instances \
  --image-id ami-0c02fb55956c7d316 \
  --count 1 \
  --instance-type t2.micro \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=nautilus-ec2}]'
```

---

### 🔹 Step 4: Get Instance Public IP

```bash
aws ec2 describe-instances \
  --query 'Reservations[*].Instances[*].PublicIpAddress' \
  --output text
```

---

### 🔹 Step 5: Configure Security Group (Allow SSH)

Get Security Group ID:

```bash
aws ec2 describe-instances \
  --query 'Reservations[*].Instances[*].SecurityGroups[*].GroupId' \
  --output text
```

Allow SSH (port 22):

```bash
aws ec2 authorize-security-group-ingress \
  --group-id <SG_ID> \
  --protocol tcp \
  --port 22 \
  --cidr 0.0.0.0/0
```

---

### 🔹 Step 6: Copy Public Key

```bash
cat /root/.ssh/id_rsa.pub
```

---

### 🔹 Step 7: Connect to EC2 (via AWS Console)

* Open AWS Console
* Go to EC2 → Instances
* Select `nautilus-ec2`
* Click **Connect → EC2 Instance Connect**

---

### 🔹 Step 8: Add Public Key to EC2

```bash
sudo su -
mkdir -p /root/.ssh
nano /root/.ssh/authorized_keys
```

Paste the public key, then set permissions:

```bash
chmod 700 /root/.ssh
chmod 600 /root/.ssh/authorized_keys
```

---

### 🔹 Step 9: Test Passwordless SSH

```bash
ssh root@<PUBLIC_IP>
```

---

## ✅ Expected Result

* SSH login should work without password
* Direct access to EC2 instance

---

## 🔥 Final Checklist

* [ ] Instance name = `nautilus-ec2`
* [ ] Instance type = `t2.micro`
* [ ] Region = `us-east-1`
* [ ] Port 22 (SSH) open
* [ ] Public key added to server
* [ ] Passwordless SSH working

---

## ❌ Common Issues & Fixes

### SSH Connection Refused

* Ensure port 22 is open in Security Group

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

* Security Groups act as firewalls
* SSH keys provide secure authentication
* Public key is stored on server, private key remains local
* CLI is essential for DevOps automation

---

## 🚀 Conclusion

You successfully created an EC2 instance using AWS CLI and configured secure passwordless SSH access.

---

## 📎 Author

**Pankaj Sharma**
B.Tech CSE | DevOps Learner

```
```
