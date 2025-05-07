# EC2: Instance Types, AMIs, Key Pairs, Security Groups

Click on each topic to go to the specific section.

| **Topic** | **Description** |
|----------|-----------------|
| 🖥️ [1. EC2 Instance Types](ec2.md#--ec2-instance-types) | - Defines the hardware (vCPU, memory, storage, networking) for your EC2 virtual machine.<br>- Different instance families serve different use cases (e.g., general purpose, compute-optimized). |
| 📦 [2. AMIs](ec2.md#--amis) | - Amazon Machine Images (AMIs) are preconfigured templates used to launch EC2 instances.<br>- You can use public AMIs, AWS-provided AMIs, or create your own custom AMI. |
| 🔐 [3. Key Pairs](ec2.md#--key-pairs) | - Key pairs are used for SSH access to Linux EC2 instances (or RDP for Windows).<br>- They consist of a public key (stored in AWS) and private key (downloaded and kept safe by you). |
| 🛡️ [4. Security Groups](ec2.md#--security-groups) | - Virtual firewalls that control inbound and outbound traffic to your EC2 instances.<br>- You define rules based on ports, protocols, and IP ranges. |

---

## - EC2 Instance Types

### 🖥️ What are EC2 Instance Types?
- Define the hardware specs (CPU, RAM, network, etc.) for virtual machines on AWS.
- Choose types based on workload needs: general, compute, memory, storage, GPU, etc.

### ⚙️ Key Features:
**1. Instance Families:**
- Examples:
  - `t` = burstable (e.g., t3.micro)
  - `m` = general purpose (e.g., m5.large)
  - `c` = compute-optimized (e.g., c6g.large)
  - `r` = memory-optimized (e.g., r5.large)
  - `g/p` = GPU-accelerated (e.g., g4dn.xlarge)

**2. Lifecycle & States:**
- States: `pending`, `running`, `stopping`, `stopped`, `terminated`.
- You’re only billed for running state (mostly).

**3. Pricing Options:**
- On-Demand: pay-as-you-go
- Reserved Instances: cheaper if committed (1 or 3 years)
- Spot Instances: up to 90% off but can be interrupted
- Savings Plans: flexible commitment model

### 🌐 Example Use Case:
- Use a `t3.micro` for a dev server and `c6g.large` for CPU-heavy workloads.

---

## - AMIs

### 📦 What are AMIs?
- Templates for launching EC2 instances with a specific OS and preinstalled software.
- Includes OS, EBS snapshots, permissions, and metadata.

### ⚙️ Key Features:
**1. AMI Sources:**
- AWS-managed (e.g., Amazon Linux 2023, Ubuntu), Community AMIs, or custom AMIs.

**2. Region-Specific:**
- AMIs are regional. Copy them across regions if needed.

**3. Version Control & Maintenance:**
- It's a good idea to name/tag AMIs with versions and dates.
- Clean up old/unused AMIs and snapshots to save storage costs.

### 🌐 Example Use Case:
- Use a custom AMI to deploy a pre-configured LAMP stack across multiple instances.

---

## - Key Pairs

### 🔐 What are Key Pairs?
- Used to securely connect to your EC2 instances via SSH (Linux) or RDP (Windows).
- You need the private key (.pem file) to log in.

### ⚙️ Key Features:
**1. SSH Access:**
- Linux EC2 requires the `.pem` key to connect.

**2. Key Pair Storage:**
- Private key is downloaded once. AWS does **not** store it.
- Store it securely (e.g., encrypted in a password manager).

**3. Backup Strategy:**
- You can create a backup key pair and rotate if needed.
- Always test access before deleting or rotating the old key.

**4. Regeneration:**
- If you lose the key, you can’t SSH in.
- Workaround: create new key pair, stop instance, detach volume, attach to new instance, fix `.ssh/authorized_keys`.

### 🌐 Example Use Case:
- Create a key pair named `dev-key`, use it to SSH into development instances.

---

## - Security Groups

### 🛡️ What are Security Groups?
- Act as firewalls for EC2 instances.
- Control **inbound** and **outbound** traffic using rules.

### ⚙️ Key Features:
**1. Stateful Rules:**
- Return traffic is automatically allowed.
- If you allow inbound port 22, outbound response is auto-allowed.

**2. Rule Types:**
- Rules defined by protocol, port, and CIDR block or security group.
  - E.g., TCP port 22 from `203.0.113.5/32` (only your IP)

**3. Multiple Groups:**
- Instances can have multiple security groups for layered access control.

**4. Best Practices:**
- Principle of least privilege: open only the ports you need.
- Avoid using `0.0.0.0/0` for SSH/RDP—limit to your IP.

### 🌐 Example Use Case:
- Create a security group that only allows SSH from your IP and HTTP/HTTPS from anywhere.

---
