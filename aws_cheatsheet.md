# 💻 AWS Cheatsheet + Mock Interview Prep

## ☁️ Core AWS Services Summary

### EC2 (Elastic Compute Cloud)

* **What**: Virtual servers in the cloud
* **When**: You need full control of the OS, or to run custom backend services
* **How**:

  * Launch instance from console or CLI
  * Use SSH to connect
  * Manage with security groups and key pairs

### S3 (Simple Storage Service)

* **What**: Object storage service
* **When**: Store files, backups, website assets, etc.
* **How**:

  * Create a bucket
  * Upload/download via console or CLI
  * Manage access with bucket policies and ACLs

### IAM (Identity and Access Management)

* **What**: Manages users, roles, and permissions
* **When**: Always – controls access across AWS
* **How**:

  * Create users/roles
  * Attach policies (JSON-based)
  * Use MFA and least privilege principle

### Lambda

* **What**: Serverless function execution
* **When**: You want to run short code without managing servers
* **How**:

  * Create a function (Node.js, Python, etc.)
  * Set trigger (e.g., S3 upload)
  * Log via CloudWatch

### RDS (Relational Database Service)

* **What**: Managed database (MySQL, PostgreSQL, etc.)
* **When**: You need relational DB without admin overhead
* **How**:

  * Launch DB instance
  * Set up subnet group, security group
  * Connect via client (e.g., DBeaver, CLI)

### VPC (Virtual Private Cloud)

* **What**: Isolated network environment
* **When**: Always – every resource lives inside a VPC
* **How**:

  * Create subnets (public/private)
  * Add routing tables
  * Use NAT/Internet gateways for internet access

### Route 53

* **What**: DNS and routing
* **When**: You want to manage domains and traffic
* **How**:

  * Create hosted zone
  * Add records (A, CNAME, etc.)

### ELB (Elastic Load Balancer)

* **What**: Distributes traffic across EC2s
* **When**: You have multiple servers serving traffic
* **How**:

  * Set up an ALB
  * Register EC2 targets
  * Configure listeners and rules

### CloudWatch

* **What**: Monitoring and alerting tool
* **When**: You want to observe logs, metrics, and set alarms
* **How**:

  * Enable detailed monitoring
  * Create alarms (CPU > 80%)
  * Send alerts via SNS

### CloudFormation

* **What**: Infrastructure as Code (IaC)
* **When**: Automate consistent environments
* **How**:

  * Write YAML/JSON template
  * Deploy stack
  * Update/delete stack as needed

---

## 🧪 CLI Commands Cheat List

```sh
# S3
## Create a bucket
aws s3 mb s3://my-bucket-name

## Upload a file
aws s3 cp file.txt s3://my-bucket-name/

## Copy a file to S3
aws s3 cp file.txt s3://my-bucket-name/

## List files in a bucket
aws s3 ls s3://my-bucket-name/

## Sync a directory to S3 bucket
aws s3 sync ./local-directory/ s3://my-bucket-name/

## Delete a file from S3
aws s3 rm s3://my-bucket-name/file.txt

## Delete an empty bucket
aws s3 rb s3://my-bucket-name

## Enable versioning
aws s3api put-bucket-versioning --bucket my-bucket-name --versioning-configuration Status=Enabled


# EC2
## Describe EC2 instances
aws ec2 describe-instances

## Start an EC2 instance
aws ec2 start-instances --instance-ids i-1234abcd5678


## Stop an EC2 instance
aws ec2 stop-instances --instance-ids i-1234abcd5678

## Terminate an EC2 instance
aws ec2 terminate-instances --instance-ids i-1234abcd5678

## Create a key pair
aws ec2 create-key-pair --key-name my-key-pair --query 'KeyMaterial' --output text > my-key-pair.pem

## Get instance public IP
aws ec2 describe-instances --instance-ids i-1234abcd5678 --query 'Reservations[0].Instances[0].PublicIpAddress' --output text

## Create a security group
aws ec2 create-security-group --group-name my-security-group --description "My security group"



# IAM
## List IAM users
aws iam list-users

## Create an IAM user
aws iam create-user --user-name new-user

## Attach policy to user
aws iam attach-user-policy --user-name new-user --policy-arn arn:aws:iam::aws:policy/AdministratorAccess

## Create an IAM role
aws iam create-role --role-name my-role --assume-role-policy-document file://trust-policy.json

## List IAM roles
aws iam list-roles

## Create an IAM access key for user
aws iam create-access-key --user-name new-user

## Delete an IAM user
aws iam delete-user --user-name new-user




# CloudWatch
## Put a metric alarm
aws cloudwatch put-metric-alarm --alarm-name HighCPU --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 80 --comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 2 --alarm-actions arn:aws:sns:us-west-2:123456789012:my-sns-topic

## Describe alarms
aws cloudwatch describe-alarms

## List metrics
aws cloudwatch list-metrics --namespace AWS/EC2

## Get logs from CloudWatch log group
aws logs filter-log-events --log-group-name my-log-group

## Delete an alarm
aws cloudwatch delete-alarms --alarm-names HighCPU

# VPC

## Create a VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16

## Create a subnet
aws ec2 create-subnet --vpc-id vpc-1234abcd --cidr-block 10.0.1.0/24

## Create a subnet in a specific availability zone
aws ec2 create-subnet --vpc-id vpc-12345678 --cidr-block 89.207.132.170/24 --availability-zone us-west-2a

## Create an internet gateway
aws ec2 create-internet-gateway

## Attach internet gateway to VPC
aws ec2 attach-internet-gateway --vpc-id vpc-1234abcd --internet-gateway-id igw-1234abcd

## Create a route table
aws ec2 create-route-table --vpc-id vpc-1234abcd

# Lambda

## Create a Lambda function
aws lambda create-function --function-name my-function --runtime nodejs14.x --role arn:aws:iam::123456789012:role/my-role --handler index.handler --zip-file fileb://index.zip

## List Lambda functions
aws lambda list-functions

## Invoke a Lambda function
aws lambda invoke --function-name MyFunction output.txt

## Delete a Lambda function
aws lambda delete-function --function-name MyFunction

## Update a Lambda function code
aws lambda update-function-code --function-name MyFunction --zip-file fileb://index.zip
```

