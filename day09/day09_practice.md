# Day 9 Practice – Troubleshooting & Security

## 🔐 Goal
Understand how to troubleshoot access errors and strengthen IAM policies and security group configurations.


## ✅ Step-by-step

### 1. **Simulate "Access Denied" (S3)**

- [ ] Create an S3 bucket.
- [ ] Create an IAM user without S3 permissions.
- [ ] Log in as that user and try to list the bucket:

aws s3 ls s3://your-bucket-name

- ❌ You should get an AccessDenied error.

---

### 2. **Fix the IAM Permissions**
- [ ] Go to **IAM → Users → [your user] → Permissions**
- [ ] Attach the policy `AmazonS3ReadOnlyAccess`
- [ ] Try the `aws s3 ls` command again → it should now work ✅

---

### 3. **Simulate EC2 Security Group Block**
- [ ] Launch an EC2 instance with a security group that has **no inbound rules**
- [ ] Try SSH-ing into the instance:

ssh -i your-key.pem ec2-user@your-public-ip

- ❌ It should timeout or be refused

---

### 4. **Fix the Security Group**
- [ ] Go to **EC2 → Security Groups**
- [ ] Edit the security group to add:

Type: SSH  
Protocol: TCP  
Port: 22  
Source: Your IP (or 0.0.0.0/0 for testing)

- [ ] Retry SSH → should now connect ✅

---

### 5. **Simulate IAM Denial for RDS**
- [ ] Create an IAM user with no RDS permissions.
- [ ] Try listing RDS instances:

aws rds describe-db-instances

- ❌ Expect an `AccessDeniedException`

---

### 6. **Fix by Attaching Policy**
- [ ] Attach the policy `AmazonRDSReadOnlyAccess`
- [ ] Retry → You should now see RDS info

---

## ✅ Done!
You’ve now practiced real-world troubleshooting scenarios across IAM, S3, EC2, and RDS — key skills for support engineers.
