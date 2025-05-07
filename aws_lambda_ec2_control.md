
# AWS Lambda: Start and Stop EC2 Instances with Node.js

## 🚀 Goal
Create:
- A Lambda function that **starts** an EC2 instance.
- A Lambda function that **stops** an EC2 instance.
- Both exposed via an HTTP endpoint.

## 🧰 What you'll need:
- An **Amazon AWS account** (you already have it ✅)
- No prior setup required

## ✅ Step-by-step

### 1. **Log into AWS Console**
- Go to [https://console.aws.amazon.com](https://console.aws.amazon.com)
- Choose your region (e.g., `us-east-1`)

### 2. **Create an EC2 Instance (for testing)**
- [ ] 1. Go to **EC2 → Instances → Launch Instance**
- [ ] 2. Choose **Amazon Linux 2023**
- [ ] 3. Pick `t2.micro` (Free tier)
- [ ] 4. Leave defaults and launch it
- [ ] 5. After it's running, note the **Instance ID** (e.g., `i-1234abcd5678efgh`)

### 3. **Create IAM Role for Lambda**
- [ ] 1. Go to **IAM → Roles → Create role**
- [ ] 2. Choose **Trusted entity: AWS Service**, use case: **Lambda**
- [ ] 3. Click **Next**, then **Add permissions**
- [ ] 4. Attach:
  - `AmazonEC2FullAccess` (for demo)
- [ ] 5. Name it `LambdaEC2ControlRole`
- [ ] 6. Create role

### 4. **Create a Lambda Function (Start EC2)**
- [ ] 1. Go to **Lambda → Create function**
- [ ] 2. Name it: `startEC2`
- [ ] 3. Runtime: `Node.js 20.x`
- [ ] 4. Choose **Use an existing role** → Select `LambdaEC2ControlRole`
- [ ] 5. Click **Create Function**

- [ ] 6. Replace the default code with:
```js
const AWS = require('aws-sdk');
const ec2 = new AWS.EC2({ region: 'us-east-1' }); // change region if needed

exports.handler = async (event) => {
  const instanceId = 'i-1234abcd5678efgh'; // replace with your real instance ID

  try {
    await ec2.startInstances({ InstanceIds: [instanceId] }).promise();
    return {
      statusCode: 200,
      body: JSON.stringify({ message: `EC2 ${instanceId} starting...` }),
    };
  } catch (err) {
    return {
      statusCode: 500,
      body: JSON.stringify({ error: err.message }),
    };
  }
};
```

- [ ] 7. Click **Deploy**

### 5. **Create Another Function (Stop EC2)**
- [ ] Repeat step 4 but name the function `stopEC2` and use this code:

```js
const AWS = require('aws-sdk');
const ec2 = new AWS.EC2({ region: 'us-east-1' });

exports.handler = async (event) => {
  const instanceId = 'i-1234abcd5678efgh'; // same instance

  try {
    await ec2.stopInstances({ InstanceIds: [instanceId] }).promise();
    return {
      statusCode: 200,
      body: JSON.stringify({ message: `EC2 ${instanceId} stopping...` }),
    };
  } catch (err) {
    return {
      statusCode: 500,
      body: JSON.stringify({ error: err.message }),
    };
  }
};
```

### 6. **Expose via API Gateway**
- [ ] 1. In the Lambda function → Click **Add trigger**
- [ ] 2. Select **API Gateway**
- [ ] 3. Choose **HTTP API**
- [ ] 4. Create a new one (name it something like `ec2-control-api`)
- [ ] 5. Leave auth as "Open" (for now), click **Add**

Now you'll get a **public URL** you can use to trigger your Lambda from a browser or Postman.

Repeat for the `stopEC2` function as well (can use same API or separate one).

## ✅ Done!

- Now you can visit the **GET URL** to start/stop your EC2.
- You can later add security (API Key, IAM, Cognito, etc.)
