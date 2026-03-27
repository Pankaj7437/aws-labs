# 🌐 AWS Public VPC with EC2 Setup (KodeKloud Lab)

## 📌 Objective

Create a **public VPC**, configure internet access using an **Internet Gateway and Route Table**, and launch an EC2 instance accessible via SSH.

---

## 🧾 Requirements

* VPC: `xfusion-pub-vpc`
* Subnet: `xfusion-pub-subnet`
* Public IP: Enabled
* EC2: `xfusion-pub-ec2`
* Instance Type: `t2.micro`
* SSH: Port 22 open

---

## 🛠️ Steps

### 1️⃣ Login to AWS

* Region: `us-east-1`

---

### 2️⃣ Create VPC

* Name: `xfusion-pub-vpc`
* CIDR: `10.0.0.0/16`

---

### 3️⃣ Create Subnet

* Name: `xfusion-pub-subnet`
* CIDR: `10.0.1.0/24`
* VPC: `xfusion-pub-vpc`

---

### 4️⃣ Enable Public IP

* Subnet → Actions → Edit settings
* Enable:
  ✅ Auto-assign Public IPv4

---

### 5️⃣ Create Internet Gateway (IMPORTANT 🔥)

* Go to **Internet Gateways → Create**
* Name: `xfusion-igw`
* Attach to VPC: `xfusion-pub-vpc`

---

### 6️⃣ Configure Route Table (MOST IMPORTANT ⚠️)

#### ➤ Add Internet Route

* Go to **Route Tables**
* Select route table of your VPC
* Add route:

| Destination | Target                           |
| ----------- | -------------------------------- |
| 0.0.0.0/0   | Internet Gateway (`xfusion-igw`) |

---

#### ➤ Associate Subnet

* Route Table → Subnet Associations
* Add: `xfusion-pub-subnet`

---

### 7️⃣ Launch EC2 Instance

* Name: `xfusion-pub-ec2`
* AMI: Ubuntu
* Type: `t2.micro`
* Network: `xfusion-pub-vpc`
* Subnet: `xfusion-pub-subnet`
* Public IP: Enabled

---

### 8️⃣ Security Group

* Allow:

  * SSH (22) → 0.0.0.0/0

---

### 9️⃣ Launch Instance

---

## 🔍 Verification

```bash
ssh ubuntu@<public-ip>
```

---

## ⚠️ Common Mistakes

| Problem           | Reason              |
| ----------------- | ------------------- |
| ❌ No internet     | IGW not attached    |
| ❌ SSH fails       | Port 22 closed      |
| ❌ No public IP    | Subnet setting off  |
| ❌ Still no access | Route table missing |

---

## 🎯 Key Concept (Interview Point 🔥)

A VPC becomes **public only when:**

1. Internet Gateway is attached
2. Route table has `0.0.0.0/0 → IGW`
3. Subnet is associated with that route table
4. Instance has public IP

---

## 📁 Author

Pankaj Sharma 🚀
