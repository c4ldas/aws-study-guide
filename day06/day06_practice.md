# Day 6 Practice – RDS (Databases)

## 🚀 Goal
Launch a managed database (MySQL/PostgreSQL) with Amazon RDS, connect to it from a client, and secure it properly.


## ✅ Step-by-step

### 1. **Launch RDS (MySQL/PostgreSQL)**

- [ ] Go to **RDS → Create database**
- [ ] Choose **Standard Create**
- [ ] Engine options: Choose **MySQL** or **PostgreSQL**
- [ ] Use **Free Tier** (e.g., `db.t3.micro`)
- [ ] Set DB instance ID, master username, and password
- [ ] Uncheck **Enable storage autoscaling** (optional)
- [ ] In **Connectivity**:
  - Choose **Default VPC** or a custom one
  - Make sure to **enable public access** for testing
- [ ] Leave default port (3306 for MySQL, 5432 for PostgreSQL)
- [ ] Create a **new security group** or use an existing one that allows inbound access from your IP on DB port

---

### 2. **Wait for DB to be Available**
- [ ] Monitor status until it's marked as **Available**
- [ ] Copy the **endpoint URL** shown in the RDS dashboard

---

### 3. **Connect via Client**

#### Using DBeaver or MySQL/PostgreSQL CLI
- [ ] Open DBeaver (or any SQL client)
- [ ] Create a new connection
  - Host: RDS endpoint
  - Port: 3306 (MySQL) / 5432 (PostgreSQL)
  - User/pass: the credentials you set earlier

- [ ] Or, via CLI:
  - MySQL:  
    `mysql -h your-endpoint.amazonaws.com -u youruser -p`
  - PostgreSQL:  
    `psql -h your-endpoint.amazonaws.com -U youruser -d postgres`

---

### 4. **Test Security Group Access**
- [ ] Try connecting with correct IP → should succeed
- [ ] Edit the security group and **block your IP**
- [ ] Try again → connection should fail

---

## ✅ Done!
You've launched a managed cloud database, connected to it, and tested network-level access using AWS security groups.
