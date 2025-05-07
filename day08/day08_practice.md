# Day 8 Practice – CloudFormation + AWS Support Tools

## 🚀 Goal
Learn how to use CloudFormation to define infrastructure as code and explore AWS support tools like Trusted Advisor and the Health Dashboard.


## ✅ Step-by-step

### 1. **Create a CloudFormation Template**
- Use this basic YAML template for launching an EC2 instance:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Simple EC2 instance
Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0c02fb55956c7d316  # Amazon Linux 2023 in us-east-1
      InstanceType: t2.micro
```
- Save the file as `ec2-basic.yaml`

---

### 2. **Deploy the Stack**
- [ ] Go to **CloudFormation → Create stack → With new resources**
- [ ] Choose **Upload a template file** and upload `ec2-basic.yaml`
- [ ] Click **Next**, give your stack a name (e.g., `BasicEC2Stack`)
- [ ] Click **Next** → Leave defaults → Click **Create stack**
- [ ] Wait until status is `CREATE_COMPLETE`

---

### 3. **Verify EC2 Instance**
- [ ] Go to **EC2 → Instances**
- [ ] You should see the new instance launched by CloudFormation

---

### 4. **Explore AWS Trusted Advisor**
- [ ] Go to **Trusted Advisor** from the AWS Console (use the search bar)
- [ ] Review checks for:
  - Cost optimization
  - Security
  - Fault tolerance
  - Service limits

> Note: Full Trusted Advisor access may require a Business or Enterprise support plan, but you still get some free checks.

---

### 5. **Check the AWS Health Dashboard**
- [ ] Go to **Health Dashboard** in the console
- [ ] Look for any events or scheduled maintenance in your region/account

---

## ✅ Done!
You now know how to provision infrastructure using CloudFormation and use AWS support tools to monitor and optimize your setup!
