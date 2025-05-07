# S3: Event Notifications

Click on each topic to go to the specific section.

| **Topic** | **Description** |
|----------|-----------------|
| 🔔 [1. What Are S3 Event Notifications?](#-what-are-s3-event-notifications) | Mechanism to trigger actions when S3 events occur. |
| 📂 [2. Supported Event Types](#-supported-event-types) | Events like object creation, deletion, etc. |
| 🎯 [3. Destinations](#-destinations) | Where notifications are sent (Lambda, SQS, SNS). |
| ⚙️ [4. Configuring Notifications](#-configuring-notifications) | Methods to configure event notifications. |
| 🔧 [5. Hands-On: S3 Notifications via AWS CLI](#-hands-on-s3-notifications-via-aws-cli) | CLI example for adding a Lambda trigger. |

---

## 🔔 What Are S3 Event Notifications?

S3 can automatically send notifications when certain events happen in a bucket. This is commonly used to trigger downstream processing.

### 💡 Key Points:
- Enables serverless automation with services like Lambda, SQS, and SNS.
- Helps build event-driven architectures.
- Configured per bucket.

### 🌐 Example Use Case:
You want to trigger a Lambda function every time a user uploads a file to a bucket.

---

## 📂 Supported Event Types

You can listen to a variety of events related to objects in S3.

### 💡 Common Events:
- `s3:ObjectCreated:*` — All object creation events
- `s3:ObjectCreated:Put` — PUT requests
- `s3:ObjectCreated:Post` — POST requests
- `s3:ObjectRemoved:*` — All delete events
- `s3:ReducedRedundancyLostObject` — RRS object lost

### 🌐 Example Use Case:
Trigger processing when new images are uploaded to a specific folder (prefix filter: `images/`).

---

## 🎯 Destinations

S3 can send notifications to the following destinations:

### 💡 Destinations:
- **Lambda** — Trigger functions for processing.
- **SQS** — Queue the events for decoupled processing.
- **SNS** — Broadcast the event to subscribers.

### 🌐 Example Use Case:
Send S3 delete events to an SNS topic to alert admins.

---

## ⚙️ Configuring Notifications

You can configure event notifications using:

- AWS Console (easiest)
- AWS CLI
- SDKs or IaC (e.g., CloudFormation, Terraform)

### 💡 Notes:
- Only one event notification configuration can exist per bucket (contains multiple rules).
- Use filters to scope notifications:
  - **Prefix** — Limit to keys starting with a certain string.
  - **Suffix** — Limit to keys ending with a certain string (e.g., `.jpg`).

---

## 🔧 Hands-On: S3 Notifications via AWS CLI

### ✅ Add Permission for Lambda to Be Invoked by S3
```
aws lambda add-permission \
  --function-name my-s3-function \
  --statement-id s3invoke \
  --action "lambda:InvokeFunction" \
  --principal s3.amazonaws.com \
  --source-arn arn:aws:s3:::my-bucket \
  --source-account 123456789012
```
---

### ✅ Create Notification Configuration JSON
```json
{
  "LambdaFunctionConfigurations": [
    {
      "Id": "ProcessUploads",
      "LambdaFunctionArn": "arn:aws:lambda:us-east-1:123456789012:function:my-s3-function",
      "Events": ["s3:ObjectCreated:*"],
      "Filter": {
        "Key": {
          "FilterRules": [
            {
              "Name": "prefix",
              "Value": "uploads/"
            },
            {
              "Name": "suffix",
              "Value": ".jpg"
            }
          ]
        }
      }
    }
  ]
}
```
---

### ✅ Apply Notification Configuration to the Bucket
```
aws s3api put-bucket-notification-configuration \
  --bucket my-bucket \
  --notification-configuration file://notification.json
```
---

### ✅ Get Current Notification Configuration
```
aws s3api get-bucket-notification-configuration \
  --bucket my-bucket
```
---

In summary, S3 event notifications allow you to respond to changes in S3 buckets by sending events to other AWS services, helping build scalable and automated workflows.
