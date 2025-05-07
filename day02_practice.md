# Day 2 Practice - Launch EC2, SSH, and Serve a Static Site

## 🚀 Goal
- Launch an EC2 instance (Amazon Linux).
- SSH into the instance.
- Install and serve a static site using Apache or Nginx.
- Open and close ports using security groups.

## ✅ Step-by-step

### 1. **Launch EC2 (Amazon Linux)**
- [ ] 1. Go to **EC2 → Instances → Launch Instance**
- [ ] 2. Choose **Amazon Linux 2023** as the AMI.
- [ ] 3. Select **t2.micro** (Free tier eligible).
- [ ] 4. Configure the instance (you can leave most options as default).
- [ ] 5. Add storage (default settings are fine for now).
- [ ] 6. Add a **tag** (e.g., `Name: MyFirstEC2`).
- [ ] 7. Configure the **Security Group**:
  - Create a new one allowing **SSH (port 22)** from your IP (for now).
  - Allow **HTTP (port 80)** for accessing the static site later.
- [ ] 8. Review and launch the instance.
- [ ] 9. Download the **private key** (.pem) to access the instance.

### 2. **SSH Into EC2**
- [ ] 1. Open your terminal.
- [ ] 2. Use the following SSH command to connect to your EC2 instance:
```bash
ssh -i /path/to/your-key.pem ec2-user@<Your-EC2-Public-IP>
```
 - Replace /path/to/your-key.pem with the path to your private key.
 - Replace <Your-EC2-Public-IP> with your EC2 instance's public IP.
- [ ] 3. You should now be logged into the EC2 instance.

### 3. **Install Apache or Nginx**
- [ ] 1. Install Apache:
  - Run the following commands to install Apache and start the service:
    ```bash
    sudo yum update -y
    sudo yum install -y httpd
    sudo systemctl start httpd
    sudo systemctl enable httpd
    ```
  - Verify Apache is running by accessing your EC2 public IP in a browser (you should see the Apache test page).
- [ ] 2. Install Nginx:
  - Run the following commands to install Nginx and start the service:
    ```bash
    sudo amazon-linux-extras install -y nginx1
    sudo systemctl start nginx
    sudo systemctl enable nginx
    ```
  - Verify Nginx is running by accessing your EC2 public IP in a browser (you should see the Nginx welcome page).

### 4. **Serve a Static Site**
- [ ] 1. Create a simple index.html page:
  - Run the following command to create the page:
    ```bash
    sudo echo '<html><body><h1>Welcome to My Static Site!</h1></body></html>' > /var/www/html/index.html
    ```
- [ ] 2. Refresh the browser at your EC2 public IP, and you should see the static page served.

### 5. **Open/Close Ports with Security Groups**
- [ ] 1. Go to EC2 → Security Groups in the AWS Console.
- [ ] 2. Select the security group associated with your instance.
- [ ] 3. To Open Ports:
  - Click Edit inbound rules.
  - Add a rule to allow HTTP (port 80) if not already added.
- [ ] 4. To Close Ports:
  - In the same inboud rules section, remove the SSH (port 22) rule to lock down your instance from public SSH access (be cautious of this step as you may lock yourself out if you don’t have proper access methods).

## ✅ Done!
You’ve launched an EC2 instance, SSH-ed into it, served a static site, and managed security group ports.


