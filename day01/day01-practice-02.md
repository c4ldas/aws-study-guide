# Day 1 Practice 02 - AWS IAM Users and AWS CLI S3 Bucket

### Activity 1: Explore AWS Global Infrastructure
**Goal**: Understand AWS Regions, Availability Zones, and Global Services.
- **Steps**:
1. Go to the [AWS Global Infrastructure page](https://aws.amazon.com/about-aws/global-infrastructure/).
2. Learn about AWS Regions and Availability Zones.
3. Identify your preferred region for resource creation (e.g., `us-east-1`).
4. Use the AWS CLI to list available regions:

```bash
aws ec2 describe-regions --query "Regions[*].RegionName"
```
5. Review the concept of AWS global services (e.g., Route 53, CloudFront) and why they are region-independent.

### Activity 2: Create an S3 Bucket with Versioning Enabled
**Goal**: Practice creating an S3 bucket and enable versioning.
- **Steps**:
1. Use the AWS CLI to create a new S3 bucket:
```bash
aws s3 mb s3://my-unique-bucket-name --region us-east-1
```
2. Enable versioning on the newly created bucket:
```bash
aws s3api put-bucket-versioning --bucket my-unique-bucket-name --versioning-configuration Status=Enabled
```
3. Verify that versioning is enabled:
```bash
aws s3api get-bucket-versioning --bucket my-unique-bucket-name
```

### Activity 3: Upload and Manage Files in S3
**Goal**: Learn how to upload, list, and delete files in an S3 bucket.
- **Steps**:
1. Upload a file to your S3 bucket:
   
```bash
aws s3 cp my-file.txt s3://my-unique-bucket-name/
```
2. List the contents of the S3 bucket:

```bash
aws s3 ls s3://my-unique-bucket-name/
```
3. Delete the file from the S3 bucket:

```bash
aws s3 rm s3://my-unique-bucket-name/my-file.txt
```

### Activity 4: Create a Bucket Policy for Access Control
**Goal**: Practice creating an S3 bucket policy to control access.
- **Steps**:
1. Create a simple bucket policy that allows read-only access to your S3 bucket:
2. 
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-unique-bucket-name/*"
    }
  ]
}
```
2. Apply the policy to your bucket using the AWS CLI:

```bash
aws s3api put-bucket-policy --bucket my-unique-bucket-name --policy file://policy.json
```
3. Verify the policy is applied correctly by retrieving it:

```bash
aws s3api get-bucket-policy --bucket my-unique-bucket-name
```

### Activity 5: Create a Custom IAM Policy for S3 Actions
**Goal**: Create a custom IAM policy that grants specific S3 permissions.
- **Steps**:
1. Create a policy JSON file that allows only the `s3:ListBucket` and `s3:GetObject` actions.
2. Go to IAM → Policies → Create Policy and select JSON.
3. Paste your policy and give it a name (e.g., `S3ReadOnlyPolicy`).
4. Attach the new policy to the IAM user you created earlier.
