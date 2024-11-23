---
title: "Day 49 - Interview Questions on AWS"
datePublished: Sat Nov 23 2024 11:50:24 GMT+0000 (Coordinated Universal Time)
cuid: cm3u3z85t000c08mhbunthiyp
slug: day-49-interview-questions-on-aws
tags: lambda, ec2, aws, devops, rds, s3, aws-interview-question-and-answers, 90daysofdevops, tws

---

Hey everyone! 👋  
We’ve heard your feedback and are excited to include **interview-based questions** as part of our daily tasks. Here's a curated list of AWS interview questions to sharpen your skills. Let’s dive in! 🚀

---

## **INTERVIEW QUESTIONS**

### 1\. **Name 5 AWS services you have used and their use cases**

* **Amazon EC2**: For hosting virtual servers to run applications.
    
* **Amazon S3**: For scalable object storage and static website hosting.
    
* **AWS Lambda**: For running serverless applications without managing servers.
    
* **Amazon RDS**: For managing relational databases like MySQL/PostgreSQL.
    
* **AWS CloudFront**: For speeding up content delivery through a CDN.
    

---

### 2\. **What are the tools used to send logs to the cloud environment?**

* **AWS CloudWatch**: Monitors and stores logs for analysis.
    
* **AWS Kinesis**: Streams real-time logs and event data.
    
* **Fluentd**: Open-source tool for collecting, processing, and transporting logs.
    
* **Logstash**: For log ingestion and processing before sending to AWS services.
    

---

### 3\. **What are IAM Roles? How do you create/manage them?**

* **Definition**: IAM Roles provide temporary access permissions to AWS services.
    
* **How to Create**:
    
    1. Go to **IAM Console** → **Roles**.
        
    2. Choose a **trusted entity** (e.g., AWS service).
        
    3. Attach a **policy** defining permissions.
        
* **Management**: Regularly review attached policies and rotate credentials.
    

---

### 4\. **How to upgrade or downgrade a system with zero downtime?**

* **Steps**:
    
    1. Use **Auto Scaling Groups** for horizontal scaling.
        
    2. Leverage a **blue/green deployment strategy**.
        
    3. Configure **Load Balancers** to route traffic between environments.
        

---

### 5\. **What is Infrastructure as Code (IaC), and how do you use it?**

* **Definition**: IaC automates infrastructure setup using code (e.g., YAML, JSON).
    
* **Tools**:
    
    * **AWS CloudFormation**: For creating and managing AWS resources.
        
    * **Terraform**: For multi-cloud IaC automation.
        

---

### 6\. **What is a Load Balancer? Give scenarios of each kind.**

* **Definition**: Distributes traffic evenly to multiple instances.
    
* **Types**:
    
    * **Application Load Balancer**: For HTTP/HTTPS traffic (e.g., web apps).
        
    * **Network Load Balancer**: For TCP/UDP traffic (e.g., real-time gaming).
        
    * **Classic Load Balancer**: Legacy option for basic load balancing.
        

---

### 7\. **What is AWS CloudFormation, and why is it used?**

* **Definition**: Automates the provisioning of AWS resources using templates.
    
* **Why Use It?**:
    
    * Simplifies infrastructure management.
        
    * Ensures repeatability and consistency across deployments.
        

---

### 8\. **Difference between AWS CloudFormation and AWS Elastic Beanstalk**

| Feature | **AWS CloudFormation** | **AWS Elastic Beanstalk** |
| --- | --- | --- |
| **Purpose** | Automates resource provisioning. | Manages application deployments. |
| **Control** | Full control of resources. | Limited control with managed service. |
| **Use Case** | Infrastructure management. | Deploying apps quickly. |

---

### 9\. **What are the kinds of security attacks that can occur on the cloud? How can we minimize them?**

* **Attacks**:
    
    * DDoS Attacks
        
    * Data Breaches
        
    * Malware Injections
        
    * Man-in-the-Middle (MITM) Attacks
        
* **Minimization Strategies**:
    
    * Enable **AWS Shield** for DDoS protection.
        
    * Use **IAM Policies** for least privilege access.
        
    * Encrypt data with **AWS KMS**.
        
    * Regularly monitor with **AWS GuardDuty**.
        

---

### 10\. **Can we recover an EC2 instance if we have lost the key?**

* **Yes**! Steps:
    
    1. Stop the instance.
        
    2. Detach its root volume.
        
    3. Attach it to another instance.
        
    4. Add a new key to the `authorized_keys` file.
        
    5. Reattach the volume and restart the instance.
        

---

### 11\. **What is a Gateway?**

* **Definition**: Connects internal resources to external networks.
    
* **Types**:
    
    * **Internet Gateway**: For VPC internet access.
        
    * **NAT Gateway**: For outbound traffic without exposing instances.
        

---

### 12\. **What is the difference between Amazon RDS, DynamoDB, and Redshift?**

| Feature | **Amazon RDS** | **DynamoDB** | **Redshift** |
| --- | --- | --- | --- |
| **Type** | Relational Database | NoSQL Database | Data Warehouse |
| **Use Case** | Structured transactional data. | Low-latency unstructured data. | Big data analytics. |
| **Scaling** | Vertical scaling. | Horizontal scaling. | Cluster-based scaling. |

---

### 13\. **Do you prefer to host a website on S3? Why or why not?**

* **Yes**: Ideal for static websites because:
    
    * Highly scalable and cost-effective.
        
    * Built-in integration with **CloudFront** for CDN.
        
* **No**: Not suitable for dynamic content or server-side processing.
    

---

That’s it for **Day 49**! Keep practicing these questions to boost your AWS interview preparation. Have more suggestions? Let us know in the comments! 😊