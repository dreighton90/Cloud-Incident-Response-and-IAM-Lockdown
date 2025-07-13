# Cloud-Incident-Response-and-IAM-Lockdown

# 🔐 Cloud Incident Response + IAM Lockdown

## 🔢 Project Overview

This project simulates a real-world cloud incident response workflow in AWS. It detects suspicious user behavior in real time — such as unauthorized privilege escalation — and automatically triggers IAM lockdown actions to contain the threat.

✅ This project extends my previous **Cloud Security Alerting System (AWS + PostgreSQL)** by adding **automated incident response** and **IAM access control**, strengthening detection and containment within a cloud-native environment.

---

## 📊 Use Case

A user attempts to create IAM roles or policies without authorization. The system:

1. Detects the event through a CloudTrail filter  
2. Sends a CloudWatch alarm to an SNS topic  
3. Triggers an automated IAM policy lockdown  

---

## 🛠️ Architecture

- **CloudTrail**: Logs API events like `CreatePolicyVersion`  
- **CloudWatch Logs + Metric Filter**: Detects suspicious user activity  
- **CloudWatch Alarm**: Monitors for filtered events and sends notifications  
- **SNS Topic**: Sends alert to email or Lambda  
- **IAM Policy + CLI**: Restricts access to mitigate the threat  

---

## 🔧 Tools & Services Used

- AWS CloudTrail  
- AWS CloudWatch Logs & Alarms  
- Amazon SNS  
- IAM (Identity and Access Management)  
- AWS CLI  
- Ubuntu 24.04 VM (VirtualBox)  

---

## 🔢 Sample Detection Logic

```json
{
  "eventName": "CreatePolicyVersion",
  "userIdentity": {
    "userName": "suspect-user"
  }
}
```

## ⚡ Alert Workflow
- CloudTrail logs an unauthorized CreatePolicyVersion event
- Metric filter flags the log with metricValue = 1
- CloudWatch Alarm triggers based on threshold = 1
- SNS notifies the security team or initiates an IAM lockdown

## 🔐 IAM Lockdown Scenario
aws iam create-policy-version \
--policy-arn arn:aws:iam::YOUR_ACCOUNT_ID:policy/suspectPrivilegeEscalationPolicy \
--policy-document file://policy.json \
--set-as-default \
--profile suspect-profile

## 📸 Screenshots
