# Day 4 Practice – VPC + Subnets + Routing

## 🚀 Goal
Understand how to build a custom VPC, use public/private subnets, and control internet access using routing and gateways.

## ✅ Step-by-step

### 1. **Create a Custom VPC**
- [ ] Go to **VPC → Your VPCs → Create VPC**
- [ ] Name: `MyCustomVPC`
- [ ] IPv4 CIDR block: `10.0.0.0/16`
- [ ] Leave other settings as default
- [ ] Click **Create VPC**

### 2. **Create Two Subnets**
- [ ] Go to **Subnets → Create subnet**
- [ ] Choose your VPC `MyCustomVPC`
- [ ] Create a **Public Subnet**:
  - Name: `PublicSubnet`
  - CIDR: `10.0.1.0/24`
  - Availability Zone: any (e.g., `us-east-1a`)
- [ ] Create a **Private Subnet**:
  - Name: `PrivateSubnet`
  - CIDR: `10.0.2.0/24`
  - Availability Zone: same or different

### 3. **Create and Attach Internet Gateway**
- [ ] Go to **Internet Gateways → Create Internet Gateway**
- [ ] Name it: `MyIGW`
- [ ] Attach it to `MyCustomVPC`

### 4. **Update Route Table for Public Subnet**
- [ ] Go to **Route Tables → Find the one for MyCustomVPC**
- [ ] Edit Routes → Add:
  - Destination: `0.0.0.0/0`
  - Target: `Internet Gateway → MyIGW`
- [ ] Associate the route table with the **PublicSubnet**

### 5. **Launch EC2 Instances**
- [ ] Launch an EC2 (Amazon Linux) in the **PublicSubnet**
  - Ensure Auto-assign Public IP is enabled
- [ ] Launch another EC2 (Amazon Linux) in the **PrivateSubnet**
  - No public IP

### 6. **Test Internet Access**
- [ ] SSH into the **Public EC2**
- [ ] From Public EC2, try pinging an external site to test outbound internet (e.g., `ping google.com`)
- [ ] Try to SSH from Public EC2 into the Private one (if security group allows)

### 7. **Add a NAT Gateway for the Private Subnet**
- [ ] Go to **NAT Gateways → Create NAT Gateway**
- [ ] Subnet: **PublicSubnet**
- [ ] Allocate a new Elastic IP
- [ ] Create the NAT Gateway

- [ ] Go to **Route Tables → Create a new one for PrivateSubnet**
- [ ] Add route:
  - Destination: `0.0.0.0/0`
  - Target: NAT Gateway
- [ ] Associate this route table with the **PrivateSubnet**

### 8. **Test Internet from Private EC2**
- [ ] SSH into Public EC2
- [ ] From there, SSH into the Private EC2
- [ ] On Private EC2, try `ping google.com`
- [ ] It should now have outbound internet via the NAT Gateway

---

## ✅ Done!
You’ve created a full VPC network with subnets, routing, internet/NAT gateways, and verified connectivity.
