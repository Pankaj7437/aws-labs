# 🚀 AWS EC2 Nginx Setup (KodeKloud Lab)

## 📌 Objective

Create an EC2 instance that serves as a web server using **Nginx**, ensuring it is accessible over the internet.

---

## 🧾 Requirements

* Instance Name: `xfusion-ec2`
* AMI: Ubuntu (any available)
* Web Server: Nginx
* Security Group: Allow HTTP (port 80)

---

## 🛠️ Steps to Perform

### 1️⃣ Login to AWS Console

* Use the provided credentials
* Select region: `us-east-1`

---

### 2️⃣ Launch EC2 Instance

* Navigate to **EC2 → Instances → Launch Instance**

#### Basic Configuration:

* **Name**: `xfusion-ec2`
* **AMI**: Ubuntu
* **Instance Type**: t2.micro

---

### 3️⃣ Configure Key Pair

* Select **Proceed without key pair** (lab environment)

---

### 4️⃣ Configure Network Settings

* Allow inbound traffic:

  * HTTP (Port 80) → Required
  * SSH (optional)

---

### 5️⃣ Add User Data Script

Go to **Advanced Details → User Data** and add:

```bash
#!/bin/bash
apt update -y
apt install nginx -y
systemctl start nginx
systemctl enable nginx
```

---

### 6️⃣ Launch Instance

* Click **Launch Instance**

---

## 🔍 Verification

1. Wait until instance state = **Running**
2. Copy the **Public IP**
3. Open in browser:

```
http://<public-ip>
```

✅ Expected Output:
Nginx default welcome page

---

## ⚠️ Common Issues

| Issue                   | Cause           | Fix                          |
| ----------------------- | --------------- | ---------------------------- |
| Website not loading     | Port 80 blocked | Allow HTTP in Security Group |
| Nginx not running       | Script missing  | Add user data script         |
| Lab failing             | Wrong name      | Use exact: `xfusion-ec2`     |
| Instance not accessible | Wrong region    | Use `us-east-1`              |

---

## 🎯 Conclusion

Successfully deployed an EC2 instance with Nginx using a user data script and made it accessible over HTTP.

---

## 📁 Author

**Pankaj Sharma**
DevOps Learner 🚀
