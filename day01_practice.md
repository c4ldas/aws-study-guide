# Day 1 Practice - AWS IAM Users and AWS CLI S3 Bucket

## 🚀 Goal
- Create IAM users with limited permissions.
- Use the AWS CLI to create an S3 bucket.

## ✅ Step-by-step

### 1. **Create IAM Users with Limited Permissions**
- [ ] 1. Go to **IAM → Users → Add user**
- [ ] 2. Enter a **username** (e.g., `limited-user`)
- [ ] 3. Under **Access type**, select **Programmatic access** (to allow AWS CLI/API access).
- [ ] 4. Set **Permissions**:
  - Choose **Attach policies directly**
  - Attach the `AmazonS3ReadOnlyAccess` policy (for limited S3 permissions).
  - Optionally, attach other policies (like `IAMReadOnlyAccess` if you want the user to have read-only access to IAM).
- [ ] 5. Click **Next: Tags**, then **Next: Review**, and finally **Create user**.
- [ ] 6. Save the **Access key ID** and **Secret access key** (you’ll need these for CLI access).

### 2. **Set Up AWS CLI**
- [ ] 1. If you haven’t already, install the AWS CLI from [here](https://aws.amazon.com/cli/).
- [ ] 2. Open your terminal or command prompt and run the following command to configure the CLI with your new user’s credentials:
```bash
aws configure
```

- [ ] 3. When prompted, enter:
  - AWS Access Key ID: (from the IAM user you just created)
  - AWS Secret Access Key: (from the IAM user you just created)
  - Default region name: (choose your region, e.g., us-east-1)
  - Default output format: (choose json)

### 3. **Use AWS CLI to Create an S3 Bucket**
- [ ] 1. Now that your CLI is set up, create an S3 bucket with the following command:
```bash
aws s3 mb s3://my-unique-bucket-name --region us-east-1
```
- [ ] 2. Replace my-unique-bucket-name with a unique name (AWS S3 bucket names must be globally unique).
- [ ] 3. Verify that the bucket was created by listing your S3 buckets:
```bash
aws s3 ls
```
- [ ] 4. You should see the newly created bucket in the list.

## ✅ Done!
You’ve created an IAM user with limited permissions and used the AWS CLI to create an S3 bucket.

🔑 Pro Tip: You can manage multiple IAM users, roles, and policies through AWS IAM to secure your AWS environment and grant only the necessary permissions.
