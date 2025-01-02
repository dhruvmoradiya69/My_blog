---
title: "Day 74: Connecting EC2 with Grafana – Monitor Your Instances Like a Pro"
datePublished: Thu Jan 02 2025 12:01:27 GMT+0000 (Coordinated Universal Time)
cuid: cm5f9zibf001l09ldgjzke60y
slug: day-74-connecting-ec2-with-grafana-monitor-your-instances-like-a-pro
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1735819238963/950434f4-e93c-47a0-b591-bb213111d954.webp
tags: aws, grafana, grafana-monitoring, grafana-dashboard

---

## **Introduction**

Yesterday, you accomplished a significant milestone by setting up Grafana locally. Kudos to you! Now, let’s take it up a notch. In today’s session, we’ll connect **Linux** and **Windows EC2 instances** to Grafana, enabling you to monitor their metrics effectively. By the end of this blog, you’ll have a functional setup to visualize and analyze server performance metrics in real time.

## **What is Grafana, and Why Connect EC2 Instances?**

Grafana is a powerful open-source tool for visualizing and analyzing metrics. It supports multiple data sources, making it a go-to choice for server monitoring. By connecting EC2 instances to Grafana, you can:

* **Track server performance metrics** like CPU usage, memory, disk I/O, and network traffic.
    
* **Identify bottlenecks** in real-time.
    
* **Gain actionable insights** to optimize your infrastructure.
    

## **How to Connect EC2 Instances with Grafana**

Here’s a step-by-step guide to connecting both Linux and Windows EC2 instances to Grafana.

### **Step 1: Prerequisites**

Before diving in, ensure you have the following:

1. **Grafana installed and running locally or on a server** (Refer to Day 73).
    
2. **AWS EC2 instances ready** – one Linux and one Windows instance.
    
3. **Access to AWS CloudWatch** – Grafana integrates seamlessly with CloudWatch for EC2 metrics.
    
4. **IAM Role** with CloudWatch read permissions attached to your EC2 instances.
    

---

### **Step 2: Set Up AWS CloudWatch Integration**

1. **Create an IAM Role**:
    
    * Navigate to the **IAM Console** in AWS.
        
    * Create a new role for **EC2** and attach the policy **CloudWatchAgentServerPolicy**.
        
    * Attach this role to both your Linux and Windows EC2 instances.
        
2. **Enable CloudWatch Logs**:
    
    * Ensure your instances have CloudWatch logs enabled to stream metrics.
        

---

### **Step 3: Install the CloudWatch Agent**

#### On Linux EC2:

1. SSH into your Linux instance.
    
2. Install the CloudWatch Agent:
    
    ```bash
    sudo yum install amazon-cloudwatch-agent
    ```
    
3. Configure the agent:
    
    ```bash
    sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
    ```
    
    * Choose **EC2 Instance** as the source.
        
    * Enable metrics for CPU, memory, and disk.
        
4. Start the agent:
    
    ```bash
    sudo systemctl start amazon-cloudwatch-agent
    ```
    

#### On Windows EC2:

1. RDP into your Windows instance.
    
2. Download the CloudWatch Agent MSI package from the [AWS website](https://docs.aws.amazon.com/).
    
3. Run the installer and follow the on-screen instructions.
    
4. Configure the agent using the **CloudWatch Agent Wizard**.
    

---

### **Step 4: Configure Grafana to Pull CloudWatch Data**

1. **Add a Data Source** in Grafana:
    
    * Log in to Grafana.
        
    * Navigate to **Configuration &gt; Data Sources**.
        
    * Select **CloudWatch**.
        
2. **Set Up CloudWatch in Grafana**:
    
    * Enter your **AWS Access Key** and **Secret Key**.
        
    * Choose the appropriate **AWS Region**.
        
    * Save the configuration.
        
3. **Create a Dashboard**:
    
    * Go to **Dashboards &gt; New Dashboard**.
        
    * Add a panel and select **CloudWatch** as the data source.
        
    * Configure the panel to display metrics like CPUUtilization, DiskReadOps, and NetworkIn.
        

---

### **Step 5: Monitor Linux and Windows EC2 Metrics**

1. For Linux, monitor:
    
    * CPU usage
        
    * Memory consumption
        
    * Disk I/O performance
        
2. For Windows, track:
    
    * Disk utilization
        
    * Network traffic
        
    * Active processes
        

Use Grafana’s powerful visualization tools to create graphs, alerts, and thresholds.

---

## **Why Monitor EC2 Instances with Grafana?**

Monitoring your EC2 instances ensures your infrastructure is:

* **Resilient** – Detect and resolve issues before they impact users.
    
* **Scalable** – Identify trends to plan for future capacity.
    
* **Efficient** – Optimize resources to reduce costs.
    

## **Hands-On Task**

1. Follow the steps to connect your Linux and Windows EC2 instances to Grafana.
    
2. Create a dashboard with at least three panels for each instance:
    
    * CPU usage
        
    * Disk I/O
        
    * Network metrics
        
3. Set up alerts for high CPU usage or low memory.
    

---

## **Conclusion**

By connecting your EC2 instances to Grafana, you’ve taken a significant step in mastering server monitoring. This integration not only provides real-time insights but also empowers you to make data-driven decisions. Keep experimenting with different metrics and visualizations to get the most out of Grafana.