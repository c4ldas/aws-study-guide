# Elastic Load Balancing (ELB)

Elastic Load Balancing automatically distributes incoming application or network traffic across multiple targets, such as EC2 instances, containers, and IP addresses, to ensure high availability and fault tolerance.

Click on each topic to go to the specific section.

<table>
  <tr>
    <th><strong>Topic</strong></th>
    <th><strong>Description</strong></th>
  </tr>
  <tr>
    <td>⚙️ <a href="#--elb-overview">1. ELB Overview</a></td>
    <td>- AWS's Elastic Load Balancing service that distributes incoming traffic across multiple targets (EC2, IP addresses, containers, etc.).</td>
  </tr>
  <tr>
    <td>⚖️ <a href="#--types-of-elb">2. Types of ELB</a></td>
    <td>- Explains the different types of load balancers in AWS: Classic Load Balancer, Application Load Balancer, and Network Load Balancer.</td>
  </tr>
  <tr>
    <td>💡 <a href="#--alb">3. Application Load Balancer (ALB)</a></td>
    <td>- A type of ELB that handles HTTP/HTTPS traffic with advanced routing capabilities.</td>
  </tr>
  <tr>
    <td>🔗 <a href="#--nlb">4. Network Load Balancer (NLB)</a></td>
    <td>- A type of ELB designed for high-performance TCP traffic.</td>
  </tr>
  <tr>
    <td>🔒 <a href="#--clb">5. Classic Load Balancer (CLB)</a></td>
    <td>- The original ELB offering for basic load balancing of HTTP/HTTPS and TCP traffic.</td>
  </tr>
  <tr>
    <td>🛠️ <a href="#--creating-and-configuring-elb">6. Creating and Configuring ELB</a></td>
    <td>- Steps to create and configure an ELB to distribute traffic to targets.</td>
  </tr>
  <tr>
    <td>🔧 <a href="#--health-checks">7. Health Checks</a></td>
    <td>- Configuring health checks to ensure healthy targets receive traffic.</td>
  </tr>
</table>

## - ELB Overview

Elastic Load Balancing (ELB) is a fully managed service that automatically distributes incoming application traffic across multiple targets (such as Amazon EC2 instances, containers, and IP addresses), ensuring that no single resource is overwhelmed.

- **What is ELB?**
  - ELB automatically adjusts to your traffic, scaling up or down based on demand.
  - ELB supports three types of load balancers: **Application Load Balancer (ALB)**, **Network Load Balancer (NLB)**, and **Classic Load Balancer (CLB)**.

### 🌐 Example Use Case:
An e-commerce website can use ELB to distribute incoming user requests across multiple EC2 instances, ensuring high availability and fault tolerance.

---

## - Types of ELB

### ⚖️ What are the Types of ELB?
AWS provides three main types of load balancers:

1. **Classic Load Balancer (CLB)**:  
   - The oldest type, used primarily for EC2-Classic instances.
   - Supports both HTTP/HTTPS and TCP traffic.
  
2. **Application Load Balancer (ALB)**:  
   - Ideal for HTTP and HTTPS traffic.
   - Works at the **Application Layer (Layer 7)**, allowing it to inspect HTTP requests and make routing decisions based on content such as URL paths, hostnames, and HTTP methods.
   - Supports **path-based routing**, **host-based routing**, and **WebSocket connections**.

3. **Network Load Balancer (NLB)**:  
   - Best suited for high-performance, low-latency network traffic.
   - Works at the **Transport Layer (Layer 4)**, optimized for TCP and UDP traffic and can handle millions of requests per second.

### ⚙️ Key Features:
- **CLB**: Basic load balancing with limited features.
- **ALB**: Advanced routing, ideal for web applications and microservices.
- **NLB**: High-performance, low-latency for network-heavy applications.

