# Day 7 Practice – Lambda + S3 Trigger

## 🚀 Goal
Create a Lambda function that automatically runs when a file is uploaded to an S3 bucket and logs output to CloudWatch.


## ✅ Step-by-step

### 1. **Create S3 Bucket**
- [ ] Go to **S3 → Create bucket**
- [ ] Name it (e.g., `lambda-trigger-bucket`)
- [ ] Region: Choose your preferred region
- [ ] Uncheck **Block all public access** (optional)
- [ ] Create bucket

---

### 2. **Create Lambda Function**
- [ ] Go to **Lambda → Create function**
- [ ] Name it (e.g., `s3FileLogger`)
- [ ] Runtime: `Node.js 20.x`
- [ ] Choose **Create new role with basic Lambda permissions**
- [ ] Click **Create function**

- [ ] In the code editor, replace default code with:

```js
exports.handler = async (event) => {
  console.log("New S3 event:", JSON.stringify(event, null, 2));
  return {
    statusCode: 200,
    body: "Success",
  };
};
```

- [ ] Click **Deploy**

---

### 3. **Add S3 Trigger**
- [ ] In your Lambda function, go to **Add Trigger**
- [ ] Select **S3**
- [ ] Bucket: select the one you just created
- [ ] Event type: **PUT** (for new uploads)
- [ ] Click **Add**

---

### 4. **Test the Trigger**
- [ ] Upload a file to your S3 bucket
- [ ] Go to **CloudWatch → Logs → Log groups**
- [ ] Open your function’s log group
- [ ] You should see a new log with the file upload event

---

## ✅ Done!
You've created a serverless automation that reacts to S3 file uploads and logs activity to CloudWatch. 🎉
