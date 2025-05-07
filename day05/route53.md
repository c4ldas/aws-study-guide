# 🧭 Route 53 – Hosted Zones, A Records, CNAME Records

Click on each topic to go to the specific section.

<table>
  <tr>
    <th><strong>Topic</strong></th>
    <th><strong>Description</strong></th>
  </tr>
  <tr>
    <td>🌐 <a href="#--hosted-zones">1. Hosted Zones</a></td>
    <td>
      <p>- A container for DNS records for a domain.</p>
      <p>- Public or private scope depending on your use case.</p>
    </td>
  </tr>
  <tr>
    <td>📍 <a href="#--a-records">2. A Records</a></td>
    <td>
      <p>- Maps a domain name to an IPv4 address.</p>
      <p>- Most common DNS record type for websites.</p>
    </td>
  </tr>
  <tr>
    <td>🔗 <a href="#--cname-records">3. CNAME Records</a></td>
    <td>
      <p>- Maps one domain name (alias) to another domain.</p>
      <p>- Useful for subdomains and third-party services.</p>
    </td>
  </tr>
  <tr>
    <td>🌐 <a href="#--s3-website-hosting-route-53-integration">4. S3 Website Hosting + Route 53</a></td>
    <td>
      <p>- Set up an S3 bucket as a static website and use Route 53 to route traffic to it.</p>
      <p>- Supports custom domain names for static website hosting.</p>
    </td>
  </tr>
  <tr>
    <td>📧 <a href="#--mx-txt-records-for-email">5. MX/TXT Records for Email</a></td>
    <td>
      <p>- Configure email routing for your domain using MX records.</p>
      <p>- Use TXT records for domain verification (e.g., SPF, DKIM).</p>
    </td>
  </tr>
</table>


---

## - Hosted Zones

Hosted zones in Route 53 are containers that hold DNS records for a domain.

### 🌐 What is a Hosted Zone?
- It's where Route 53 stores information about how to route traffic for a domain (like example.com).
- You create one per domain/subdomain.

### ⚙️ Key Features:
**1. Public vs Private Zones:**  
- Public zones route traffic from the internet.
- Private zones are used within a VPC only.

**2. Default Record Set:**  
Route 53 automatically creates NS and SOA records when you create a hosted zone.

**3. DNS Record Management:**  
You manage A, AAAA, MX, TXT, CNAME, etc., inside a zone.

### 🌐 Example Use Case:
- You register a domain, then create a public hosted zone to manage DNS and route `www.example.com` to your web server.

### ✅ CLI Examples:
```
aws route53 create-hosted-zone --name example.com --caller-reference 1234  
aws route53 list-hosted-zones  
aws route53 get-hosted-zone --id ZONE-ID-HERE  
```
---

## - A Records

An A (Address) record links your domain name to an IPv4 address.

### 📍 What is an A Record?
- When someone visits your domain, this record tells DNS to point them to a specific IP address.

### ⚙️ Key Features:
**1. Direct Mapping:**  
Points a domain (like `example.com`) to an IPv4 address (e.g., `203.0.113.10`).

**2. Alias to AWS Resources:**  
Can also be used to map to S3 buckets, CloudFront, or ELB using alias = true.

**3. TTL (Time to Live):**  
Controls DNS cache duration — e.g., 300 seconds.

### 🌐 Example Use Case:
- You want `example.com` to point to your EC2 instance’s public IP.

### ✅ CLI Examples:
```
aws route53 change-resource-record-sets --hosted-zone-id ZONE-ID --change-batch '  
{
  "Changes": [{
    "Action": "UPSERT",
    "ResourceRecordSet": {
      "Name": "example.com.",
      "Type": "A",
      "TTL": 300,
      "ResourceRecords": [{ "Value": "203.0.113.10" }]
    }
  }]
}'
```
---

## - CNAME Records

A CNAME (Canonical Name) record maps a domain to another domain name (not to an IP).

### 🔗 What is a CNAME Record?
- Instead of pointing to an IP, it aliases one domain to another domain.
- Often used with www, app, api, etc.

### ⚙️ Key Features:
**1. Subdomain Redirection:**  
Maps `www.example.com` ➝ `example.com` or to an external service (like a Heroku app).

