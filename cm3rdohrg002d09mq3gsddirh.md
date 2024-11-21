---
title: "Day 47: Exploring AWS Elastic Beanstalk and EC2 Tasks"
datePublished: Thu Nov 21 2024 13:58:41 GMT+0000 (Coordinated Universal Time)
cuid: cm3rdohrg002d09mq3gsddirh
slug: day-47-exploring-aws-elastic-beanstalk-and-ec2-tasks
tags: aws, devops, 90daysofdevops, aws-elastic-beanstalk, tws, 2048-game

---

Today, we dive into **AWS Elastic Beanstalk**, a powerful platform for deploying and scaling web applications. Additionally, we’ll walk through deploying a web game, **2048**, on Elastic Beanstalk and testing our knowledge with hands-on tasks involving AWS services like **EC2**, **Auto Scaling**, and **CloudWatch**.

---

## What is AWS Elastic Beanstalk? 🌱

**AWS Elastic Beanstalk** is a service that simplifies the deployment and scaling of web applications. Designed for developers, it supports multiple programming languages and runtime environments like:

* Java
    
* .NET
    
* PHP
    
* Node.js
    
* Python
    
* Ruby
    
* Go
    
* Docker
    

### Why AWS Elastic Beanstalk? 🤔

Before Elastic Beanstalk, developers struggled to share software modules across geographically distributed teams. Elastic Beanstalk solves this problem by providing a platform to easily share and deploy applications across devices.

### Advantages of AWS Elastic Beanstalk ✅

* **Highly Scalable**: Automatically handles scaling to meet traffic demands.
    
* **Fast and Simple**: Easy to begin with minimal configuration.
    
* **Quick Deployment**: Allows rapid deployment of applications.
    
* **Supports Multi-Tenant Architecture**: Suitable for diverse users and teams.
    
* **Simplifies Operations**: Manages infrastructure tasks like provisioning and monitoring.
    
* **Cost-Efficient**: Pay only for the AWS resources you use.
    

---

## Components of AWS Elastic Beanstalk 🧩

1. **Application Version**: A specific iteration or release of an application’s codebase.
    
2. **Environment Tier**: Infrastructure type (e.g., web server or worker environment).
    
3. **Environment**: Collection of AWS resources running an application version.
    
4. **Configuration Template**: Defines environment settings like instance types and scaling options.
    

---

### Elastic Beanstalk Environments 🌐

* **Web Server Environments**:  
    Front-end facing, accessible via URL by clients.
    
* **Worker Environments**:  
    Backend applications or microservices, often processing tasks asynchronously.
    

---

## Task 1: Deploying the 2048 Game on AWS Elastic Beanstalk 🎮

Let’s deploy a simple web-based game, **2048**, using Elastic Beanstalk.

### Steps:

1. **Prepare the Game Application**:
    
    * Download the 2048 game source code from [`GitHub`](https://github.com/Simbaa815/2048-game).
        
    * Ensure the codebase is zipped for deployment.
        
2. **Log in to AWS Management Console**:
    
    * Navigate to **AWS Elastic Beanstalk**.
        
3. **Create a New Application**:
    
    * Click **Create Application**.
        
    * Provide a name, like "2048 Game".
        
4. **Choose a Platform**:
    
    * Select the runtime environment that matches your game (e.g., Node.js, Python).
        
5. **Upload the Source Code**:
    
    * Upload the zipped game file.
        
6. **Deploy the Application**:
    
    * Click **Deploy** and wait for Elastic Beanstalk to set up resources.
        
7. **Test the Game**:
    
    * Open the provided URL to ensure the game is running.
        

---

## Additional Work: AWS Knowledge Tasks 💻 📈

As part of the **90 Days of DevOps Challenge**, test your understanding of AWS services with the following hands-on tasks.

### **Task 1: Launch an EC2 Instance and Deploy a Web Application**

#### Steps:

1. **Launch an EC2 Instance**:
    
    * Log in to the **AWS Management Console**.
        
    * Navigate to **EC2** and launch an instance.
        
    * Choose an Amazon Linux AMI.
        
2. **Connect Using SSH**:
    
    * Use your terminal or command prompt:
        
        ```bash
        ssh -i "your-key.pem" ec2-user@your-ec2-public-ip  
        ```
        
3. **Install a Web Server**:
    
    * Update the instance:
        
        ```bash
        sudo apt-get update -y  
        ```
        
    * Install Apache:
        
        ```bash
        sudo apt-get install nginx -y  
        sudo systemctl start nginx  
        sudo systemctl enable nginx  
        ```
        
4. **Deploy a Simple Web Application**:
    
    * Upload your HTML files to `/var/www/html`.
        
5. **Monitor with CloudWatch**:
    
    * Set up CloudWatch to monitor CPU utilization and resolve issues.
        

---

### **Task 2: Configure Auto Scaling with AWS**

#### Steps:

1. **Create an Auto Scaling Group**:
    
    * In the **AWS Management Console**, navigate to **Auto Scaling**.
        
    * Define scaling policies based on CPU usage or network traffic.
        
2. **Monitor with CloudWatch**:
    
    * Set CloudWatch alarms to track performance metrics.
        
3. **Verify with AWS CLI**:
    
    * Use the CLI to ensure correct scaling:
        
        ```bash
        aws autoscaling describe-auto-scaling-groups  
        ```
        
    * Verify instances:
        
        ```bash
        aws ec2 describe-instances  
        ```
        

---

## Key Takeaways ✨

* **AWS Elastic Beanstalk** simplifies application deployment and scaling with minimal effort.
    
* **EC2 Instances** are flexible compute resources for hosting applications and testing configurations.
    
* **CloudWatch** and **Auto Scaling** ensure applications remain resilient and cost-efficient under variable workloads.