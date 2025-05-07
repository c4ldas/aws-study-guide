# AWS CLI Basics

Click on each topic to go to the specific section.

<table>
  <tr>
    <th><strong>Topic</strong></th>
    <th><strong>Description</strong></th>
  </tr>
  <tr>
    <td>💻 <a href="aws-cli-basics.md#--aws-cli-introduction">1. AWS CLI Introduction</a></td>
    <td>
      <p>- Overview of what the AWS CLI is and how it helps in managing AWS services from the command line.</p>
    </td>
  </tr>
  <tr>
    <td>🔧 <a href="aws-cli-basics.md#--aws-cli-configuration">2. AWS CLI Configuration</a></td>
    <td>
      <p>- Configuring your AWS CLI with access keys and region setup.</p>
    </td>
  </tr>
  <tr>
    <td>📡 <a href="aws-cli-basics.md#--basic-commands">3. Basic Commands</a></td>
    <td>
      <p>- Introduction to common AWS CLI commands for managing resources.</p>
    </td>
  </tr>
  <tr>
    <td>⚙️ <a href="aws-cli-basics.md#--advanced-commands">4. Advanced Commands</a></td>
    <td>
      <p>- Explore more advanced AWS CLI options and usage.</p>
    </td>
  </tr>
  <tr>
    <td>🛠 <a href="aws-cli-basics.md#--output-formats-and-filtering">5. Output Formats and Filtering</a></td>
    <td>
      <p>- Learn how to format output and filter data returned from AWS services.</p>
    </td>
  </tr>
  <tr>
    <td>⚡ <a href="aws-cli-basics.md#--scripting-and-automation">6. Scripting and Automation</a></td>
    <td>
      <p>- Use AWS CLI in scripts for automating repetitive tasks and managing resources in bulk.</p>
    </td>
  </tr>
  <tr>
    <td>🔍 <a href="aws-cli-basics.md#--troubleshooting-and-errors">7. Troubleshooting and Errors</a></td>
    <td>
      <p>- Identify common errors and how to resolve issues when using the AWS CLI.</p>
    </td>
  </tr>
    <tr>
    <td>🔍 <a href="aws-cli-basics.md#--command-examples">8. Command Examples</a></td>
    <td>
      <p>- List of useful commands.</p>
    </td>
  </tr>
</table>

## - AWS CLI Introduction

The AWS Command Line Interface (CLI) is a unified tool to manage AWS services. It provides a way to interact with AWS services from the command line, allowing you to automate tasks and manage AWS resources efficiently.

### ⚙️ Key Points about AWS CLI:
- **Cross-platform**: Works on Windows, macOS, and Linux.
- **Scriptable**: Great for automating tasks like provisioning EC2 instances, creating S3 buckets, managing IAM users, etc.
- **Service Support**: Supports most AWS services.
- **Interactive or Scripted**: You can run one-off commands or automate them in shell scripts.

---

## - AWS CLI Configuration

Before using the AWS CLI, you need to configure it with your AWS credentials, default region, and output format. This can be done using the aws configure command.

### 💡 Setting up AWS CLI:
To configure your AWS CLI, run:
```bash
aws configure
```
You’ll be prompted for the following:
1. **AWS Access Key ID**
2. **AWS Secret Access Key**
3. **Default region name** (e.g., us-east-1)
4. **Default output format** (json, text, or table)

---

## - Basic Commands

The AWS CLI allows you to interact with AWS resources. Here are some common commands:

### 🌐 List S3 Buckets:
```bash
aws s3 ls
```
### 🚀 Describe EC2 Instances:
```bash
aws ec2 describe-instances
```
### 💼 List IAM Users:
```bash
aws iam list-users
```
### 🔒 Create an IAM User:
```bash
aws iam create-user --user-name NewUser
```
---

## - Advanced Commands

Once you're comfortable with basic commands, you can start using more advanced features, like filtering results, paginating, and combining commands.

### 🔍 Filter EC2 Instances:
```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].InstanceId'
```

### ⏳ Paginate Results:
```bash
aws ec2 describe-instances --max-items 10
```
### 🎯 Run Multiple Commands:
```bash
aws s3 cp file.txt s3://my-bucket/ && aws ec2 describe-instances
```
---

## - Output Formats and Filtering

The AWS CLI provides several output formats and allows you to filter and customize results.

### 🧩 Querying with --query:
```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].InstanceId'
```
### 🗣 Output Formats:
You can specify the output format with the --output flag:

- json (default)
- table
- text

Example:
```bash
aws ec2 describe-instances --output table
```
---

## - Scripting and Automation

The AWS CLI is great for automating AWS tasks using shell scripts.

### 🔄 Running Scripts:
Example Bash script to start an EC2 instance:
```bash
#!/bin/bash  
aws ec2 start-instances --instance-ids i-0abcd1234efgh5678
```

### 🕹 Scheduled Tasks:
You can automate scripts to run at specific intervals using cron jobs (Linux/macOS) or Task Scheduler (Windows).
```bash
0 0 * * * /usr/local/bin/aws s3 sync /local/path s3://my-bucket
```