**2. Cannot Be Used on Root Domains:**  
You can’t have a CNAME for `example.com`, only for subdomains (like `www.example.com`).

**3. Helpful for SaaS & CDN:**  
CDN providers often require using CNAME records.

### 🌐 Example Use Case:
- You want `www.example.com` to forward to your root domain (`example.com`), or to a third-party like GitHub Pages.

### ✅ CLI Examples:
```
aws route53 change-resource-record-sets --hosted-zone-id ZONE-ID --change-batch '  
{
  "Changes": [{
    "Action": "UPSERT",
    "ResourceRecordSet": {
      "Name": "www.example.com.",
      "Type": "CNAME",
      "TTL": 300,
      "ResourceRecords": [{ "Value": "example.com." }]
    }
  }]
}'
```
---

## - S3 Website Hosting + Route 53 Integration

You can use Route 53 to route traffic to an S3 bucket that’s configured to host a static website.

### 🌐 What is S3 Website Hosting?
- You can configure an S3 bucket to serve static website content (HTML, CSS, JS, images).
- Combine it with Route 53 to route traffic to your S3 bucket using a custom domain (like `www.example.com`).

### ⚙️ Key Features:
**1. S3 Bucket Website Configuration:**  
Set up an S3 bucket as a static website by enabling static website hosting in the S3 console and providing index and error document names.

**2. Route 53 Alias Record:**  
Create an A record with an alias to your S3 bucket’s endpoint, so Route 53 can resolve to it without needing a public IP.

**3. Redirection to S3:**  
You can configure Route 53 to redirect traffic (e.g., from `www.example.com` to `example.com`) to your S3 website.

### 🌐 Example Use Case:
- You set up an S3 bucket as a static website to serve the homepage for `www.example.com`, and Route 53 handles domain routing.

### ✅ CLI Examples:
```
aws s3 website s3://example-bucket --index-document index.html --error-document error.html  
aws route53 change-resource-record-sets --hosted-zone-id ZONE-ID --change-batch '  
{
  "Changes": [{
    "Action": "UPSERT",
    "ResourceRecordSet": {
      "Name": "www.example.com.",
      "Type": "A",
      "AliasTarget": {
        "HostedZoneId": "Z3AQBSTGFYJSTF",
        "DNSName": "example-bucket.s3-website-us-east-1.amazonaws.com.",
        "EvaluateTargetHealth": false
      }
    }
  }]
}'
```
---

## - MX/TXT Records for Email

You can configure MX (Mail Exchange) and TXT records in Route 53 to handle email services for your domain.

### 🌐 What are MX Records?
- MX records specify the mail servers responsible for receiving email on behalf of your domain.
- You need to set up MX records to receive emails at your domain (e.g., `contact@example.com`).

### ⚙️ Key Features:
**1. Email Provider Setup:**  
Most email services (like Google Workspace, Microsoft 365, etc.) provide you with the required MX records.

**2. TXT Records for Verification:**  
TXT records are often used for domain verification (e.g., SPF, DKIM) to authenticate email messages and improve security.

**3. TTL Management:**  
Set an appropriate TTL value for email records, typically 3600 seconds.

### 🌐 Example Use Case:
- You configure Route 53 to route email to Google Workspace’s mail servers by setting up the required MX records.

### ✅ CLI Examples:
```
aws route53 change-resource-record-sets --hosted-zone-id ZONE-ID --change-batch '  
{
  "Changes": [{
    "Action": "UPSERT",
    "ResourceRecordSet": {
      "Name": "example.com.",
      "Type": "MX",
      "TTL": 3600,
      "ResourceRecords": [{ "Value": "10 ASPMX.L.GOOGLE.COM." }]
    }
  }]
}'

aws route53 change-resource-record-sets --hosted-zone-id ZONE-ID --change-batch '  
{
  "Changes": [{
    "Action": "UPSERT",
    "ResourceRecordSet": {
      "Name": "example.com.",
      "Type": "TXT",
      "TTL": 3600,
      "ResourceRecords": [{ "Value": "\"v=spf1 include:_spf.google.com ~all\"" }]
    }
  }]
}'
```