### 🌐 Example Use Case:
- **ALB**: A web application with complex routing rules might use ALB to distribute traffic based on URL paths or hostnames (e.g., `/api` to one set of instances, `/images` to another).
- **NLB**: A gaming application requiring low-latency connections can benefit from using NLB for fast and reliable communication.

---

## - Application Load Balancer (ALB)

### 💡 What is ALB?
- **ALB** is designed for HTTP and HTTPS traffic and operates at the **Application Layer (Layer 7)** of the OSI model.
- It allows advanced routing based on URL paths, hostnames, and HTTP methods.
- Ideal for microservices or containerized applications.

### ⚙️ Key Features of ALB:
- **Host-based routing**: Route traffic based on the domain name (e.g., `api.myapp.com` to one group, `www.myapp.com` to another).
- **Path-based routing**: Route traffic based on the URL path (e.g., `/images/*` routes to an image service).
- **WebSocket Support**: ALB supports WebSockets for real-time applications.
- **Health checks**: Built-in health checks for routing traffic to only healthy targets.

### 🌐 Example Use Case:
A web application with different microservices can use ALB to route traffic to different target groups, such as routing traffic from `api.myapp.com` to one set of EC2 instances and `www.myapp.com` to another.

---

## - Network Load Balancer (NLB)

### 🔗 What is NLB?
- **NLB** operates at the **Transport Layer (Layer 4)**, optimized for TCP traffic with high performance and low latency.
- Ideal for real-time applications, gaming servers, or IoT applications.

### ⚙️ Key Features of NLB:
- **TCP traffic**: Optimized for high-performance, low-latency traffic.
- **Static IP Support**: You can assign static IP addresses to your NLB.
- **High Availability**: NLB can handle unpredictable traffic while maintaining availability.

### 🌐 Example Use Case:
A gaming application requiring low-latency communication can use NLB for routing player connections.

---

## - Classic Load Balancer (CLB)

### 🔒 What is CLB?
- **CLB** is the original AWS load balancing solution for both HTTP/HTTPS and TCP traffic.
- Ideal for legacy applications that do not require advanced routing capabilities.

### ⚙️ Key Features of CLB:
- **Basic load balancing**: CLB offers basic load balancing with limited routing features.
- **Stickiness**: Supports session stickiness, directing a user's requests to the same instance.

### 🌐 Example Use Case:
A simple web application that doesn't need advanced routing or WebSocket support can use CLB for basic load balancing.

---

## - Creating and Configuring ELB

### 🛠️ How to Create and Configure ELB?
To create an Elastic Load Balancer:
1. Go to the **EC2 Dashboard** → **Load Balancers**.
2. Click on **Create Load Balancer** and choose the desired type (CLB, ALB, or NLB).
3. Configure settings like name, listeners, and availability zones.
4. Add targets (EC2 instances or IPs) to handle traffic.
5. Configure health checks and security groups.

### ⚙️ Key Features:
- **Listeners**: Define protocols and ports (e.g., HTTP on port 80).
- **Target Groups**: Groups of targets (EC2 instances, containers) that receive traffic.
- **Security Groups**: Set network access control for the load balancer.

---

## - Health Checks

### 🔧 What are Health Checks?
Health checks are used to determine if targets are healthy and capable of handling traffic. If a target fails a health check, the load balancer will stop routing traffic to it until it passes again.

### ⚙️ Key Features:
- **Protocol and Port**: Specify the protocol (HTTP, HTTPS, TCP) and port for health checks.
- **Path**: For ALB, you can specify a URL path (e.g., `/health`).
- **Thresholds**: Set the number of successful checks required for a target to be considered healthy.

### 🌐 Example Use Case:
A health check can be configured to monitor an HTTP endpoint (e.g., `/healthcheck`) on your EC2 instances to ensure they are functioning correctly.

---

In summary, **ALB** is best suited for modern web applications requiring advanced routing features. If your application requires low-latency, high-performance handling, **NLB** is the ideal choice. For legacy applications, **CLB** provides basic load balancing capabilities.
