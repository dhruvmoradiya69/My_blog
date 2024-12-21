---
title: "Day 73 - Grafana: A Hands-On Guide to Setting Up Grafana on AWS EC2 🌟"
datePublished: Sat Dec 21 2024 11:26:07 GMT+0000 (Coordinated Universal Time)
cuid: cm4y3fuqk000t09la1tst2hnb
slug: day-73-grafana-a-hands-on-guide-to-setting-up-grafana-on-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734780332875/0ad38996-edf4-4fe3-b4b3-85ad1a0ee193.webp
tags: ec2, aws, grafana, grafana-dashboard

---

If you’ve been following along with our Grafana series, you should now have a solid understanding of the basics—what Grafana is, why it’s used, and its incredible capabilities. Today, we’re diving into the practical side of things with a hands-on task: **Setting up Grafana in a local environment on AWS EC2**. Let’s explore the **what**, **how**, and **why** of this task in detail.

---

## **What is Grafana?**

Grafana is an open-source platform for data visualization, monitoring, and observability. It lets you create customizable dashboards to visualize metrics from various data sources like Prometheus, Elasticsearch, and InfluxDB. It’s widely used for monitoring infrastructure, applications, and business processes.

---

## **Why Set Up Grafana Locally on AWS EC2?**

1. **Hands-On Experience:** Setting up Grafana locally on EC2 gives you practical knowledge, bridging the gap between theory and real-world scenarios.
    
2. **Scalability Testing:** EC2 provides a scalable cloud environment to mimic real-world use cases.
    
3. **Cost-Effective Learning:** With AWS Free Tier, you can experiment with minimal costs.
    
4. **Foundation for Advanced Use:** Once you’ve mastered local setup, you can expand to integrate Grafana with multiple data sources or even set up clusters for high availability.
    

---

## **How to Set Up Grafana on AWS EC2**

Follow these steps to get Grafana running on an EC2 instance:

### **Step 1: Launch an AWS EC2 Instance**

1. Log in to your AWS Management Console.
    
2. Navigate to **EC2 Dashboard**.
    
3. Click **Launch Instance** and configure:
    
    * **AMI:** Choose Amazon Linux 2 or Ubuntu.
        
    * **Instance Type:** Select a free-tier eligible type, such as `t2.micro`.
        
    * **Key Pair:** Create or use an existing key pair for SSH access.
        
    * **Security Group:** Open ports `22` (SSH) and `3000` (Grafana default port).
        
4. Click **Launch** to start the instance.
    

---

### **Step 2: Connect to Your EC2 Instance**

1. Open a terminal on your local machine.
    
2. Use the following SSH command to connect:
    
    ```bash
    ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
    ```
    
3. Replace `your-key.pem` with your key file and `your-ec2-public-ip` with the instance’s public IP address.
    

---

### **Step 3: Install Grafana**

1. Update the system packages:
    
    ```bash
    sudo apt update && sudo apt upgrade -y   # For Ubuntu
    sudo yum update -y                       # For Amazon Linux
    ```
    
2. Add the Grafana repository and install Grafana:
    
    * For Ubuntu:
        
        ```bash
        sudo apt-get install -y software-properties-common
        sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
        sudo apt-get update
        sudo apt-get install -y grafana
        ```
        
    * For Amazon Linux:
        
        ```bash
        sudo tee /etc/yum.repos.d/grafana.repo <<-'EOF'
        [grafana]
        name=grafana
        baseurl=https://packages.grafana.com/oss/rpm
        repo_gpgcheck=1
        enabled=1
        gpgcheck=1
        gpgkey=https://packages.grafana.com/gpg.key
        EOF
        sudo yum install grafana -y
        ```
        

---

### **Step 4: Start and Enable Grafana**

1. Start the Grafana service:
    
    ```bash
    sudo systemctl start grafana-server
    ```
    
2. Enable Grafana to start on boot:
    
    ```bash
    sudo systemctl enable grafana-server
    ```
    
3. Check the service status to ensure it’s running:
    
    ```bash
    sudo systemctl status grafana-server
    ```
    

---

### **Step 5: Access Grafana**

1. Open a browser on your local machine.
    
2. Navigate to [`http://your-ec2-public-ip:3000`](http://your-ec2-public-ip:3000).
    
3. Log in with the default credentials:
    
    * Username: `admin`
        
    * Password: `admin`
        
4. Change the default password as prompted for security reasons.
    

---

## **Optional Tasks for Exploration**

1. **Connect a Data Source:** Add a data source like Prometheus or InfluxDB to Grafana and start visualizing metrics.
    
2. **Create a Dashboard:** Experiment with creating custom dashboards to represent your data visually.
    
3. **Enable Alerts:** Set up alerting rules to receive notifications for specific conditions.
    

---

## **Conclusion**

Setting up Grafana on AWS EC2 is a valuable exercise that reinforces your understanding of monitoring and observability tools. With the steps outlined above, you’ll have a fully functional Grafana instance up and running in no time. Whether you’re monitoring server performance, application logs, or business metrics, Grafana’s flexibility and visual appeal make it an indispensable tool for any tech stack.

Now it’s your turn! Complete the setup, and share your experience in the comments. Let’s learn together! 🚀