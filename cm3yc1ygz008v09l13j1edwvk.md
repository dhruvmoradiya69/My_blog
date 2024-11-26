---
title: "Day 52: Your CI/CD Pipeline on AWS - Part 3 🚀☁"
datePublished: Tue Nov 26 2024 10:47:33 GMT+0000 (Coordinated Universal Time)
cuid: cm3yc1ygz008v09l13j1edwvk
slug: day-52-your-cicd-pipeline-on-aws-part-3
tags: 90daysofdevops, tws, devops-aws-codedeploy-cicd-continuouslearning-cloudcomputing-learningbydoing

---

Welcome to Part 3 of your CI/CD pipeline journey on AWS! So far, you’ve explored **CodeCommit** for version control and **CodeBuild** for automating builds. Today, we dive into **AWS CodeDeploy**, the tool that ensures smooth, automated application deployments across various environments. Let’s get started!

---

## What is AWS CodeDeploy?

**AWS CodeDeploy** automates application deployments to:

* **Amazon EC2 instances**
    
* **On-premises servers**
    
* **Serverless Lambda functions**
    
* **Amazon ECS services**
    

It supports deploying code stored in:

* **Amazon S3 buckets**
    
* **CodeCommit repositories**
    
* **Third-party repositories** (e.g., GitHub, Bitbucket)
    

With CodeDeploy, you don’t need to modify your existing code. It’s designed to handle deployments reliably with rollback and tracking capabilities.

---

## Tasks for Today

### **Task 01: Learn About** `appspec.yml` and Deploy to EC2

#### Requirements:

* An **Amazon EC2 instance** with Nginx installed.
    
* A CodeDeploy **IAM role** with permissions to deploy applications.
    
* CodeDeploy **agent installed** on the EC2 instance.
    

#### Steps:

1. **Understand the** `appspec.yml` File:
    
    * This file defines how AWS CodeDeploy should deploy your application.
        
    * Key sections:
        
        * **Resources**: Files and scripts to deploy.
            
        * **Hooks**: Commands to execute at specific deployment stages (e.g., BeforeInstall, AfterInstall).
            
    * Example `appspec.yml`:
        
        ```yaml
        version: 0.0
        os: linux
        files:
          - source: /
            destination: /usr/share/nginx/html
        hooks:
          AfterInstall:
            - location: scripts/restart-nginx.sh
              timeout: 300
              runas: root
        ```
        
2. **Set Up CodeDeploy Agent on EC2**:
    
    * SSH into your EC2 instance:
        
        ```bash
        ssh -i your-key.pem ec2-user@your-ec2-public-ip
        ```
        
    * Install the CodeDeploy agent:
        
        ```bash
        sudo apt-get update -y
        sudo apt-get install -y ruby wget
        cd /home/ec2-user
        wget https://aws-codedeploy-us-east-1.s3.amazonaws.com/latest/install
        sudo chmod +x ./install
        sudo ./install auto
        sudo service codedeploy-agent start
        ```
        
    * Verify the agent is running:
        
        ```bash
        sudo service codedeploy-agent status
        ```
        
3. **Deploy** `index.html` with Nginx:
    
    * Ensure your EC2 instance is ready to serve files using Nginx.
        

---

### **Task 02: Add** `appspec.yml` and Deploy Application

#### Steps:

1. **Create the** `appspec.yml` File:
    
    * Add an `appspec.yml` file to your CodeCommit repository:
        
        ```yaml
        version: 0.0
        os: linux
        files:
          - source: /
            destination: /usr/share/nginx/html
        hooks:
          AfterInstall:
            - location: scripts/restart-nginx.sh
              timeout: 300
              runas: root
        ```
        
2. **Add a Restart Script**:
    
    * Create a script to restart Nginx and add it to the repository (`scripts/`[`restart-nginx.sh`](http://restart-nginx.sh)):
        
        ```bash
        #!/bin/bash
        sudo systemctl restart nginx
        ```
        
3. **Push Changes to CodeCommit**:
    
    ```bash
    git add appspec.yml scripts/restart-nginx.sh
    git commit -m "Added appspec.yml and restart script"
    git push origin main
    ```
    
4. **Create a Deployment Group in CodeDeploy**:
    
    * Go to **AWS CodeDeploy** in the AWS Management Console.
        
    * Create an **Application** and a **Deployment Group**.
        
    * Select your EC2 instance and associate it with the deployment group.
        
5. **Run the Deployment**:
    
    * Start a deployment using the CodeCommit repository and `appspec.yml`.
        
    * Monitor the deployment in the CodeDeploy console.
        

---

### Key Takeaways

* **CodeDeploy** simplifies deploying applications to various environments with zero manual effort.
    
* The `appspec.yml` file is crucial for defining deployment steps and hooks.
    
* Installing the CodeDeploy agent on EC2 is necessary for deployments.
    

---

Stay tuned for **Part 4**, where we’ll bring everything together with **AWS CodePipeline**!