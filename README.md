# 🚀 Lift and Shift Application Workload on AWS Cloud

Welcome to the **Lift and Shift Application Workload** project! This initiative demonstrates how to seamlessly migrate a multi-tier web application stack—originally hosted on local VMs—to the **AWS Cloud** using a **Lift and Shift** (rehosting) strategy.

---

## 📌 Project Overview

This project focuses on migrating the **vProfile** application stack to the AWS Cloud for production deployment. Previously, vProfile was run in a Vagrant-managed local environment. Now, we're leveraging AWS Infrastructure-as-a-Service (IaaS) to modernize and automate its deployment.

By the end of this project, you’ll understand how to:
- Run a full application workload on AWS
- Rehost existing workloads without refactoring (Lift & Shift strategy)
- Optimize cost, scalability, and management using native AWS tools

---

## 🧰 AWS Services Used

| Service                | Purpose                                                             |
|------------------------|----------------------------------------------------------------------|
| **EC2**                | Hosts Tomcat, MySQL, RabbitMQ, and Memcached services               |
| **Elastic Load Balancer (ELB)** | Distributes incoming traffic and handles HTTPS via ACM        |
| **Auto Scaling Groups**| Manages horizontal scaling of Tomcat EC2 instances                  |
| **S3**                 | Stores application artifacts and binaries                           |
| **Route 53 (Private Hosted Zone)** | Provides internal DNS resolution for backend components   |
| **ACM**                | Manages SSL/TLS certificates for secure connections                 |
| **IAM**                | Manages identity and access control                                 |
| **EBS** / **EFS**      | Persistent storage options for EC2 instances                        |

---

## 🧱 Architecture Design

### 📡 Entry Point
- End-users access the application via a DNS entry hosted on **GoDaddy**, which points to the **Application Load Balancer (ELB)**.
- ELB routes HTTPS traffic to EC2 instances running **Apache Tomcat**.

### 🛠 Application Layer
- Tomcat servers are part of an **Auto Scaling Group** to ensure elasticity based on demand.
- These servers pull the application artifact from **S3**, and serve it to users over port 8080.

### 💾 Backend Layer
- Backend services include:
  - **MySQL**
  - **RabbitMQ**
  - **Memcached**
- These run on separate EC2 instances, referenced by hostname via **Route 53 private DNS**.

### 🔐 Security
- Security Groups are segmented by roles:
  - **ELB Security Group**: Allows HTTPS traffic only.
  - **Tomcat SG**: Allows port 8080 traffic only from ELB.
  - **Backend SG**: Allows only required ports from Tomcat SG.

---

## ⚙️ Deployment Workflow

1. **Login to AWS**
2. **Generate Key Pairs** for SSH access to instances
3. **Create Security Groups** for ELB, Tomcat, and backend servers
4. **Launch EC2 Instances** with User Data (Bash scripts)
5. **Configure Route 53** with IP-to-Hostname mapping
6. **Build Application Locally** and upload artifact to **S3**
7. **Deploy Application** from S3 to Tomcat EC2 Instances
8. **Set Up HTTPS Load Balancer** via ACM
9. **Point GoDaddy DNS** to ELB endpoint
10. **Create Auto Scaling Group** for Tomcat to enable elasticity

---

## 🌐 Benefits of AWS Migration

- **Elastic & Scalable** Infrastructure
- **Pay-as-you-go** pricing model
- **High Availability & Resilience**
- **Centralized Monitoring**
- **Infrastructure as Code** capabilities
- **Automated Deployments**

---

## 📌 Key Objectives

- Replace traditional data center complexity with AWS-native services
- Achieve infrastructure automation and cost efficiency
- Enable dynamic scaling and fault tolerance
- Simplify backend connectivity using internal DNS
- Enhance security using Security Groups and IAM

---

## 📎 Related Concepts

- Lift and Shift (Rehosting Strategy)
- EC2 Auto Scaling
- HTTPS with ACM and ELB
- S3 for artifact storage
- Route 53 Private Hosted Zones
- Application Resiliency on Cloud

---

> 💡 _This project exemplifies how to migrate legacy on-prem applications into a modern, cost-optimized, and resilient cloud-native deployment without refactoring code._

---

## 📷 Architecture Diagram

*(Insert your architectural diagram here, if available)*

---

## 📬 Contact

For questions or collaboration opportunities, feel free to connect via [LinkedIn](linkedin.com/in/etinosa-imafidon/) or email at etinosahendrix@yahoo.com.
