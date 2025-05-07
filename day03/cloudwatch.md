# CloudWatch: Metrics, Logs, Alarms

Click on each topic to go to the specific section.

| **Topic** | **Description** |
|----------|-----------------|
| 📊 [1. Metrics](#-cloudwatch-metrics) | Numeric time-series data from AWS services or custom sources. |
| 📝 [2. Logs](#-cloudwatch-logs) | Stores, monitors, and queries log data. |
| 🚨 [3. Alarms](#-cloudwatch-alarms) | Triggers actions based on metric thresholds. |
| 🔧 [4. Hands-On: CloudWatch with AWS CLI](#-hands-on-cloudwatch-with-aws-cli) | CLI commands to interact with CloudWatch |

---

## 📊 CloudWatch Metrics

Metrics are numerical data points over time for AWS services or custom applications.

### 💡 Key Points:
- Collected automatically for many AWS services (e.g., CPUUtilization for EC2).
- Each metric has:
  - A namespace (e.g., `AWS/EC2`).
  - Dimensions (e.g., InstanceId).
  - A timestamp and a unit (e.g., Percent).
- Custom metrics can be pushed using the AWS CLI or SDKs.

### 🌐 Example Use Case:
Monitor an EC2 instance's CPU usage and memory utilization using built-in and custom metrics.

---

## 📝 CloudWatch Logs

CloudWatch Logs stores and manages logs from AWS services and your applications.

### 💡 Key Points:
- Logs are grouped into *Log Groups*.
- Each log group contains *Log Streams* (individual sequence of events).
- Useful for:
  - Debugging apps (e.g., Lambda logs).
  - Centralized log storage.
  - Running queries with CloudWatch Logs Insights.

### 🌐 Example Use Case:
A Lambda function logs all API requests. These logs are sent to a CloudWatch Log Group for analysis and monitoring.

---

## 🚨 CloudWatch Alarms

Alarms trigger actions based on metric thresholds.

### 💡 Key Points:
- Alarms can monitor one metric or a math expression over metrics.
- States: OK, ALARM, INSUFFICIENT_DATA.
- Actions:
  - Send SNS notifications.
  - Trigger Auto Scaling policies.
  - Stop, reboot, or terminate EC2 instances.

### 🌐 Example Use Case:
You create an alarm that notifies you via email if EC2 CPU usage exceeds 80% for 5 minutes.

--

## 🔧 Hands-On: CloudWatch with AWS CLI

### 📊 Metrics

#### ✅ List available metrics:
```bash
aws cloudwatch list-metrics --namespace "AWS/EC2"
```

#### ✅ Publish a custom metric:
```bash
aws cloudwatch put-metric-data \
  --namespace "Custom/MyApp" \
  --metric-name PageLoadTime \
  --value 1.23 \
  --unit Seconds
```

### 📝 Logs
#### ✅ Create a log group:
```bash
aws logs create-log-group --log-group-name my-log-group
```

#### ✅ Create a log stream:
```bash
aws logs create-log-stream \
  --log-group-name my-log-group \
  --log-stream-name my-log-stream
```

#### ✅ Push a log event:
```bash
aws logs put-log-events \
  --log-group-name my-log-group \
  --log-stream-name my-log-stream \
  --log-events timestamp=$(date +%s%3N),message="Hello from CLI"
```

### 🚨 Alarms
#### ✅ Create an alarm for EC2 CPU Utilization > 80%:
```bash
aws cloudwatch put-metric-alarm \
  --alarm-name HighCPU \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --statistic Average \
  --period 300 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --evaluation-periods 2 \
  --alarm-actions arn:aws:sns:REGION:ACCOUNT_ID:MyTopic \
  --dimensions Name=InstanceId,Value=i-0abcdef1234567890 \
  --unit Percent
```

#### ✅ Describe alarms:
```bash
aws cloudwatch describe-alarms
```

#### ✅ Delete an alarm:
```bash
aws cloudwatch delete-alarms --alarm-names HighCPU
```

💡 Replace `REGION`, `ACCOUNT_ID`, and `i-0abcdef1234567890` with your own values.



---

In summary, CloudWatch is essential for observability in AWS. Metrics let you track performance, logs provide deep insights, and alarms help you take automated actions when something goes wrong.
