---
title: "Day 59 - Deploying a Web App with Ansible 🚀"
datePublished: Fri Dec 06 2024 11:32:36 GMT+0000 (Coordinated Universal Time)
cuid: cm4co2ejj000409mkheg5edmm
slug: day-59-deploying-a-web-app-with-ansible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733484708510/bf0dab00-d65f-4f48-b66f-2133f273abc9.webp
tags: aws, ansible, devops

---

I**ntroduction**  
Automation simplifies complex tasks, and **Ansible** is a shining star in the automation space. Today, let's embark on a hands-on project: deploying a simple web app using Ansible. By the end of this task, you'll learn how to create EC2 instances, set up Ansible, and deploy a web application—all with seamless automation.

---

### **What You’ll Learn**

This blog walks you through deploying a sample web application using **Ansible**. Here's a snapshot of what we’ll do:

* Set up **three EC2 instances** on AWS.
    
* Configure **Ansible** on the host server.
    
* Use an **Ansible playbook** to install Nginx and deploy a sample webpage.
    

Whether you're a DevOps enthusiast or a beginner exploring automation, this guide offers detailed, actionable steps.

---

### **Step-by-Step Guide to Deploying a Web App**

---

#### **Task 01: Set Up EC2 Instances**

1. **Create Three EC2 Instances**:
    
    * Launch three AWS EC2 instances with the same **Key Pair** for SSH access.
        
    * Use the **Ubuntu** image for consistency.
        
    
    **Command Example (AWS CLI):**
    
    ```bash
    aws ec2 run-instances \
      --image-id ami-12345678 \
      --count 3 \
      --instance-type t2.micro \
      --key-name your-key-pair \
      --security-group-ids sg-12345678 \
      --subnet-id subnet-12345678
    ```
    
    *Pro Tip*: Ensure the security group allows SSH (port 22) and HTTP (port 80) access.
    
2. **Identify the Instances**:
    
    * Note down the public IPs of your instances for configuring Ansible.
        

---

#### **Task 02: Set Up the Ansible Host Server**

1. **Install Ansible on the Host Server**:
    
    * SSH into your host server and install Ansible.
        
    * For **Ubuntu**, use:
        
        ```bash
        sudo apt update
        sudo apt install ansible -y
        ```
        
2. **Transfer the Private Key**:
    
    * Copy your EC2 **Key Pair** file to the host server for seamless SSH access to the instances.
        
    
    **Command Example (From Local to Host Server):**
    
    ```bash
    scp -i your-key.pem your-key.pem ubuntu@host-server-ip:/home/ubuntu/.ssh/
    ```
    
3. **Set Permissions**:
    
    ```bash
    chmod 600 /home/ubuntu/.ssh/your-key.pem
    ```
    

---

#### **Task 03: Configure Ansible Inventory**

1. **Edit the Inventory File**:
    
    * Open the **inventory file** to add the IPs of your EC2 instances.
        
        ```bash
        sudo vim /etc/ansible/hosts
        ```
        
    * Add the following content:
        
        ```ini
        [webservers]
        instance1 ansible_host=<public-ip-1> ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/.ssh/your-key.pem
        instance2 ansible_host=<public-ip-2> ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/.ssh/your-key.pem
        instance3 ansible_host=<public-ip-3> ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/.ssh/your-key.pem
        ```
        
2. **Test Connectivity**:
    
    ```bash
    ansible -m ping all
    ```
    
    * If successful, you'll see a "pong" response for all instances.
        

---

#### **Task 04: Write and Execute an Ansible Playbook**

1. **Create the Playbook File**:
    
    * Use a YAML file to define your Ansible playbook:
        
        ```bash
        sudo vim nginx_webapp.yml
        ```
        
    
    **Sample Playbook Content**:
    
    ```yaml
    ---
    - name: Deploy Nginx and a Sample Web Page
      hosts: webservers
      become: true
      tasks:
        - name: Install Nginx
          apt:
            name: nginx
            state: present
            update_cache: yes
    
        - name: Start and enable Nginx
          service:
            name: nginx
            state: started
            enabled: yes
    
        - name: Deploy sample HTML page
          copy:
            content: "<h1>Welcome to My Ansible Web App!</h1>"
            dest: /var/www/html/index.html
    ```
    
2. **Run the Playbook**:
    
    ```bash
    ansible-playbook nginx_webapp.yml
    ```
    

---

### **Why This Project Matters**

* **Hands-On Learning**: Gain practical experience with Ansible by configuring servers and deploying a web app.
    
* **Automation Expertise**: Understand how to automate repetitive server management tasks.
    
* **Scalability**: Learn how Ansible simplifies managing multiple servers in a distributed environment.
    

---

### **Final Thoughts**

This project is a stepping stone for mastering **Ansible** and server automation. As you successfully deploy the web app, you’ll appreciate how much time and effort automation tools like Ansible save in real-world scenarios.