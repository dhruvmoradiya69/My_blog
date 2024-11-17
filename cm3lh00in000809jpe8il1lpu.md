---
title: "Day 43: S3 Programmatic Access with AWS CLI 💻📁"
datePublished: Sun Nov 17 2024 10:45:00 GMT+0000 (Coordinated Universal Time)
cuid: cm3lh00in000809jpe8il1lpu
slug: day-43-s3-programmatic-access-with-aws-cli
tags: devops, 90daysofdevops, s3-cli, tws, s3-bucket, aws-s3-for-beginners

---

Hello, DevOps enthusiasts! 👋 I hope you had an amazing day yesterday. Today, as part of the #90DaysOfDevOps Challenge, we're diving into **Amazon S3**, one of the most widely used services in AWS. Let's explore its functionality and learn how to interact with it programmatically using the AWS Command Line Interface (CLI).

---

## What is Amazon S3?

**Amazon Simple Storage Service (Amazon S3)** is a highly scalable and secure object storage service designed to store virtually any type of data: text files, images, videos, backups, etc. Whether you're managing data for web applications, big data analytics, or backups, S3 is your go-to service.

➡️ [**Read more about S3 here**](https://aws.amazon.com/s3/)

---

## Tasks for Today

### **Task 1: Work with EC2 and S3 Using AWS CLI**

1. **Launch an EC2 Instance**
    
    * Use the **AWS Management Console** to launch an EC2 instance.
        
    * Connect to your instance via Secure Shell (**SSH**).
        
    * If you’re new to this, refer to AWS documentation for a step-by-step guide.
        
2. **Create an S3 Bucket**
    
    * Open the **AWS Management Console** and navigate to the S3 service.
        
    * Create a bucket with a unique name.
        
3. **Upload a File to S3**
    
    * Upload any file (e.g., `file.txt`) to the bucket using the console.
        
4. **Access the File from EC2 Using AWS CLI**
    
    * Install and configure the AWS CLI on your EC2 instance (if not already done).
        
    * Use the following commands:
        
        ```bash
        aws s3 ls                      # Lists all your S3 buckets
        aws s3 cp s3://<bucket-name>/<file-name> .  # Downloads the file to the EC2 instance
        cat <file-name>                # Displays the file content
        ```
        
    * **Read more about using AWS CLI with S3** [**here**](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3.html)
        

---

### **Task 2: Create Snapshots and Download Files**

1. **Create a Snapshot of Your EC2 Instance**
    
    * Open the **EC2 Dashboard** and create a snapshot of your instance.
        
    * Use this snapshot to launch a new EC2 instance.
        
2. **Download a File from S3**
    
    * On the new EC2 instance, configure AWS CLI if needed.
        
    * Download the file from your S3 bucket:
        
        ```bash
        aws s3 cp s3://<bucket-name>/<file-name> .
        ```
        
3. **Verify File Consistency**
    
    * Compare the contents of the downloaded file on both instances to ensure they are identical:
        
        ```bash
        diff <file-name-on-instance-1> <file-name-on-instance-2>
        ```
        

---

## Useful AWS CLI Commands for S3

Here are some handy AWS CLI commands to manage S3 buckets and objects:

* **List all S3 buckets**:
    
    ```bash
    aws s3 ls
    ```
    
* **Create a new S3 bucket**:
    
    ```bash
    aws s3 mb s3://<bucket-name>
    ```
    
* **Delete an S3 bucket**:
    
    ```bash
    aws s3 rb s3://<bucket-name>
    ```
    
* **Upload a file to S3**:
    
    ```bash
    aws s3 cp <file-name> s3://<bucket-name>
    ```
    
* **Download a file from S3**:
    
    ```bash
    aws s3 cp s3://<bucket-name>/<file-name> .
    ```
    
* **Sync a local folder with S3**:
    
    ```bash
    aws s3 sync <local-folder> s3://<bucket-name>
    ```
    
* **List objects in a bucket**:
    
    ```bash
    aws s3 ls s3://<bucket-name>
    ```
    
* **Delete an object from S3**:
    
    ```bash
    aws s3 rm s3://<bucket-name>/<file-name>
    ```
    
* **Generate a pre-signed URL** (temporary file access):
    
    ```bash
    aws s3 presign s3://<bucket-name>/<file-name>
    ```
    
* **List buckets using S3 API**:
    
    ```bash
    aws s3api list-buckets
    ```
    

---

## Conclusion

Today, you learned how to interact with **Amazon S3** programmatically using **AWS CLI** and combined it with EC2 instances to manage files effectively. S3's flexibility and CLI commands make it a vital skill for every DevOps professional.

Happy Learning! 😊