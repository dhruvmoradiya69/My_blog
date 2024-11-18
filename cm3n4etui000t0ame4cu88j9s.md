---
title: "Day 44: Relational Database Service in AWS"
datePublished: Mon Nov 18 2024 14:28:09 GMT+0000 (Coordinated Universal Time)
cuid: cm3n4etui000t0ame4cu88j9s
slug: day-44-relational-database-service-in-aws
tags: aws, rdbms, aws-rds, 90daysofdevops, tws

---

Amazon Relational Database Service (Amazon RDS) simplifies setting up, operating, and scaling databases in the cloud. It automates tasks like hardware provisioning, database setup, patching, and backups. In this blog, we’ll walk through how to create and connect a **Free Tier RDS instance of MySQL** with an **EC2 instance**.

### Objectives

* Set up a MySQL database using RDS in AWS.
    
* Connect the database with an EC2 instance via a MySQL client.
    

---

### **Task 01: Create a Free Tier RDS Instance of MySQL**

#### **Steps**:

1. **Login to AWS Console**:
    
    * Navigate to the [AWS Management Console](https://aws.amazon.com/console/).
        
2. **Open RDS Service**:
    
    * Search for **RDS** in the AWS console search bar and click on it.
        
3. **Create Database**:
    
    * Click on the **"Create Database"** button.
        
    * **Select Engine Type**: Choose **MySQL**.
        
    * **Choose Edition**: Select the **Free Tier** option.
        
4. **Database Settings**:
    
    * Set a **DB Identifier** (e.g., `mydb`).
        
    * Provide a **Master Username** (e.g., `admin`).
        
    * Set a **Master Password** and confirm it.
        
5. **Instance Configuration**:
    
    * For Free Tier, choose **db.t2.micro** instance type.
        
    * Storage: Select the default **20 GB** storage.
        
6. **Network & Security**:
    
    * Place the RDS in a **VPC**.
        
    * Ensure the **Public Access** option is enabled to connect externally.
        
    * Create or use an existing security group that allows MySQL traffic (port 3306).
        
7. **Launch the Database**:
    
    * Click **Create Database** and wait for the instance to become **Available**.
        

---

### **Task 02: Create an EC2 Instance**

#### **Steps**:

1. **Open EC2 Service**:
    
    * Navigate to the EC2 dashboard from the AWS Console.
        
2. **Launch Instance**:
    
    * Click **Launch Instances**.
        
    * Select an **Amazon Linux 2 AMI** or Ubuntu as the instance type.
        
3. **Instance Settings**:
    
    * Choose the **t2.micro** instance for Free Tier eligibility.
        
    * Ensure the EC2 instance is in the same **VPC** and **Availability Zone** as the RDS instance.
        
4. **Configure Security Group**:
    
    * Allow inbound **SSH** (port 22) for your IP.
        
    * Add a rule to allow **outbound MySQL (port 3306)** for communication with RDS.
        
5. **Launch Instance**:
    
    * Create or select a key pair for secure login.
        
    * Launch the instance.
        

---

### **Task 03: Create an IAM Role with RDS Access**

#### **Steps**:

1. **Open IAM Console**:
    
    * Navigate to the **IAM** service in AWS.
        
2. **Create a Role**:
    
    * Choose **AWS Service** as the trusted entity type.
        
    * Select **EC2** as the service.
        
3. **Attach Policy**:
    
    * Attach the **AmazonRDSFullAccess** policy to grant RDS permissions.
        
4. **Name and Create**:
    
    * Name the role (e.g., `RDSAccessRole`) and create it.
        

---

### **Task 04: Assign the Role to EC2 Instance**

#### **Steps**:

1. **Go to EC2 Dashboard**:
    
    * Select the EC2 instance you created earlier.
        
2. **Attach IAM Role**:
    
    * Click **Actions** &gt; **Security** &gt; **Modify IAM Role**.
        
    * Choose the role you created (e.g., `RDSAccessRole`).
        

---

### **Task 05: Connect EC2 Instance to RDS Instance**

#### **Steps**:

1. **SSH into EC2 Instance**:
    
    * Open a terminal and connect to your EC2 instance:
        
        ```bash
        ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
        ```
        
2. **Install MySQL Client**:
    
    * For Amazon Linux:
        
        ```bash
        sudo apt-get install mysql -y
        ```
        
    * For Ubuntu:
        
        ```bash
        sudo apt update  
        sudo apt install mysql-client -y
        ```
        
3. **Connect to RDS**:
    
    * Use the credentials from the RDS console to connect:
        
        ```bash
        mysql -h <RDS-endpoint> -u <MasterUsername> -p
        ```
        
    * Replace `<RDS-endpoint>` with the endpoint URL of your RDS instance, and provide the master password when prompted.
        
4. **Verify Connection**:
    
    * Run MySQL commands to ensure the connection is successful:
        
        ```sql
        SHOW DATABASES;  
        CREATE DATABASE testdb;
        ```
        

---

### **Key Notes**

* **Security Groups**: Ensure both EC2 and RDS security groups allow traffic on port 3306.
    
* **IAM Role**: The role simplifies access management by eliminating the need to store credentials on the EC2 instance.
    
* **Free Tier Eligibility**: Both RDS and EC2 must meet Free Tier requirements to avoid charges.
    

---

### **Conclusion**

By completing this task, you’ve learned to set up a managed database with Amazon RDS and securely connect it to an EC2 instance. This foundational skill is essential for cloud-based applications, enabling robust and scalable database solutions.

---