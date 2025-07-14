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

---

## 🔐 IAM Lockdown Scenario
aws iam create-policy-version \
--policy-arn arn:aws:iam::YOUR_ACCOUNT_ID:policy/suspectPrivilegeEscalationPolicy \
--policy-document file://policy.json \
--set-as-default \
--profile suspect-profile

---

## 💪 Key Skills Demonstrated
- Cloud Security Monitoring
- IAM Policy Management
- Incident Response Automation
- AWS CLI Proficiency
- Log Filtering & Correlation

---

## 🌟 Why It Stands Out
- Real-time detection and response ✅
- Security automation (no manual triage) ✅
- Includes alert-to-response flow ✅
- Job-ready architecture for SOC and Cloud Analyst roles ✅

---

## 📚 Lessons Learned
- How to convert logs to metrics
- When to trigger alarms using thresholds
- How to safely rotate IAM policies via CLI
- Cloud-native response without third-party tools

---

## 📸 Screenshots
![CloudTrail Created](screenshots/01-cloudtrail-creation.png)
*CloudTrail initialized for activity logging*

![CloudTrail Logging Enabled](screenshots/03-enable-logging.png)
*Logging turned on for governance and visibility*

![EventBridge Rule Created](screenshots/04-eventbridge-rule-created.png)
*EventBridge rule routes IAM change events*

![CloudWatch Metric Filter Check](screenshots/08-cloudwatch-metric-check.png)
*Verifying metric filter setup for CloudTrail log group*

![Log Group Filter Fix](screenshots/11-cloudwatch-metric-filter-loggroup-fix.png)
*Fixing filter destination for log group*

![Root Login Alarm Configured](screenshots/15-cloudwatch-root-login-alarm-configured.png)
*CloudWatch alarm monitors root account logins*

![Email Alert Received](screenshots/16-root-login-alarm-email.png)
*Email notification triggered by root login*

![CloudTrail Root Event Detected](screenshots/18-cloudtrail-root-events.png)
*Root login event captured in logs*

![Suspect IAM User Exists](screenshots/19-iam-user-already-exists-suspect-user.png)
*Suspicious user detected in IAM*

![User Details Retrieved](screenshots/20-iam-get-user-suspect-user-details.png)
*Getting user metadata and ARN*

![User Has No Policies](screenshots/21-iam-check-user-policies-suspect-user-empty.png)
*No policies initially attached to the user*

![Admin Policy Added](screenshots/22-iam-attach-admin-policy-to-suspect-user.png)
*Privilege escalation via AdministratorAccess*

![Access Key Created](screenshots/24-access-key-created-suspect-user-aws-compromise.png)
*Suspect creates new access key (compromise starts)*

![Configure AWS Profile](screenshots/suspect-configure-profile.PNG)
*Profile set with stolen credentials*

![Verify Profile Setup](screenshots/27-suspect-profile-verify.png)
*CLI confirms correct configuration*

![Log Groups Queried](screenshots/28-identity-log-groups-output.png)
*Attacker recon via CLI command*

![Recon Filter Set](screenshots/29-put-metric-filter-recon.png)
*Custom filter for recon pattern added*

![Alarm Confirmed](screenshots/31-cloudwatch-alarm-confirmation..png)
*Metric alarm created for suspicious recon*

![SNS Alarm Triggered](screenshots/33-sns-recon-alarm.png)
*Alert sent when threshold breached*

![Escalation Filter Added](screenshots/34-filter-escalation.png)
*Log filter added for escalation attempt*

![Policy JSON for Lockdown](screenshots/36-policy-json..png)
*Custom lockdown policy drafted*

![Policy Created](screenshots/38-create-policy-v1.png)
*Policy successfully deployed*

![Alarm Triggers on Escalation](screenshots/39-create-policy-v2-alarm-trigger.png)
*Alarm fires on policy misuse*

![Threshold Breach Confirmed](screenshots/40-alarm-threshold-crossed.png)
*CloudWatch confirms incident severity*