---

## - Troubleshooting and Errors

AWS CLI provides error messages that are helpful for troubleshooting. Common issues include incorrect IAM permissions or missing arguments.

### ⚠️ Common Errors:
- **Access Denied**  
  This typically occurs if your IAM user does not have the correct permissions.

- **Invalid Argument**  
  You might have forgotten to specify a required argument for a command.

Example error:
An error occurred (AccessDenied) when calling the ListBuckets operation: Access Denied

### 🔍 Logs and Debugging:
Use the --debug flag to get more details:
aws s3 ls --debug

This will provide a detailed log of the API request, helpful for debugging.

## - Command Examples

Here are some commands that you can find useful.

### Listing Resources
You can list resources with the `describe` or `ls` operations, depending on the service:
```bash
aws ec2 describe-instances
aws s3 ls
aws iam list-users
```

### Creating Resources
Most AWS services allow resource creation via the CLI. For example, to create an EC2 instance:
```bash
aws ec2 run-instances --image-id ami-12345678 --instance-type t2.micro
```

### Deleting Resources
To delete resources, use the `delete` or `terminate` commands:
```bash
aws ec2 terminate-instances --instance-ids i-12345678
aws s3 rm s3://my-bucket-name/my-file.txt
```

### Updating Resources
Some resources, like security groups or EC2 instances, allow modification:
```bash
aws ec2 modify-instance-attribute --instance-id i-12345678 --attribute instanceType --value t2.medium
```

### Tagging Resources
You can tag AWS resources to organize and manage them:
```bash
aws ec2 create-tags --resources i-12345678 --tags Key=Environment,Value=Production
```

### Launching an EC2 Instance
To launch an EC2 instance with a specified AMI and instance type:
```bash
aws ec2 run-instances --image-id ami-12345678 --instance-type t2.micro --key-name MyKeyPair
```
### Stopping and Starting EC2 Instances
To stop or start an EC2 instance:
```bash
aws ec2 stop-instances --instance-ids i-12345678
aws ec2 start-instances --instance-ids i-12345678
```
### Viewing EC2 Instance Status
To view the status of EC2 instances:
```bash
aws ec2 describe-instance-status --instance-ids i-12345678
```
### Listing S3 Buckets
To list all S3 buckets:
```bash
aws s3 ls
```
### Creating an S3 Bucket
To create a new S3 bucket:
```bash
aws s3 mb s3://my-new-bucket
```
### Uploading Files to S3
To upload files to an S3 bucket:
```bash
aws s3 cp myfile.txt s3://my-bucket-name/
```
### Downloading Files from S3
To download files from an S3 bucket:
```bash
aws s3 cp s3://my-bucket-name/myfile.txt .
```
### Removing Files from S3
To remove files from an S3 bucket:
```bash
aws s3 rm s3://my-bucket-name/myfile.txt
```
### Listing IAM Users
To list IAM users:
```bash
aws iam list-users
```
### Creating IAM Users
To create a new IAM user:
```bash
aws iam create-user --user-name newUser
```
### Adding IAM User to a Group
To add an IAM user to a group:
```bash
aws iam add-user-to-group --user-name newUser --group-name Admins
```
### Removing IAM User from a Group
To remove an IAM user from a group:
```bash
aws iam remove-user-from-group --user-name newUser --group-name Admins
```
### Deleting IAM Users
To delete an IAM user:
```bash
aws iam delete-user --user-name newUser
```
### Creating a CloudFormation Stack
To create a CloudFormation stack:
```bash
aws cloudformation create-stack --stack-name my-stack --template-body file://template.json
```
### Updating a CloudFormation Stack
To update a CloudFormation stack:
```bash
aws cloudformation update-stack --stack-name my-stack --template-body file://template.json
```
### Deleting a CloudFormation Stack
To delete a CloudFormation stack:
```bash
aws cloudformation delete-stack --stack-name my-stack
```
### Listing Lambda Functions
To list all Lambda functions:
```bash
aws lambda list-functions
```
### Creating a Lambda Function
To create a new Lambda function:
```bash
aws lambda create-function --function-name my-function --runtime nodejs14.x --role arn:aws:iam::123456789012:role/service-role/my-role --handler index.handler --zip-file fileb://function.zip
```
### Invoking a Lambda Function
To invoke a Lambda function:
```bash
aws lambda invoke --function-name my-function output.txt
```
### Deleting a Lambda Function
To delete a Lambda function:
```bash
aws lambda delete-function --function-name my-function
```
### Setting a Specific Region
You can specify a region for each command using the `--region` flag:
```bash
aws s3 ls --region us-west-2
```
### Using Multiple Profiles
If you have multiple AWS CLI profiles, you can specify the profile with the `--profile` flag:
```bash
aws s3 ls --profile my-other-profile
```














---

In summary, mastering the AWS CLI involves understanding how to interact with different services, using advanced command options, automating tasks, and troubleshooting errors efficiently. The more you use it, the more comfortable you’ll get with managing your AWS resources via the command line.
