---
title: "Day 42: IAM Programmatic Access and AWS CLI - A Step-by-Step Guide 🚀 ☁"
seoDescription: "Learn how to set up IAM Programmatic Access and install AWS CLI to automate tasks on AWS. A step-by-step guide for beginners to securely access AWS services"
datePublished: Sat Nov 16 2024 11:57:42 GMT+0000 (Coordinated Universal Time)
cuid: cm3k45n4m000i08mha0akgwq8
slug: day-42-iam-programmatic-access-and-aws-cli-a-step-by-step-guide
tags: devops, 90daysofdevops, tws, aws-cli-iam-programmatic-access-aws-access-key-aws-secret-access-key-automating-aws-aws-tutorial-aws-cli-installation

---

In this guide, we'll dive into IAM Programmatic Access and how to set up the AWS CLI (Command Line Interface) to access and manage your AWS services more efficiently. These tasks are essential for automating processes, managing resources via scripts, and accessing your AWS environment programmatically. Let’s break it down step by step!

---

## **What is IAM Programmatic Access?**

IAM (Identity and Access Management) programmatic access allows you to interact with AWS services from the terminal or other systems using **AWS Access Keys** and **AWS Secret Access Keys**. These credentials are necessary for applications and scripts to securely access AWS resources without needing to manually log in each time.

### **AWS Access Keys and Secret Keys**

* **AWS Access Key ID:** Acts as the username.
    
* **AWS Secret Access Key:** Acts as the password.
    

These keys must be handled with care, as they provide access to your AWS resources. For more detailed steps on how to generate these keys, you can watch this [video tutorial](#).

---

## **What is AWS CLI?**

The **AWS Command Line Interface (CLI)** is a unified tool that enables you to manage AWS services from the command line. By using just one tool, you can control multiple AWS services and automate tasks through scripts. AWS CLI v2 brings enhanced features such as improved installers and new configuration options like **AWS IAM Identity Center** (successor to AWS SSO).

With AWS CLI, you can:

* Manage your AWS services without logging into the AWS Management Console.
    
* Automate common tasks using scripts.
    
* Access services and resources programmatically.
    

---

## **Task 1: Create AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY from AWS Console**

### **Step-by-Step Guide**

1. **Log in to your AWS Console.**
    
    * Go to the AWS Management Console.
        
    * Enter your credentials and access the dashboard.
        
2. **Navigate to IAM (Identity and Access Management):**
    
    * In the search bar, type "IAM" and click on it to open the IAM dashboard.
        
3. **Create a New User:**
    
    * In the IAM dashboard, select **Users** from the left-hand menu.
        
    * Click the **Add user** button.
        
    * Choose **Programmatic access** under **Access type**.
        
    * Set a username and proceed to the next step.
        
4. **Attach Permissions:**
    
    * Choose the necessary permissions for your new user. For example, you can select **AdministratorAccess** or customize permissions based on your use case.
        
5. **Review and Create:**
    
    * Review the user configuration and click **Create user**.
        
    * Once the user is created, you'll see the **Access Key ID** and **Secret Access Key**. Make sure to **download** or **copy** these keys and store them securely. You will need them to set up the AWS CLI.
        

---

## **Task 2: Install AWS CLI and Configure Your Account Credentials**

Now that you have your access keys, it’s time to install the AWS CLI and configure it with your account credentials.

### **Step-by-Step Guide to Set Up AWS CLI**

1. **Install AWS CLI:**
    
    * **Windows:**
        
        * Download the **AWS CLI MSI installer** from the [AWS website](https://aws.amazon.com/cli/).
            
        * Run the installer and follow the prompts.
            
    * **macOS:**
        
        * Use **Homebrew** to install AWS CLI:
            
            ```bash
            brew install awscli
            ```
            
    * **Linux:**
        
        * Use the following command to install AWS CLI v2:
            
            ```bash
            curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
            unzip awscliv2.zip
            sudo ./aws/install
            ```
            
2. **Verify AWS CLI Installation:**
    
    * Run the following command to confirm that AWS CLI is installed correctly:
        
        ```json
        aws --version
        ```
        
3. **Configure AWS CLI with Your Credentials:**
    
    * Open your terminal and run:
        
        ```bash
        aws configure
        ```
        
    * Enter the following details when prompted:
        
        * **AWS Access Key ID**: Your AWS Access Key ID (created in Task 1).
            
        * **AWS Secret Access Key**: Your AWS Secret Access Key.
            
        * **Default region name**: Choose your preferred AWS region (e.g., `us-east-1`).
            
        * **Default output format**: Choose your preferred output format (e.g., `json`).
            
4. **Test Your Configuration:**
    
    * Run a simple AWS CLI command to test if everything is set up correctly. For example:
        
        ```bash
        aws s3 ls
        ```
        
    * This will list all S3 buckets in your account, confirming that your configuration works properly.
        

---

## **Conclusion**

By completing these tasks, you’ve successfully set up **IAM programmatic access** and installed the **AWS CLI** to manage your AWS resources programmatically. With these tools in place, you can start automating tasks, managing services, and building scripts to streamline your workflow.