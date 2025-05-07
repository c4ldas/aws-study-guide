# Infrastructure as Code: CloudFormation Basics

Click on each topic to go to the specific section.

| **Topic** | **Description** |
|----------|-----------------|
| 🧱 [1. What is CloudFormation?](#-what-is-cloudformation) | AWS service to define and provision infrastructure as code. |
| 📄 [2. Template Structure](#-template-structure) | Core components of a CloudFormation template. |
| 🚀 [3. Deploying Stacks](#-deploying-stacks) | How to launch CloudFormation stacks. |
| 🔁 [4. Updating & Deleting Stacks](#-updating--deleting-stacks) | Change or remove your infrastructure declaratively. |
| 🛠 [5. Hands-On: CloudFormation via AWS CLI](#-hands-on-cloudformation-via-aws-cli) | CLI commands for deploying and managing stacks. |

---

## 🧱 What is CloudFormation?

CloudFormation lets you define AWS resources using JSON or YAML templates, enabling repeatable and version-controlled infrastructure.

### 💡 Key Points:
- Automates provisioning and updating infrastructure.
- Supports almost all AWS services.
- Templates are declarative and human-readable.
- Ideal for team environments and CI/CD pipelines.

### 🌐 Example Use Case:
You define a template that creates a VPC, subnets, and an EC2 instance, and deploy it across multiple environments.

---

## 📄 Template Structure

CloudFormation templates follow a structured format:

### 💡 Sections:
- **AWSTemplateFormatVersion**: Optional version declaration.
- **Description**: Human-readable description of the stack.
- **Parameters**: Accept user inputs.
- **Resources**: The only required section — defines AWS resources.
- **Outputs**: Values returned after stack creation (e.g., instance ID).
- **Conditions, Mappings, Metadata**: Advanced customization options.

### 🌐 Example Use Case:
A parameter lets you choose the EC2 instance type when launching a stack.

---

## 🚀 Deploying Stacks

You can deploy a stack using:

- AWS Console (guided form)
- AWS CLI
- SDKs or IaC tools (e.g., CDK)

### 💡 Key Concepts:
- **Stack**: A collection of AWS resources managed together.
- **Change Set**: A preview of changes before updating a stack.

### 🌐 Example Use Case:
You deploy a stack from a YAML template stored in an S3 bucket.

---

## 🔁 Updating & Deleting Stacks

When requirements change, you can update or delete stacks safely.

### 💡 Key Actions:
- **Update Stack**: Provide a modified template.
- **Delete Stack**: Removes all resources (be cautious).
- **Rollback**: Automatically reverts changes on failure.

### 🌐 Example Use Case:
You add an output for the public IP of an EC2 instance and update the stack.

---

## 🛠 Hands-On: CloudFormation via AWS CLI

### ✅ Deploy a New Stack
```
aws cloudformation create-stack \
  --stack-name my-stack \
  --template-body file://template.yaml \
  --capabilities CAPABILITY_IAM
```
---

### ✅ Validate a Template Before Deploying
```
aws cloudformation validate-template \
  --template-body file://template.yaml
```
---

### ✅ Describe a Stack
```
aws cloudformation describe-stacks \
  --stack-name my-stack
```
---

### ✅ Update an Existing Stack
```
aws cloudformation update-stack \
  --stack-name my-stack \
  --template-body file://template.yaml \
  --capabilities CAPABILITY_IAM
```
---

### ✅ Delete a Stack
```
aws cloudformation delete-stack \
  --stack-name my-stack
```
---

In summary, CloudFormation enables infrastructure as code by defining your AWS environment in templates, supporting version control, consistency, and automation.
