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

### 2.1 **Add additional permissions**
Before proceeding to the next step where you are going to create an S3 Bucket, the user needs additional permissions to create that bucket.
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
- [ ] 4. Seach for the custom policy recently created (`S3CreateBucketPolicy-test`) and check the box
- [ ] 5. Click Next > Add permissions


### 3. **Use AWS CLI to Create an S3 Bucket**
- [ ] 1. Now that your CLI is set up, create an S3 bucket with the following command:
```bash
aws s3 mb s3://my-unique-bucket-name-20250513 --region us-east-1
```
- [ ] 2. Replace `my-unique-bucket-name-20250513` with a unique name (AWS S3 bucket names must be globally unique, so using timestamp in the name is a good call).
- [ ] 3. Verify that the bucket was created by listing your S3 buckets:
```bash
aws s3 ls
```
- [ ] 4. You should see the newly created bucket in the list.

## ✅ Done!
You’ve created an IAM user with limited permissions and used the AWS CLI to create an S3 bucket.

🔑 Pro Tip: You can manage multiple IAM users, roles, and policies through AWS IAM to secure your AWS environment and grant only the necessary permissions.

## Additional notes:

JSON explanation:

THe following JSON was used to create a custom policy:

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
- So using * means it applies to any bucket.

#### Skeleton 
This is a core skeleton of an IAM policy that can be used as a template:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow", // or "Deny"
      "Action": [
        "service:Action1",
        "service:Action2"
      ],
      "Resource": "arn:aws:service:::resource"
    }
  ]
}
```

#### 🛠 Optional Additions

You can add more keys when needed:

- `"Condition"`: Add rules like "only allow from this IP."
- `"Principal"`: Specify who the policy is for (used mostly in bucket policies, not IAM ones).