---

## 🎤 Mock Interview Questions

### General

* What’s the difference between EC2 and Lambda?
  * EC2 (Elastic Compute Cloud) is a scalable virtual server where you manage the operating system, updates, scaling, and infrastructure. It's great for applications that need persistent running compute resources.
  * Lambda is a serverless compute service where you only write code, and AWS automatically runs it in response to events (e.g., file uploads, HTTP requests). You don't manage servers or scaling; it automatically scales for you and charges only for execution time.

* How do IAM policies differ from security groups?
  * IAM Policies are used to manage access to AWS resources based on users, groups, or roles. They define who can access what resources and what actions they can perform (e.g., read, write, delete).
  * Security Groups are virtual firewalls that control inbound and outbound traffic to EC2 instances. They define which network traffic is allowed to and from resources like EC2.

* How do you debug a 403 error in S3?
  * A 403 error typically means the user or service doesn’t have permission to access the resource.
  * Steps to troubleshoot:
  * Check the S3 bucket's Bucket Policy to ensure access is granted to the correct user or role.
  * Check IAM policies to ensure the user or role has the necessary permissions (s3:GetObject, s3:ListBucket, etc.).
  * Verify if the object is publicly accessible or if it’s blocked by a Bucket ACL.
  * Ensure any CORS or VPC settings aren’t restricting access.

* What’s the difference between CloudFormation and Terraform?
  * CloudFormation is a service that automates the creation and management of AWS infrastructure resources. It allows you to define your infrastructure as code, enabling the automatic creation, management, and updating of AWS resources in a repeatable and consistent manner.
  * Terraform is an open-source infrastructure as code tool used for building, changing, and versioning infrastructure safely and efficiently. It provides a declarative syntax for defining AWS infrastructure resources, making it easier to manage and maintain AWS resources.  

### Scenario-Based

* A server can’t access the internet. What would you check?
  * Check if the EC2 instance is in a public subnet with an Internet Gateway attached to the VPC.
  * Verify that the instance has an Elastic IP (if needed).
  * Ensure the instance's security group allows outbound traffic (e.g., allow TCP/80, 443).
  * Check the route table to make sure the instance has a default route (0.0.0.0/0) pointing to the Internet Gateway.
  * If using a private subnet, verify that a NAT Gateway is set up and working.

* Your Lambda isn’t triggered on S3 upload. How do you troubleshoot?
  * Check the S3 bucket event configuration to ensure it's set to trigger the Lambda on the correct event (e.g., s3:ObjectCreated).
  * Verify that the Lambda’s execution role has permission to access the S3 bucket.
  * Check the Lambda function logs in CloudWatch for any errors.
  * Ensure that the S3 bucket policy allows events to trigger the Lambda (sometimes buckets have restricted event policies).

* An EC2 instance isn’t accessible via SSH. How do you fix it?
  * Check the Security Group associated with the EC2 instance and ensure it allows inbound traffic on port 22 (SSH).
  * Verify the network ACLs for the subnet to ensure they’re not blocking SSH.
  * Ensure the instance is running and has a public IP if it’s in a public subnet.
  * Check if the instance's SSH key is correctly added and that you're using the right one.
  * If the instance is using a private subnet, ensure it has internet access via a NAT Gateway or is connected to a VPN.

### Deep Dive

* How does a NAT Gateway differ from an Internet Gateway?
  * An Internet Gateway is used to allow communication between instances in a VPC and the internet. It provides bi-directional communication between resources in a public subnet and the internet.
  * A NAT Gateway allows instances in a private subnet to initiate outbound traffic to the internet (e.g., for software updates) while blocking inbound traffic from the internet. It allows one-way traffic to the internet.

* How does versioning work in S3?
  * Versioning in S3 allows you to keep multiple versions of an object in a bucket. When versioning is enabled, each new upload of an object with the same key will create a new version, while preserving the older versions.
  * You can retrieve, restore, or permanently delete any previous version of the object. This feature is useful for backup, data protection, and recovery.

* What’s the benefit of using CloudFormation vs manually creating resources?
  * CloudFormation allows you to define your infrastructure as code (IaC), enabling the automatic creation, management, and updating of AWS resources in a repeatable and consistent manner. It eliminates human error and provides version control for infrastructure changes.
  * Manually creating resources involves configuring each service through the console or CLI, which can lead to inconsistencies, errors, and difficult-to-reproduce setups.

---

## 📌 Bookmark These Docs

* [https://docs.aws.amazon.com/](https://docs.aws.amazon.com/)
* [https://explore.skillbuilder.aws/](https://explore.skillbuilder.aws/)
* [https://github.com/open-guides/og-aws](https://github.com/open-guides/og-aws)

---
