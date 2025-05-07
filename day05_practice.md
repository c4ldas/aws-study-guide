# Day 5 Practice – Route 53 + ELB

## 🚀 Goal
Set up DNS with Route 53, host a static website, and use an Application Load Balancer (ALB) to route traffic to EC2 instances.


## ✅ Step-by-step

### 1. **Host Static Site on S3 + Route 53**

#### Create S3 Bucket
- [ ] Go to **S3 → Create bucket**
- [ ] Bucket name: Must match your domain (e.g., `yourdomain.com`)
- [ ] Uncheck "Block all public access"
- [ ] Enable static website hosting in **Properties**
- [ ] Upload your `index.html`

#### Register or Use a Domain
- [ ] Go to **Route 53 → Hosted zones**
- [ ] Create a new hosted zone if you have a domain
- [ ] If using AWS domain, Route 53 may create it automatically

#### Point Domain to S3 Website
- [ ] In Hosted Zone → Create record:
  - Type: A (alias)
  - Alias to: S3 website endpoint

- [ ] Wait for DNS propagation
- [ ] Visit your domain to see the static site

---

### 2. **Launch EC2 Instances Behind an ALB**

#### Create EC2 Instances
- [ ] Launch 2+ EC2 instances (Amazon Linux)
- [ ] Install and serve a basic web page on port 80
- [ ] Example:
  - sudo yum install -y httpd
  - echo "Hello from EC2-1" > /var/www/html/index.html
  - sudo systemctl start httpd

#### Create Security Group
- [ ] Allow HTTP (port 80) from anywhere
- [ ] Assign to your EC2 instances

#### Create Target Group
- [ ] Go to **EC2 → Target Groups → Create target group**
- [ ] Type: Instances
- [ ] Protocol: HTTP, Port: 80
- [ ] Register your EC2 instances

#### Create ALB
- [ ] Go to **EC2 → Load Balancers → Create Load Balancer**
- [ ] Choose **Application Load Balancer**
- [ ] Name it, set scheme to internet-facing
- [ ] Listener: HTTP 80
- [ ] Attach your public subnets
- [ ] Assign a new or existing security group
- [ ] Register your target group

#### Test the Load Balancer
- [ ] Get the ALB DNS name
- [ ] Open it in a browser → You should see responses from EC2-1 and EC2-2 (round-robin)

---

### 3. **Optional: Point Domain to ALB**
- [ ] In Route 53 → Create A record:
  - Alias: Yes
  - Target: Your ALB DNS

---

## ✅ Done!
You’ve now hosted a static site via S3 + Route 53 and deployed an EC2 app behind an ALB for high availability.
