# 🚀 AWS EC2 + CloudWatch Alarm Setup using CLI (KodeKloud Lab)

## 📌 Overview
This lab demonstrates how to:
- Launch an EC2 instance  
- Create a CloudWatch alarm to monitor CPU utilization  
- Send notifications using an SNS topic  

All tasks are performed using **AWS CLI**.

---

## 🧠 Concepts
- **EC2** = Virtual Server  
- **CloudWatch** = Monitoring service  
- **Alarm** = Trigger based on metrics  
- **SNS (Simple Notification Service)** = Sends alerts  
- **CPU Utilization** = Performance metric  

---

## 🏗️ Workflow
EC2 Instance → CloudWatch Metric → Alarm → SNS Notification  

---

## ⚙️ Prerequisites
- AWS CLI installed  
- AWS CLI configured  
- Region: `us-east-1`  

---

## 🧩 Step-by-Step Implementation

### 🔹 Step 1: Launch EC2 Instance

```bash
aws ec2 run-instances \
  --image-id ami-0c02fb55956c7d316 \
  --count 1 \
  --instance-type t2.micro \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=xfusion-ec2}]'
````

---

### 🔹 Step 2: Get Instance ID

```bash
aws ec2 describe-instances \
  --query 'Reservations[*].Instances[*].InstanceId' \
  --output text
```

---

### 🔹 Step 3: Get SNS Topic ARN

```bash
aws sns list-topics
```

📌 Find ARN of:

```
xfusion-sns-topic
```

---

### 🔹 Step 4: Create CloudWatch Alarm

```bash
aws cloudwatch put-metric-alarm \
  --alarm-name xfusion-alarm \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --statistic Average \
  --period 300 \
  --threshold 90 \
  --comparison-operator GreaterThanOrEqualToThreshold \
  --dimensions Name=InstanceId,Value=<INSTANCE_ID> \
  --evaluation-periods 1 \
  --alarm-actions <SNS_TOPIC_ARN> \
  --region us-east-1
```

---

## ✅ Expected Result

* EC2 instance created successfully
* CloudWatch alarm configured
* Alarm triggers when CPU ≥ 90%
* SNS sends notification

---

## 🔥 Final Checklist

* [ ] Instance name = `xfusion-ec2`
* [ ] Instance running
* [ ] Alarm name = `xfusion-alarm`
* [ ] Metric = CPUUtilization
* [ ] Threshold = 90%
* [ ] Period = 5 minutes (300 seconds)
* [ ] SNS topic attached

---

## ❌ Common Issues & Fixes

### Alarm Not Triggering

* Ensure EC2 instance is running
* Wait for metrics to appear (2–5 mins)

---

### SNS Not Sending Notifications

* Verify correct SNS ARN
* Ensure subscription is confirmed

---

### Wrong Instance ID

```bash
aws ec2 describe-instances
```

---

## 🧠 Key Learnings

* CloudWatch monitors AWS resources
* Alarms trigger based on thresholds
* SNS integrates with monitoring for alerts
* CLI is powerful for automation

---

## 🚀 Conclusion

You successfully created an EC2 instance and configured a CloudWatch alarm with SNS notifications using AWS CLI.

---

## 📎 Author

**Pankaj Sharma**
B.Tech CSE | DevOps Learner
