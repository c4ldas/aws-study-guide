# Common AWS Support Scenarios: Troubleshooting & Security

Click on each topic to go to the specific section.

| **Topic** | **Description** |
|----------|-----------------|
| 🐞 [1. General Troubleshooting](#-general-troubleshooting) | Common issues with EC2, S3, and networking. |
| 🔐 [2. IAM and Security](#-iam-and-security) | Permissions, credential issues, and best practices. |
| 📊 [3. Monitoring & Logging](#-monitoring--logging) | Use of CloudWatch, CloudTrail, and logs to debug problems. |
| 🛠 [4. Hands-On: Debugging with AWS CLI](#-hands-on-debugging-with-aws-cli) | CLI commands for common diagnostics. |

---

## 🐞 General Troubleshooting

### 💡 EC2
- Instance not starting? Check limits, AMI permissions, and instance types.
- Can't SSH? Check:
  - Security group allows port 22
  - Key pair exists and is correct
  - Network ACLs and routing

### 💡 S3
- 403 Access Denied? Verify:
  - Bucket policy and object ACLs
  - IAM user permissions
  - Bucket ownership

### 💡 VPC
- Can't access internet? Ensure:
  - Public subnet with route to Internet Gateway
  - Instance has public IP or Elastic IP

---

## 🔐 IAM and Security

### 💡 Common Issues:
- **AccessDenied** errors → Role/user lacks required policy.
- **AssumeRole failure** → Trust policy misconfigured.
- **MFA errors** → Check that device is configured and synced.

### 🔐 Best Practices:
- Use least privilege principle.
- Rotate access keys regularly.
- Use IAM roles instead of access keys for EC2.

---

## 📊 Monitoring & Logging

### 💡 Tools:
- **CloudWatch Logs**: Debug Lambda, ECS, EC2 issues.
- **CloudWatch Metrics**: Monitor CPU, memory, etc.
- **CloudTrail**: Track API calls for audit/security.
- **VPC Flow Logs**: Diagnose network access issues.

### 🌐 Example Use Case:
Use CloudTrail to track which IAM user deleted an S3 object.

---

## 🛠 Hands-On: Debugging with AWS CLI

### ✅ Describe EC2 Instance
```
aws ec2 describe-instances \
  --instance-ids i-1234567890abcdef0
```
---

### ✅ View Security Groups
```
aws ec2 describe-security-groups
```
---

### ✅ Get CloudWatch Logs
```
aws logs get-log-events \
  --log-group-name /aws/lambda/my-function \
  --log-stream-name <stream-name>
```
---

### ✅ Check IAM Policy Simulator
Visit:
https://policysim.aws.amazon.com/

---

### ✅ Check CloudTrail Events
```
aws cloudtrail lookup-events \
  --lookup-attributes AttributeKey=Username,AttributeValue=myuser
```
---

Troubleshooting and securing AWS requires understanding how services connect and are monitored. CloudWatch, IAM, and proper CLI usage are your best tools.
