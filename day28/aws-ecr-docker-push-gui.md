# 🐳 AWS ECR Docker Image Push (GUI Method - KodeKloud Lab)

## 📌 Objective

Create a **private Amazon ECR repository**, build a Docker image from a given Dockerfile, and push it to ECR using GUI + CLI.

---

## 🧾 Requirements

* Repository Name: `devops-ecr`
* Dockerfile Path: `/root/pypapp`
* Image Tag: `latest`
* Region: `us-east-1`

---

## 🛠️ Steps to Perform

### 1️⃣ Login to AWS Console

* Open provided Console URL
* Login with given credentials
* Select region: `us-east-1`

---

### 2️⃣ Create ECR Repository (GUI)

* Go to **ECR → Repositories → Create repository**

#### Configuration:

* **Visibility**: Private
* **Repository Name**: `devops-ecr`
* Leave other settings as default

👉 Click **Create repository**

---

### 3️⃣ Copy Repository URI

* Open your repository
* Copy the **Repository URI**

  ```
  <account-id>.dkr.ecr.us-east-1.amazonaws.com/devops-ecr
  ```

---

### 4️⃣ Login to ECR (CLI)

Run on `aws-client`:

```bash id="j5v8g1"
aws ecr get-login-password \
| docker login --username AWS --password-stdin <repository-uri-without-repo-name>
```

👉 Example:

```bash id="sqc1q2"
aws ecr get-login-password \
| docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com
```

---

### 5️⃣ Build Docker Image

```bash id="q4fz2k"
cd /root/pypapp
docker build -t devops-ecr .
```

---

### 6️⃣ Tag Image

```bash id="x2s8ld"
docker tag devops-ecr:latest <repository-uri>:latest
```

---

### 7️⃣ Push Image to ECR

```bash id="c8v9zp"
docker push <repository-uri>:latest
```

---

## 🔍 Verification

* Go to **ECR → Repositories → devops-ecr**
* Check **Images section**

✅ Expected: Image with tag `latest`

---

## ⚠️ Common Issues

| Issue            | Cause           | Fix                      |
| ---------------- | --------------- | ------------------------ |
| Login failed     | Wrong URI       | Use correct registry URI |
| Push denied      | Not logged in   | Run docker login again   |
| No image in repo | Push not done   | Run docker push          |
| Wrong region     | Region mismatch | Use us-east-1            |

---

## 🎯 Key Concept (Interview Point 🔥)

Even in GUI workflow:

* ECR repo is created via Console
* But image push always happens via Docker CLI

---

## 📁 Author

Pankaj Sharma 🚀
DevOps Learner
