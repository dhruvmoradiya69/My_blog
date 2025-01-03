---
title: "Day 75: Sending Docker Logs to Grafana"
datePublished: Fri Jan 03 2025 11:36:28 GMT+0000 (Coordinated Universal Time)
cuid: cm5goj8i4000j09la1dqy02b3
slug: day-75-sending-docker-logs-to-grafana
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1735904143025/69aa2a51-f73b-4f3b-9087-020547691945.webp
tags: docker, aws, grafana

---

Monitoring application performance is crucial in modern DevOps workflows. Today, we'll take it a step further by integrating Docker container logs into Grafana for real-time visualization. This hands-on project adds a valuable skill to your resume while giving you practical experience in monitoring tools.

Let’s dive into what, why, and how to accomplish this task!

---

## **What Will You Do?**

1. Install Docker on a Linux EC2 instance using User Data.
    
2. Deploy two Docker containers running a simple application (a To-Do app).
    
3. Configure Docker to send real-time logs to Grafana via Loki.
    
4. Visualize and analyze these logs in the Grafana UI.
    

---

## **Why Is This Important?**

1. **Centralized Monitoring:** Grafana provides a unified dashboard to monitor logs from multiple containers.
    
2. **Real-Time Insights:** Logs are streamed in real-time, enabling quicker diagnosis of issues.
    
3. **Resume-Worthy:** Proficiency in tools like Docker, Grafana, and Loki demonstrates strong DevOps skills.
    

---

## **How to Accomplish This?**

### **Step 1: Automate Docker Installation on EC2**

Launch your Linux EC2 instance with the following User Data script to automatically install and start Docker:

```bash
#!/bin/bash
sudo yum update -y
sudo amazon-linux-extras install docker -y
sudo service docker start
sudo systemctl enable docker
sudo usermod -a -G docker ec2-user
```

This script ensures Docker is installed, the service is running, and the `ec2-user` has permission to run Docker commands.

---

### **Step 2: Deploy Applications in Docker Containers**

1. **SSH into Your Instance:**  
    Use your EC2 instance's public IP to connect.
    
    ```bash
    ssh -i <your-key.pem> ec2-user@<public-ip>
    ```
    
2. **Run Two Docker Containers:**  
    Pull a pre-built To-Do app image from Docker Hub and run two containers.
    
    ```bash
    docker pull <todo-app-image>
    docker run -d --name todo-app-1 -p 8081:80 <todo-app-image>
    docker run -d --name todo-app-2 -p 8082:80 <todo-app-image>
    ```
    
    Replace `<todo-app-image>` with the actual image name from Docker Hub.  
    Access the applications at `http://<public-ip>:8081` and `http://<public-ip>:8082`.
    

---

### **Step 3: Configure Docker to Send Logs to Grafana**

1. **Install Loki Docker Plugin:**
    
    ```bash
    docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
    ```
    
2. **Update Docker Configuration for Loki:**  
    Edit the `/etc/docker/daemon.json` file to configure the Loki logging driver.
    
    ```json
    {
      "log-driver": "loki",
      "log-opts": {
        "loki-url": "http://<loki-server>:3100/loki/api/v1/push"
      }
    }
    ```
    
    Replace `<loki-server>` with your Loki server's IP or domain.
    
3. **Restart Docker Service:**
    
    ```bash
    sudo systemctl restart docker
    ```
    
4. **Run Containers with Loki Logging:**  
    Restart your containers with the Loki logging driver:
    
    ```bash
    docker run -d --name todo-app-1 -p 8081:80 \
      --log-driver=loki \
      --log-opt loki-url="http://<loki-server>:3100/loki/api/v1/push" \
      <todo-app-image>
    ```
    

---

### **Step 4: Visualize Logs in Grafana**

1. **Add Loki as a Data Source:**
    
    * Navigate to **Configuration &gt; Data Sources** in Grafana.
        
    * Select **Loki** and set the URL to `http://<loki-server>:3100`.
        
2. **Explore Logs:**
    
    * Go to **Explore** in Grafana.
        
    * Use queries like `{container_name="todo-app-1"}` to view logs from specific containers.
        

---

## **Hands-On Tasks for Practice**

1. **Verify Docker Installation:**
    
    ```bash
    docker --version
    sudo systemctl status docker
    ```
    
2. **Test Application Accessibility:**  
    Access the To-Do app via your browser using:
    
    ```plaintext
    http://<public-ip>:8081  
    http://<public-ip>:8082  
    ```
    
3. **Explore Logs in Grafana:**  
    Confirm real-time logs appear for both containers.
    

---

## **Conclusion**

By completing this project, you’ve automated Docker setup, deployed applications in containers, and integrated real-time logs into Grafana. This workflow not only enhances your understanding of DevOps tools but also demonstrates your ability to manage and monitor containerized applications effectively.