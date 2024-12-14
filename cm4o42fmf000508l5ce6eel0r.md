---
title: "Day 67: AWS S3 Bucket Creation and Management"
datePublished: Sat Dec 14 2024 11:45:59 GMT+0000 (Coordinated Universal Time)
cuid: cm4o42fmf000508l5ce6eel0r
slug: day-67-aws-s3-bucket-creation-and-management
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734176696769/167757df-17b4-43d3-9aae-75e8b211060e.webp
tags: aws, terraform, s3-bucket

---

Amazon Web Services (AWS) S3 (Simple Storage Service) is a fundamental cloud service for storing and retrieving any amount of data at any time. Today, we’ll focus on creating and managing an S3 bucket using **Terraform**, a popular Infrastructure-as-Code (IaC) tool. This hands-on task will walk you through key aspects such as configuring access, policies, and advanced features like versioning.

---

### **What is an S3 Bucket?**

An **S3 bucket** is essentially a container for storing data objects like files, images, or backups in the cloud. It provides durability, availability, and scalability while offering features like:

* **Data Versioning**: Helps track and restore prior versions of objects.
    
* **Access Policies**: Enables fine-grained access control.
    
* **Public Hosting**: Serves as a host for static websites.
    
* **Security**: Includes encryption and access control mechanisms.
    

---

### **Why Should You Learn S3 Bucket Management?**

AWS S3 is a cornerstone service for cloud-based solutions. Whether you're a developer, DevOps engineer, or architect, knowing how to create, configure, and manage S3 buckets is essential for:

* Automating infrastructure deployment using tools like Terraform.
    
* Managing secure storage solutions for applications.
    
* Implementing disaster recovery and compliance strategies.
    

---

### **How to Create and Manage an S3 Bucket Using Terraform**

#### **Step 1: Prerequisites**

Before you begin, ensure the following:

1. **AWS CLI Installed**: Configure it with proper credentials (`aws configure`).
    
2. **Terraform Installed**: Set up Terraform on your local machine.
    
3. **IAM Role or User**: Ensure you have permissions to create and configure S3 buckets.
    

---

#### **Step 2: Create an S3 Bucket**

1. **Define the Terraform Configuration File** Create a file named [`main.tf`](http://main.tf) and include the following configuration to create an S3 bucket.
    
    ```xml
    provider "aws" {
      region = "us-east-1" # Replace with your desired region
    }
    
    resource "aws_s3_bucket" "example_bucket" {
      bucket = "my-example-bucket-${random_id.id}" # Unique bucket name
      acl    = "public-read"
    
      tags = {
        Name        = "ExampleBucket"
        Environment = "Dev"
      }
    }
    
    resource "random_id" "id" {
      byte_length = 8
    }
    ```
    
2. **Initialize Terraform** Run the following commands:
    
    ```bash
    terraform init
    terraform apply -auto-approve
    ```
    
3. **Verify the Bucket** Check the AWS Management Console or run:
    
    ```bash
    aws s3 ls
    ```
    

---

#### **Step 3: Configure Public Read Access**

To allow public read access, add the appropriate bucket policy.

1. **Create a Bucket Policy File** Save the following JSON content in a file named `bucket-policy.json`:
    
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::my-example-bucket-*/*"
            }
        ]
    }
    ```
    
2. **Apply the Policy in Terraform** Update your [`main.tf`](http://main.tf) with:
    
    ```xml
    resource "aws_s3_bucket_policy" "example_bucket_policy" {
      bucket = aws_s3_bucket.example_bucket.id
      policy = file("bucket-policy.json")
    }
    ```
    
3. **Reapply Terraform**
    
    ```bash
    terraform apply -auto-approve
    ```
    

---

#### **Step 4: Create a Read-Only Bucket Policy for Specific IAM User or Role**

1. **Modify the Policy** Edit your `bucket-policy.json` to restrict access to a specific IAM role or user:
    
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::123456789012:user/SpecificUser" # Replace with your IAM user ARN
                },
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::my-example-bucket-*/*"
            }
        ]
    }
    ```
    
2. **Update Terraform** Reapply the updated bucket policy using:
    
    ```bash
    terraform apply -auto-approve
    ```
    

---

#### **Step 5: Enable Versioning**

Versioning in S3 allows you to preserve, retrieve, and restore every version of every object stored in a bucket.

1. **Add Versioning Block** Update the `aws_s3_bucket` resource in [`main.tf`](http://main.tf):
    
    ```xml
    resource "aws_s3_bucket_versioning" "example" {
      bucket = aws_s3_bucket.example_bucket.id
    
      versioning_configuration {
        status = "Enabled"
      }
    }
    ```
    
2. **Reapply Terraform**
    
    ```bash
    terraform apply -auto-approve
    ```
    
3. **Verify Versioning** Use the AWS CLI to confirm:
    
    ```bash
    aws s3api get-bucket-versioning --bucket my-example-bucket-${random_id.id}
    ```
    

---

### **Key Takeaways**

1. **Automation with Terraform**: Using Terraform for S3 bucket creation ensures consistency and repeatability.
    
2. **Access Control**: Balancing accessibility (public vs. private) with security policies is crucial.
    
3. **Versioning**: Enables data recovery and auditing, which are invaluable for critical operations.