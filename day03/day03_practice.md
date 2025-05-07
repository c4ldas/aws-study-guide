# Day 3 Practice - S3 + CloudWatch

## 🚀 Goal
- Use S3 for object storage, backups, and data management.
- Use CloudWatch to monitor resources, logs, and set up alerts.

## ✅ Step-by-step

### 1. **Upload/Download Files via CLI (S3)**
- [ ] 1. **Configure AWS CLI**:
    - If you haven't already, configure the AWS CLI with your credentials:
    ```bash
    aws configure
    ```
    - Enter your **AWS Access Key ID**, **AWS Secret Access Key**, **Default region name**, and **Default output format**.

- [ ] 2. **Create an S3 bucket**:
    - Run the following command to create an S3 bucket (replace `<your-bucket-name>` with a unique name):
    ```bash
    aws s3 mb s3://<your-bucket-name>
    ```

- [ ] 3. **Upload a file to the S3 bucket**:
    - Upload a file to your bucket (replace `<your-file-path>` with the file you want to upload):
    ```bash
    aws s3 cp <your-file-path> s3://<your-bucket-name>/
    ```

- [ ] 4. **Download a file from the S3 bucket**:
    - Download the file you just uploaded (replace `<file-name>` with the file's name):
    ```bash
    aws s3 cp s3://<your-bucket-name>/<file-name> <download-path>
    ```

### 2. **Create CPU Alarm for EC2 (CloudWatch)**
- [ ] 1. Go to **CloudWatch → Alarms → Create Alarm**.
- [ ] 2. Choose **Select metric** and click on **EC2 → Per-Instance Metrics**.
- [ ] 3. Find your EC2 instance, and select **CPUUtilization**.
- [ ] 4. Set the **Condition** for the alarm (e.g., "Whenever CPU utilization is greater than 80% for 5 minutes").
- [ ] 5. Configure actions (e.g., send a notification to an SNS topic).
- [ ] 6. Name the alarm and click **Create alarm**.

### 3. **Explore CloudWatch Logs**
- [ ] 1. Go to **CloudWatch → Logs**.
- [ ] 2. If you have EC2 instances or Lambda functions running, explore their log groups.
    - For EC2, you might need to configure the **CloudWatch Agent** to push logs.
    - For Lambda, logs are automatically available in CloudWatch.
- [ ] 3. Check the log stream of a function or instance, and explore the logs.

---

## ✅ Done!
- You’ve uploaded and downloaded files using the AWS CLI, created a CPU alarm for EC2, and explored CloudWatch logs.
