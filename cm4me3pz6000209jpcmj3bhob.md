---
title: "Day 66 - Terraform Hands-on Project: Build Your Own AWS Infrastructure with Ease Using IaC Techniques (Interview Questions)"
datePublished: Fri Dec 13 2024 06:51:23 GMT+0000 (Coordinated Universal Time)
cuid: cm4me3pz6000209jpcmj3bhob
slug: day-66-terraform-hands-on-project-build-your-own-aws-infrastructure-with-ease-using-iac-techniques-interview-questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734072668906/b07aedcf-e304-40b1-b970-662c91aaea82.webp
tags: aws, terraform, interview-questions

---

Welcome back to Day 66 of your Terraform journey! Today, we're diving deeper into **Terraform**, one of the most popular Infrastructure as Code (IaC) tools, to build a functional AWS infrastructure. This hands-on project is not just about coding; it's also a real-world scenario designed to sharpen your skills and prepare you for interviews. Let’s break it down.

---

## **What You’ll Learn**

* How to create AWS resources like VPCs, subnets, and EC2 instances using Terraform.
    
* Using Terraform to automate infrastructure provisioning.
    
* Hands-on experience with routing, Internet Gateways, and security groups.
    
* Hosting a simple website on an EC2 instance.
    
* Preparing for interview questions related to IaC and Terraform.
    

---

## **What is Terraform?**

Terraform is an open-source tool by HashiCorp that enables DevOps engineers and cloud professionals to define and manage infrastructure as code. It simplifies the process of deploying, scaling, and maintaining infrastructure, making it repeatable and less error-prone.

---

## **How to Approach This Hands-On Project**

### **Prerequisites**

1. **AWS Account**: Ensure you have access to an AWS account with the necessary permissions.
    
2. **Terraform Installed**: Make sure you have Terraform installed on your system.
    
3. **AWS CLI Configured**: Set up your AWS CLI with access keys and a default region.
    

---

### **Step-by-Step Guide**

#### **1\. Create a VPC**

A **Virtual Private Cloud (VPC)** is the foundation of AWS networking. Here, you’ll define a VPC with a CIDR block of `10.0.0.0/16`.

**Terraform Code:**

```xml
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_support   = true
  enable_dns_hostnames = true
  tags = {
    Name = "MyVPC"
  }
}
```

---

#### **2\. Create Subnets**

* **Public Subnet**: CIDR block `10.0.1.0/24`.
    
* **Private Subnet**: CIDR block `10.0.2.0/24`.
    

**Terraform Code:**

```xml
resource "aws_subnet" "public" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.1.0/24"
  map_public_ip_on_launch = true
  tags = {
    Name = "PublicSubnet"
  }
}

resource "aws_subnet" "private" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.2.0/24"
  tags = {
    Name = "PrivateSubnet"
  }
}
```

---

#### **3\. Create and Attach an Internet Gateway**

An Internet Gateway allows communication between your VPC and the internet.

**Terraform Code:**

```xml
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id
  tags = {
    Name = "MyInternetGateway"
  }
}
```

---

#### **4\. Create a Public Route Table**

Associate the public subnet with a route to the Internet Gateway.

**Terraform Code:**

```xml
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id
  tags = {
    Name = "PublicRouteTable"
  }
}

resource "aws_route" "public_internet_access" {
  route_table_id         = aws_route_table.public.id
  destination_cidr_block = "0.0.0.0/0"
  gateway_id             = aws_internet_gateway.igw.id
}

resource "aws_route_table_association" "public_assoc" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public.id
}
```

---

#### **5\. Launch an EC2 Instance in the Public Subnet**

Define an EC2 instance with:

* **AMI**: `ami-0557a15b87f6559cf` (Amazon Linux 2).
    
* **Instance Type**: `t2.micro`.
    
* **User Data**: Install Apache and host a website.
    

**Terraform Code:**

```xml
resource "aws_security_group" "allow_ssh" {
  vpc_id = aws_vpc.main.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "AllowSSHAndHTTP"
  }
}

resource "aws_instance" "web" {
  ami           = "ami-0557a15b87f6559cf"
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.public.id
  security_groups = [aws_security_group.allow_ssh.name]

  user_data = <<-EOF
              #!/bin/bash
              yum update -y
              yum install -y httpd
              systemctl start httpd
              systemctl enable httpd
              echo "<h1>Welcome to Terraform Hosted Website!</h1>" > /var/www/html/index.html
              EOF

  tags = {
    Name = "MyWebServer"
  }
}
```

---

#### **6\. Create and Associate an Elastic IP**

Bind a static IP to the EC2 instance for consistent access.

**Terraform Code:**

```xml
resource "aws_eip" "web_ip" {
  instance = aws_instance.web.id
  tags = {
    Name = "WebServerElasticIP"
  }
}
```

---

#### **7\. Verify the Setup**

* Run the following commands to deploy:
    
    ```bash
    terraform init
    terraform apply
    ```
    
* Copy the Elastic IP and open it in a browser.
    
* Verify that the website is hosted successfully.
    

---

### **Why This Project is Important**

1. **Interview Prep**: This is a common scenario for Terraform interviews, showcasing your ability to automate AWS infrastructure provisioning.
    
2. **Real-World Skills**: You’re getting hands-on experience with AWS networking, EC2, and IaC.
    
3. **Scalability**: This setup can be expanded into more complex architectures.
    

---

### **Common Interview Questions**

* **What is Terraform, and why is it used?**
    
* **How do you manage state in Terraform?**
    
* **Explain the difference between** `terraform plan` and `terraform apply`.
    
* **How do you ensure idempotency in Terraform?**
    
* **What are Terraform modules, and how do you use them?**
    
* **How would you debug errors during Terraform deployment?**