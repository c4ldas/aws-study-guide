# AWS Trusted Advisor & Health Dashboard

Click on each topic to go to the specific section.

| **Topic** | **Description** |
|----------|-----------------|
| 🧠 [1. AWS Trusted Advisor](#-aws-trusted-advisor) | Provides real-time guidance to help you provision resources following AWS best practices. |
| 🏥 [2. AWS Health Dashboard](#-aws-health-dashboard) | Gives visibility into AWS service events and resource-level health issues. |
| 🛠 [3. Hands-On: Accessing Trusted Advisor & Health Events](#-hands-on-accessing-trusted-advisor--health-events) | CLI and Console access for both services. |

---

## 🧠 AWS Trusted Advisor

Trusted Advisor checks your AWS environment and recommends improvements.

### 💡 Key Points:
- Categories: Cost Optimization, Performance, Security, Fault Tolerance, Service Limits.
- Some checks are free; full access requires Business or Enterprise support plans.
- Recommendations are actionable — you get direct steps to improve.

### 🌐 Example Use Case:
Trusted Advisor detects underutilized EC2 instances and recommends rightsizing to reduce cost.

---

## 🏥 AWS Health Dashboard

Monitors and reports events that may affect your AWS resources.

### 💡 Key Points:
- **AWS Health Dashboard (Global View)**: High-level overview of service status.
- **Personal Health Dashboard**: Shows events that affect your specific account.
- Events include:
  - Planned maintenance
  - Outages or degradation
  - Account-specific issues (e.g., instance reachability)

### 🌐 Example Use Case:
You receive a notification that an EC2 instance in your account is experiencing degraded networking.

---

## 🛠 Hands-On: Accessing Trusted Advisor & Health Events

### ✅ View Trusted Advisor Checks (Requires Business/Enterprise Support)
```
aws support describe-trusted-advisor-checks \
  --language en

aws support describe-trusted-advisor-check-result \
  --check-id <check-id>
```
---

### ✅ Access the Health Dashboard via Console

Visit:
https://health.aws.amazon.com/health/home

---

### ✅ Get Account-Specific Health Events via CLI
```
aws health describe-events

aws health describe-event-details \
  --event-arns <event-arn>
```
---

In summary, Trusted Advisor and the Health Dashboard are key tools for monitoring your AWS account's health, optimizing resources, and staying informed about service disruptions.
