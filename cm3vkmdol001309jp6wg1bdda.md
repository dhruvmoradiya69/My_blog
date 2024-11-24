---
title: "Day 50: Your CI/CD Pipeline on AWS - Part 1 🚀☁"
datePublished: Sun Nov 24 2024 12:24:05 GMT+0000 (Coordinated Universal Time)
cuid: cm3vkmdol001309jp6wg1bdda
slug: day-50-your-cicd-pipeline-on-aws-part-1
tags: devops, 90daysofdevops, tws, aws-cicd, clcd

---

Welcome to Day 50 of your DevOps journey! Over the next 4 days, you'll set up a **CI/CD pipeline on AWS** using powerful tools like **CodeCommit**, **CodeBuild**, **CodeDeploy**, **CodePipeline**, and **S3**. Let's break it down step by step, starting with **CodeCommit**.

---

## What is CodeCommit?

**AWS CodeCommit** is a fully-managed **source control service** that enables you to:

* Securely **store, manage, and version your source code**.
    
* Collaborate with your team using **branching and merging workflows**.
    
* Easily integrate with other **AWS services** for CI/CD pipelines.
    
* Get compliance and audit logs for tracking code changes.
    

With CodeCommit, you can manage your repositories efficiently and use them as the foundation for your CI/CD pipelines.

---

## Tasks for Today

### **Task 01: Set Up a Code Repository on CodeCommit and Clone It Locally**

#### Requirements:

* AWS account with **IAM user permissions** for **CodeCommit** and **GitCredentials**.
    
* **Git** installed locally.
    

#### Steps:

1. **Create a Repository on CodeCommit**:
    
    * Open the **AWS Management Console**.
        
    * Go to **CodeCommit** &gt; **Create Repository**.
        
    * Provide a name for your repository (e.g., `my-cicd-repo`) and optional description.
        
    * Click **Create Repository**.
        
2. **Set Up Git Credentials in AWS IAM**:
    
    * Open **IAM** in the AWS Console.
        
    * Go to your user profile and select **Security credentials**.
        
    * Under **HTTPS Git credentials for AWS CodeCommit**, click **Generate credentials**.
        
    * Save the credentials (username and password) securely.
        
3. **Clone the Repository Locally**:
    
    * Open a terminal and use the following command:
        
        ```bash
        git clone https://git-codecommit.<region>.amazonaws.com/v1/repos/my-cicd-repo
        ```
        
        Replace `<region>` with your AWS region (e.g., `us-east-1`).
        
    * When prompted, use the **Git credentials** from step 2.
        

---

### **Task 02: Add a New File Locally and Push Changes to CodeCommit**

#### Steps:

1. **Navigate to the Cloned Repository**:
    
    ```bash
    cd my-cicd-repo
    ```
    
2. **Add a New File Locally**:
    
    * Create a file (e.g., `hello-world.txt`) using a text editor or terminal:
        
        ```bash
        echo "Hello, CodeCommit!" > hello-world.txt
        ```
        
3. **Stage the File for Commit**:
    
    ```bash
    git add hello-world.txt
    ```
    
4. **Commit the Changes**:
    
    ```bash
    git commit -m "Added hello-world.txt"
    ```
    
5. **Push the Changes to CodeCommit**:
    
    ```bash
    git push origin main
    ```
    
    * Ensure the branch name is correct (`main` or `master`, depending on your setup).
        

---

### Key Takeaways

* **CodeCommit** acts as the foundation for your CI/CD pipeline by securely hosting your code.
    
* Setting up Git credentials is essential for integrating your local environment with AWS.
    
* With a simple `git add`, `commit`, and `push`, you can sync your local changes to CodeCommit.