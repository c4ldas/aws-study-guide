# IAM: Identity vs Resource-Based Policies

Click on each topic to go to the specific section.

| **Topic** | **Description** |
|----------|-----------------|
| 🧑‍💼 [1. Identity-Based Policies](#-identity-based-policies) | Permissions attached to IAM users, groups, or roles. |
| 📦 [2. Resource-Based Policies](#-resource-based-policies) | Permissions embedded in the resource (e.g., S3 bucket). |
| 🔄 [3. Policy Evaluation Logic](#-policy-evaluation-logic) | How AWS determines access using multiple policies. |
| 🛠 [4. Hands-On: Policy Examples and Debugging](#-hands-on-policy-examples-and-debugging) | Examples and tools to simulate/test permissions. |

---

## 🧑‍💼 Identity-Based Policies

These are attached directly to IAM users, groups, or roles.

### 💡 Key Points:
- Define *what actions* are allowed on *which resources*.
- Can be **AWS-managed** or **customer-managed**.
- Default *deny*, must explicitly *allow* access.
- Can include condition keys (e.g., `aws:MultiFactorAuthPresent`).

### 🌐 Example Use Case:
An IAM user is granted read-only access to all S3 buckets using `AmazonS3ReadOnlyAccess` managed policy.

---

## 📦 Resource-Based Policies

Defined *on the resource* itself, not the user/role.

### 💡 Key Points:
- Common with S3, SNS, SQS, Lambda.
- Let you grant access to **other AWS accounts** or **IAM roles**.
- Can complement identity policies or work independently.
- Includes a **Principal** element to define who has access.

### 🌐 Example Use Case:
An S3 bucket policy allows a specific IAM role from another AWS account to read its contents.

---

## 🔄 Policy Evaluation Logic

### 💡 How AWS Decides:
1. **By default, everything is denied.**
2. Identity policy *allows* → access might be granted.
3. Resource policy *allows* → access might be granted.
4. **Explicit Deny always wins**.
5. If no policy allows → access denied.

---

## 🛠 Hands-On: Policy Examples and Debugging

### ✅ Simulate a Policy
```
aws iam simulate-principal-policy \
  --policy-source-arn arn:aws:iam::123456789012:user/my-user \
  --action-names s3:ListBucket \
  --resource-arns arn:aws:s3:::my-bucket
```
---

### ✅ Get Inline and Attached Policies
```
aws iam list-attached-user-policies \
  --user-name my-user

aws iam list-user-policies \
  --user-name my-user
```
---

### ✅ View S3 Bucket Policy
```
aws s3api get-bucket-policy \
  --bucket my-bucket
```
---

### ✅ Test Permissions in Console
Visit:
https://policysim.aws.amazon.com/

---

Understanding the difference between identity-based and resource-based policies helps you design secure, flexible access controls in AWS.
