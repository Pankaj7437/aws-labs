# 🚀 AWS S3 Data Migration using CLI (KodeKloud Lab)

## 📌 Overview
This lab demonstrates how to:
- Create a new private S3 bucket  
- Migrate data from an existing S3 bucket  
- Verify data consistency  

All operations are performed using **AWS CLI**, following DevOps best practices.

---

## 🧠 Concepts
- **S3 Bucket** = Object storage container  
- **Data Migration** = Copying data between buckets  
- **aws s3 sync** = Efficiently syncs data  
- **--dryrun** = Simulates operation without executing  
- **--region** = Specifies AWS region  

---

## 🏗️ Workflow
Existing Bucket → New Bucket → Data Sync → Verification  

---

## ⚙️ Prerequisites
- AWS CLI installed  
- AWS CLI configured  
- Region: `us-east-1`  

---

## 🧩 Step-by-Step Implementation

### 🔹 Step 1: Create New S3 Bucket

```bash
aws s3 mb s3://nautilus-sync-26685 --region us-east-1
````

---

### 🔹 Step 2: Verify Bucket Creation

```bash
aws s3 ls
```

---

### 🔹 Step 3: Perform Dry Run (Verification Before Copy)

```bash
aws s3 sync s3://nautilus-s3-24542 s3://nautilus-sync-26685 --dryrun
```

📌 This ensures:

* Files to be copied are correct
* No unintended changes

---

### 🔹 Step 4: Migrate Data

```bash
aws s3 sync s3://nautilus-s3-24542 s3://nautilus-sync-26685
```

---

### 🔹 Step 5: Verify Data Consistency

```bash
aws s3 sync s3://nautilus-s3-24542 s3://nautilus-sync-26685 --dryrun
```

✅ If no output → Buckets are in sync

---

## ✅ Expected Result

* New bucket created successfully
* All data copied from source to destination
* Both buckets contain identical data

---

## 🔥 Final Checklist

* [ ] Bucket created in `us-east-1`
* [ ] Data migrated successfully
* [ ] No missing files
* [ ] Sync verification passed

---

## ❌ Common Issues & Fixes

### Bucket Already Exists

```bash
aws s3 mb s3://unique-bucket-name --region us-east-1
```

---

### Region Mismatch

* Always use `--region us-east-1`

---

### Partial Sync Issue

```bash
aws s3 sync s3://source s3://destination
```

---

## 🧠 Key Learnings

* `aws s3 mb` → create bucket
* `aws s3 ls` → list buckets
* `aws s3 sync` → migrate data
* `--dryrun` → safe verification
* CLI is efficient for large-scale data operations

---

## 🚀 Conclusion

You successfully performed S3 data migration using AWS CLI and verified data integrity using dry-run sync.

---

## 📎 Author

**Pankaj Sharma**
B.Tech CSE | DevOps Learner

```
o ek **portfolio repo** bana dete hain 💯
```
