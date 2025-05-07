# ☁️ VPC, Subnets, Routing, and Gateways

Click on each topic to go to the specific section.

<table>
  <tr>
    <th><strong>Topic</strong></th>
    <th><strong>Description</strong></th>
  </tr>
  <tr>
    <td>🌐 <a href="#--vpc">1. VPC</a></td>
    <td>
      <p>- Virtual network where you launch AWS resources.</p>
      <p>- You define IP ranges, subnets, and route rules.</p>
    </td>
  </tr>
  <tr>
    <td>📦 <a href="#--subnets">2. Subnets</a></td>
    <td>
      <p>- Public and private subdivisions within a VPC.</p>
      <p>- Control the scope of access for your resources.</p>
    </td>
  </tr>
  <tr>
    <td>🧭 <a href="#--route-tables">3. Route Tables</a></td>
    <td>
      <p>- Define how traffic is routed between subnets and outside networks.</p>
    </td>
  </tr>
  <tr>
    <td>🌍 <a href="#--internet-gateway">4. Internet Gateway (IGW)</a></td>
    <td>
      <p>- Enables internet access for resources in a public subnet.</p>
    </td>
  </tr>
  <tr>
    <td>🔁 <a href="#--nat-gateway">5. NAT Gateway</a></td>
    <td>
      <p>- Allows private subnet instances to access the internet securely.</p>
    </td>
  </tr>
</table>

---

## - VPC

A VPC (Virtual Private Cloud) is a logically isolated network within AWS where you can define your IP ranges, subnets, and gateways.

### 🌐 What is a VPC?
- A VPC lets you launch AWS resources in a private network that you define.
- You control routing, security, and connectivity to the internet or other networks.

### ⚙️ Key Features of VPC:
**1. Custom IP Ranges:**  
You define a CIDR block, like 10.0.0.0/16, giving you full control of address allocation.

**2. Isolation & Security:**  
Resources inside a VPC are isolated from the internet unless you explicitly allow access via gateways or peering.

**3. Multi-AZ Support:**  
VPCs span all Availability Zones in a region, enabling high availability designs.

**4. Multiple VPCs:**  
You can create multiple VPCs per region to separate dev, staging, and prod environments.

### 🌐 Example Use Case:
- You create a VPC with both public and private subnets to isolate a web app frontend from its backend and database.

### ✅ CLI Examples:
```
aws ec2 create-vpc --cidr-block 10.0.0.0/16  
aws ec2 describe-vpcs  
```
---

## - Subnets

Subnets are subdivisions of a VPC. They define how your instances are grouped and where they can connect.

### 📦 What are Public and Private Subnets?
- **Public Subnet**: Has a route to the internet via an Internet Gateway.
- **Private Subnet**: Has no direct route to the internet (uses NAT if needed).

### ⚙️ Key Features of Subnets:
**1. AZ Placement:**  
Each subnet exists in a single Availability Zone.

**2. Access Control:**  
You decide which subnet is public/private by how it's routed.

**3. Public IPs:**  
Instances in public subnets can get a public IP address to access the internet.

**4. Multiple Subnets per VPC:**  
You can have as many subnets as you need within your VPC's IP range.

### 🌐 Example Use Case:
- You place your web servers in public subnets, while databases stay in private subnets with no external exposure.

### ✅ CLI Examples:
```
aws ec2 create-subnet --vpc-id vpc-12345678 --cidr-block 10.0.1.0/24 --availability-zone us-east-1a  
aws ec2 modify-subnet-attribute --subnet-id subnet-12345678 --map-public-ip-on-launch  
```
---

## - Route Tables

Route Tables determine how traffic flows in/out of a subnet.

### 🧭 What are Route Tables?
- A set of rules (routes) that control where network traffic goes.
- Each subnet must be associated with one route table.

### ⚙️ Key Features of Route Tables:
**1. Main vs. Custom:**  
Every VPC has a main route table. You can create custom ones and associate them with specific subnets.

**2. Routing Control:**  
You define rules for 0.0.0.0/0 to enable external communication.

**3. One-to-Many Association:**  
One route table can be associated with multiple subnets.

### 🌐 Example Use Case:
- You create one route table for your public subnets that sends internet-bound traffic to an IGW, and another for private subnets that sends it to a NAT gateway.

### ✅ CLI Examples:
```
aws ec2 create-route-table --vpc-id vpc-12345678  
aws ec2 associate-route-table --route-table-id rtb-12345678 --subnet-id subnet-12345678  
aws ec2 create-route --route-table-id rtb-12345678 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-12345678  
```
---

## - Internet Gateway (IGW)

An Internet Gateway enables internet access for your VPC.

### 🌍 What is an IGW?
- A horizontally-scaled, redundant AWS-managed gateway that allows communication between your VPC and the internet.

### ⚙️ Key Features of IGWs:
**1. Public Connectivity:**  
Allows traffic from public subnets to access and be accessed from the internet.

**2. VPC-Level Attachment:**  
Can only be attached to one VPC at a time.

**3. Free Service:**  
There’s no cost for using an IGW (you only pay for the data transfer).

### 🌐 Example Use Case:
- You attach an IGW to your VPC and configure a route so your web servers can respond to public HTTP requests.

### ✅ CLI Examples:
```bash
aws ec2 create-internet-gateway  
aws ec2 attach-internet-gateway --internet-gateway-id igw-12345678 --vpc-id vpc-12345678
```

---

## - NAT Gateway

A NAT Gateway allows instances in private subnets to initiate internet-bound connections securely.

### 🔁 What is a NAT Gateway?
- A managed AWS service that allows outbound internet access from private subnets.
- Instances using NAT cannot receive unsolicited inbound connections.

### ⚙️ Key Features of NAT Gateways:
**1. High Availability:**  
When placed in a public subnet, it provides automatic scaling and failover.

**2. Static IP:**  
You assign an Elastic IP to the NAT Gateway.

**3. Paid Service:**  
You are billed hourly and per GB of data processed.

**4. Private-Only Outbound:**  
NAT only allows outgoing requests and responses, not inbound traffic.

### 🌐 Example Use Case:
- Your EC2 instances in a private subnet download OS updates or access the internet securely through a NAT gateway.

### ✅ CLI Examples:
```
aws ec2 allocate-address --domain vpc  
aws ec2 create-nat-gateway --subnet-id subnet-12345678 --allocation-id eipalloc-12345678  
aws ec2 create-route --route-table-id rtb-private --destination-cidr-block 0.0.0.0/0 --nat-gateway-id nat-12345678  
```
---

Understanding VPC, subnets, routing, and gateways is critical for building secure, scalable, and high-availability AWS architectures. These components form the backbone of your cloud network.
