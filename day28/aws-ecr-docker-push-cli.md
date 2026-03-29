# 🐳 AWS ECR Docker Image Push (KodeKloud Lab)

## 📌 Objective

Create a **private ECR repository**, build a Docker image from a given Dockerfile, and push it to ECR with the tag `latest`.

---

## 🧾 Requirements

* ECR Repository Name: `devops-ecr`
* Dockerfile Location: `/root/pypapp`
* Image Tag: `latest`
* Region: `us-east-1`

---

## 🛠️ Steps (CLI Method)

### 1️⃣ Set Region

```bash
aws configure set region us-east-1
```

---

### 2️⃣ Create ECR Repository

```bash
aws ecr create-repository \
  --repository-name devops-ecr
```

---

### 3️⃣ Get Login Credentials for ECR

```bash
aws ecr get-login-password \
  | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
```

👉 Replace `<account-id>` using:

```bash
aws sts get-caller-identity --query Account --output text
```

---

### 4️⃣ Build Docker Image

```bash
cd /root/pypapp

docker build -t devops-ecr .
```

---

### 5️⃣ Tag Image for ECR

```bash
docker tag devops-ecr:latest <account-id>.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
```

---

### 6️⃣ Push Image to ECR

```bash
docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
```

---

## 🔍 Verification

```bash
aws ecr describe-images \
  --repository-name devops-ecr
```

✅ Expected: Image with tag `latest` visible

---

## ⚠️ Common Issues

| Issue          | Cause            | Fix                           |
| -------------- | ---------------- | ----------------------------- |
| Login failed   | Wrong account-id | Use `sts get-caller-identity` |
| Push denied    | Not logged in    | Run docker login again        |
| Repo not found | Not created      | Create ECR repo first         |
| Wrong region   | Mismatch         | Use `us-east-1`               |

---

## 🎯 Key Concept (Interview Point 🔥)

ECR workflow:

1. Create repository
2. Authenticate Docker to ECR
3. Build image
4. Tag with ECR URI
5. Push to repository

---

## 📁 Author

Pankaj Sharma 🚀
DevOps Learner
