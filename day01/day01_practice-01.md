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

### 2.1 **Add permissions for S3 Bucket creation**
To allow bucket creation, first add these permissions:
- [ ] 1. Go to IAM > Policies > Create policy
- [ ] 2. Select JSON
- [ ] 3. Paste this policy:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:CreateBucket",
        "s3:PutBucketPolicy",
        "s3:PutBucketAcl",
        "s3:ListBucket",
        "s3:PutBucketVersioning"
      ],
      "Resource": "arn:aws:s3:::*"
    }
  ]
}
```
- [ ] 4. Click Next and give it a name (i.e.: `S3CreateBucketPolicy-test`), add a description, tag and click on Create policy

### 2.2 **Attach the Policy to `limited-user`**
- [ ] 1. Go to IAM > Users
- [ ] 2. Click on `limited-user` > Permissions > Add permissions
- [ ] 3. Choose **Attach policies directly**
- [ ] 4. Search for the custom policy recently created (`S3CreateBucketPolicy-test`) and check the box
- [ ] 5. Click Next > Add permissions


### 3. **Use AWS CLI to Create an S3 Bucket**
- [ ] 1. Now that your CLI is set up, create an S3 bucket with the following command:
```bash
aws s3 mb s3://my-unique-bucket-name-20250513 --region us-east-1
```
- [ ] 2. Replace `my-unique-bucket-name-20250513` with a unique name (AWS S3 bucket names must be globally unique. Using a timestamp in your bucket name is a good way to ensure this).
- [ ] 3. Verify that the bucket was created by listing your S3 buckets:
```bash
aws s3 ls
```
- [ ] 4. You should see the newly created bucket in the list.

## ✅ Done!
You've created an IAM user with limited permissions and used the AWS CLI to create an S3 bucket.

🔑 Pro Tip: You can manage multiple IAM users, roles, and policies through AWS IAM to secure your AWS environment and grant only the necessary permissions.

## Additional notes:

JSON explanation:

Refer to the JSON code in [step 2.1](#21-add-permissions-for-s3-bucket-creation).

`"Version": "2012-10-17"`
- This defines the version of the policy language.
- "2012-10-17" is the latest stable version used in almost all policies.

`"Statement": [ ... ]`
- This is the array of permissions you're defining.
- Each object inside this array is a statement that grants or denies access.

`"Effect": "Allow"`
- Means you're allowing these actions (instead of "Deny").
- IAM policies are deny-by-default, so you need to explicitly allow what you need.

`"Action": [ ... ]`
- This lists the exact operations the user is allowed to perform:

| Action                     | What it allows                                                   |
| -------------------------- | ---------------------------------------------------------------- |
| `"s3:CreateBucket"`        | Create a new S3 bucket.                                          |
| `"s3:PutBucketPolicy"`     | Attach or update a bucket policy (for controlling access to it). |
| `"s3:PutBucketAcl"`        | Set permissions using ACLs (another way to control access).      |
| `"s3:ListBucket"`          | List objects inside a bucket, and list available buckets.        |
| `"s3:PutBucketVersioning"` | Enable or configure versioning on a bucket.                      |

`"Resource": "arn:aws:s3:::*"`
- This applies the permissions to all S3 buckets in your account (* is a wildcard).
- The format is: `arn:aws:s3:::bucket-name`
- So using * means it applies to any bucket. For production, change `"Resource": "arn:aws:s3:::*"` to `"arn:aws:s3:::my-unique-bucket-name"` for least privilege.

#### Skeleton 
This is a core skeleton of an IAM policy that can be used as a template:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "service:Action1",
        "service:Action2"
      ],
      "Resource": "arn:aws:service:::resource"
    }
  ]
}
```

### 🛠 Optional Additions

You can add more keys when needed:

- **`"Condition"`**:  
  This key allows you to create more granular controls based on conditions. Conditions can help you enforce security policies like limiting access to certain IPs or enforcing multi-factor authentication (MFA). You can use the `"Condition"` key to define rules for various attributes, such as:
  
  **Examples of conditions**:
  - **IP Address Restriction**:  
    Only allow access to the resource from specific IP addresses.
    ```json
    "Condition": {
      "IpAddress": {
        "aws:SourceIp": "192.168.1.1/32"
      }
    }
    ```
  - **MFA Requirement**:  
    Enforce multi-factor authentication for sensitive operations like deleting objects.
    ```json
    "Condition": {
      "Bool": {
        "aws:MultiFactorAuthPresent": "true"
      }
    }
    ```
  - **Time-Based Access**:  
    Allow access only during specific hours.
    ```json
    "Condition": {
      "DateGreaterThan": {
        "aws:CurrentTime": "2025-01-01T00:00:00Z"
      }
    }
    ```

  **Why use `"Condition"`?**  
  - It helps you enforce security policies that fit your organization's specific needs.
  - Conditions allow you to limit access based on time, location, or user context (e.g., MFA), reducing the risk of unauthorized access.

- **`"Principal"`**:  
  The `"Principal"` key defines the entity that is the subject of the policy (who the policy applies to). While this is primarily used in **bucket policies**, it can also be used in certain IAM roles and cross-account access policies. The `"Principal"` is typically an AWS account, IAM user, IAM role, or federated user.

  **Examples of `"Principal"`**:
  - **AWS Account**:  
    Allow access to a specific AWS account.
    ```json
    "Principal": {
      "AWS": "arn:aws:iam::123456789012:root"
    }
    ```
  - **IAM Role**:  
    Allow a specific IAM role to perform actions on the resource.
    ```json
    "Principal": {
      "AWS": "arn:aws:iam::123456789012:role/ExampleRole"
    }
    ```
  - **Federated User**:  
    Allow access to a federated user authenticated through SSO or external identity provider.
    ```json
    "Principal": {
      "Federated": "arn:aws:sts::123456789012:assumed-role/FederatedRole/ExampleUser"
    }
    ```

  **Why use `"Principal"`?**  
  - It's essential for cross-account access scenarios. For example, you may need to grant access to resources like an S3 bucket from a different AWS account.
  - `"Principal"` ensures that only specific entities (users, roles, or services) can assume permissions granted in a policy, improving security by limiting the scope of who can act.

### Key Points:
- **Using `"Condition"`**: Allows fine-tuning of access, making your policies more secure and specific.
- **Using `"Principal"`**: Controls which entities (users, roles, accounts) can access your resources, particularly useful in cross-account or federated access scenarios.

