---
title: "Day 45: Deploying a WordPress Website on AWS"
datePublished: Tue Nov 19 2024 11:56:03 GMT+0000 (Coordinated Universal Time)
cuid: cm3oef2rg000a08mf14bj4kgc
slug: day-45-deploying-a-wordpress-website-on-aws
tags: aws, wordpress, devops, 90daysofdevops, tws, deploy-wordpress-website-on-aws

---

Over 30% of websites on the internet use WordPress, making it one of the most popular Content Management Systems (CMS). While WordPress is commonly used for blogs, it can also power e-commerce platforms, forums, and various other types of sites. In this guide, we’ll walk through how to deploy a WordPress site on AWS, leveraging its scalability and reliability.

### **What You’ll Learn**

* Set up the infrastructure required for a WordPress site.
    
* Deploy and configure WordPress on an EC2 instance.
    
* Create and connect a MySQL database using Amazon RDS.
    

---

### **Resources to Be Created**

1. **Amazon EC2 instance** – To install and host the WordPress application.
    
2. **Amazon RDS for MySQL** – To store WordPress data.
    

Let’s dive into the step-by-step process.

---

### **Task 01: Set Up the MySQL Database (Amazon RDS)**

WordPress requires a MySQL database to store its content, such as posts, pages, and user data. Follow these steps to create an RDS database:

#### **Steps to Create RDS:**

1. **Login to AWS Management Console:**  
    Navigate to the **Amazon RDS** service.
    
2. **Create a Database Instance:**
    
    * Choose the **Standard Create** option.
        
    * Engine: Select **MySQL**.
        
    * Version: Choose the latest **MySQL-compatible version**.
        
3. **Configure Database Settings:**
    
    * **DB Instance Class:** Choose a class such as `db.t2.micro` for a low-cost option.
        
    * **Storage:** Use 20 GB of General Purpose (SSD).
        
    * **DB Identifier:** Name your database, e.g., `wordpress-db`.
        
    * **Credentials:** Set a master username (e.g., `admin`) and password (save these for later).
        
4. **Network and Security Settings:**
    
    * **VPC:** Ensure it’s in the same VPC as your EC2 instance.
        
    * **Public Access:** Enable **Yes** (if needed for testing, but restrict for production).
        
    * Add a security group allowing MySQL traffic (`port 3306`).
        
5. **Create the Database:**  
    Click **Create Database** and wait for the instance to be provisioned.
    

---

### **Task 02: Set Up the WordPress Server on Amazon EC2**

Now that your database is ready, let’s set up the server to host your WordPress application.

#### **Steps to Launch an EC2 Instance:**

1. **Login to AWS Management Console:**  
    Navigate to the **Amazon EC2** service.
    
2. **Launch an Instance:**
    
    * Choose the **Amazon Linux 2 AMI** or **Ubuntu AMI**.
        
    * Select an instance type like `t2.micro` (eligible for free tier).
        
    * Configure **Key Pair:** Download and save a key pair for SSH access.
        
3. **Network Settings:**
    
    * Assign the instance to the same VPC and subnet as your RDS database.
        
    * Add a security group allowing traffic on **HTTP (80)** and **SSH (22)**.
        
4. **Connect to Your EC2 Instance:**
    
    * Use SSH to connect:
        
        ```bash
        ssh -i your-key.pem ec2-user@your-ec2-public-ip
        ```
        

---

### **Task 03: Install WordPress and Dependencies**

After connecting to the EC2 instance, install the required software to host WordPress.

#### **Install LAMP Stack:**

1. Update packages:
    
    ```bash
    sudo yum update -y
    ```
    
2. Install Apache:
    
    ```bash
    sudo yum install -y httpd
    sudo systemctl start httpd
    sudo systemctl enable httpd
    ```
    
3. Install PHP:
    
    ```bash
    sudo yum install -y php php-mysqlnd
    ```
    
4. Install MySQL client:
    
    ```bash
    sudo yum install -y mysql
    ```
    

#### **Download and Configure WordPress:**

1. Download WordPress:
    
    ```bash
    wget https://wordpress.org/latest.tar.gz
    tar -xvf latest.tar.gz
    ```
    
2. Move WordPress files to the web directory:
    
    ```bash
    sudo mv wordpress/* /var/www/html/
    ```
    
3. Set permissions:
    
    ```bash
    sudo chown -R apache:apache /var/www/html/
    ```
    

---

### **Task 04: Configure WordPress**

1. **Create the** `wp-config.php` File:  
    Rename and edit the sample config file:
    
    ```bash
    sudo cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
    sudo nano /var/www/html/wp-config.php
    ```
    
2. **Edit Database Settings in** `wp-config.php`:
    
    * Update the database name, user, and password fields to match your RDS setup:
        
        ```php
        define('DB_NAME', 'wordpress-db');
        define('DB_USER', 'admin');
        define('DB_PASSWORD', 'your-password');
        define('DB_HOST', 'your-rds-endpoint');
        ```
        
3. Restart Apache:
    
    ```bash
    sudo systemctl restart httpd
    ```
    

---

### **Task 05: Access Your WordPress Site**

1. **Get the Public IP of Your EC2 Instance:**  
    Find the public IP in the AWS EC2 dashboard.
    
2. **Visit Your WordPress Site:**  
    Open your browser and go to:
    
    ```bash
    http://your-ec2-public-ip
    ```
    
3. **Complete the WordPress Installation Wizard:**
    
    * Choose your language.
        
    * Enter site title, admin username, password, and email.
        
    * Click **Install WordPress**.
        

---

### **Key Points to Remember**

* Ensure proper security group configurations to allow traffic between EC2 and RDS.
    
* Keep your database credentials and key pair secure.
    
* Always terminate unnecessary resources after testing to avoid extra charges.
    

---

### **Conclusion**

Congratulations! You’ve successfully deployed a WordPress site on AWS. This setup highlights AWS’s flexibility and scalability for hosting web applications. Share your deployed WordPress site with others, and continue exploring AWS for advanced features like load balancing, scaling, and security enhancements.

---

If you found this guide helpful, share it with your network! 🚀