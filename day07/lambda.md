# Lambda: Functions and Triggers

Click on each topic to go to the specific section.

| **Topic** | **Description** |
|----------|-----------------|
| ⚙️ [1. Lambda Functions](#-lambda-functions) | Serverless compute service to run code in response to events. |
| 🔗 [2. Triggers](#-triggers) | AWS services/events that invoke Lambda functions. |
| 💾 [3. Lambda Layers](#-lambda-layers) | Share code/libraries across multiple Lambda functions. |
| 🔒 [4. Permissions (IAM Role)](#-permissions-iam-role) | Grant Lambda permissions to access AWS services. |
| 🔧 [5. Hands-On: Lambda with AWS CLI](#-hands-on-lambda-with-aws-cli) | Common CLI commands to manage Lambda functions. |

---

## ⚙️ Lambda Functions

Lambda lets you run code without provisioning servers. Just upload your code, and Lambda handles the rest.

### 💡 Key Points:
- Supports multiple runtimes (Node.js, Python, Java, Go, etc.).
- Automatically scales with incoming requests.
- Billed per request and execution time (ms).
- Max timeout: 15 minutes.
- Can access environment variables and VPC resources.

### 🌐 Example Use Case:
You write a Lambda function that resizes images uploaded to an S3 bucket.

---

## 🔗 Triggers

Triggers are events or services that invoke Lambda functions.

### 💡 Key Points:
- Common triggers:
  - S3 (object created)
  - API Gateway (HTTP request)
  - CloudWatch Events (scheduled)
  - DynamoDB Streams (record change)
  - EventBridge (custom events)
- You can manually invoke Lambda too (e.g., via CLI or SDK).

### 🌐 Example Use Case:
You trigger a Lambda function every time a new item is added to a DynamoDB table.

---

## 💾 Lambda Layers

Layers let you package external libraries and share them across functions.

### 💡 Key Points:
- Up to 5 layers per function.
- Useful for dependencies (e.g., Python packages, Node modules).
- Reduces duplication and makes functions smaller.

### 🌐 Example Use Case:
You use a layer that includes the AWS SDK v3 for all your Node.js functions.

---

## 🔒 Permissions (IAM Role)

Each Lambda function needs an **execution role** (IAM role) that grants access to AWS resources.

### 💡 Key Points:
- Use IAM policies to define allowed actions.
- Common permissions:
  - Write logs to CloudWatch
  - Access S3, DynamoDB, SNS, etc.
- Least privilege is recommended.

### 🌐 Example Use Case:
You attach a policy allowing `s3:GetObject` so the Lambda can read from a bucket.

---

## 🔧 Hands-On: Lambda with AWS CLI

### ⚙️ Create a Lambda Function

#### ✅ Create a basic Lambda (Node.js)
```
aws lambda create-function \
  --function-name my-function \
  --runtime nodejs18.x \
  --role arn:aws:iam::123456789012:role/lambda-execution-role \
  --handler index.handler \
  --zip-file fileb://function.zip
```
---

### 🔗 Add a Trigger (S3 example)

#### ✅ Add permission for S3 to invoke Lambda
```
aws lambda add-permission \
  --function-name my-function \
  --statement-id s3invoke \
  --action "lambda:InvokeFunction" \
  --principal s3.amazonaws.com \
  --source-arn arn:aws:s3:::my-trigger-bucket \
  --source-account 123456789012
```

---

### 🔄 Update Function Code

#### ✅ Update code (new zip)
```
aws lambda update-function-code \
  --function-name my-function \
  --zip-file fileb://updated.zip
```
---

### ❌ Delete a Lambda Function
```
aws lambda delete-function --function-name my-function
```
---

In summary, Lambda is a powerful tool for building event-driven and serverless applications. Understanding functions, triggers, permissions, and deployment will help you use it effectively.
