---
title: "Day 18: Mastering Docker Compose – A Step Forward in My DevOps Journey 🚀"
datePublished: Wed Oct 23 2024 17:00:15 GMT+0000 (Coordinated Universal Time)
cuid: cm2m4eacv000609jq29fw5ojn
slug: day-18-mastering-docker-compose-a-step-forward-in-my-devops-journey
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1729702762358/707e771c-ab6d-4c26-a7fb-0404d276270a.png

---

🚀 **Day 18 of #90DaysOfDevOps: Diving into Docker Compose!**

As DevOps engineers, we are often tasked with managing complex, multi-container applications. Docker simplifies this process with **Docker Compose**, a powerful tool designed to define and manage multi-container Docker applications using a single YAML configuration file. In this blog, we’ll explore Docker Compose and walk through some essential commands to enhance your Docker skills!

---

### 📚 **What is Docker Compose?**

**Docker Compose** allows us to define services, networks, and volumes in a YAML file, enabling us to spin up, scale, and orchestrate multi-container environments with just one command! Instead of running multiple `docker run` commands, Docker Compose simplifies it into a single `docker-compose up` or `docker-compose down`.

---

### 📝 **What is YAML?**

Before we dive into Docker Compose, let’s briefly touch on **YAML**, the format we use to define our services.

* YAML stands for "Yet Another Markup Language" or "YAML Ain’t Markup Language."
    
* It's a human-readable data serialization format, making it easy to write and understand configuration files.
    
* Files have the `.yml` or `.yaml` extension.
    

Let’s explore a sample Docker Compose configuration to understand it better!

---

### 📄 **Sample** `docker-compose.yml` File

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
  database:
    image: postgres:latest
    environment:
      POSTGRES_USER: exampleuser
      POSTGRES_PASSWORD: examplepass
```

* **Version:** Defines the Docker Compose file version.
    
* **Services:** Lists containers for the web server and database.
    
    * **web:** A service using the latest NGINX image.
        
    * **database:** A service running PostgreSQL with environment variables for configuration.
        

---

### 🛠️ **Task 1: Setting Up a Multi-Container Environment with Docker Compose**

Here’s a step-by-step guide to using the `docker-compose.yml` file:

1. **Create the** `docker-compose.yml` file: Create a file in your project directory and paste the sample YAML configuration above.
    
2. **Configure services and links:** Define services such as databases, web servers, or caching systems and how they should connect.
    
3. **Use environment variables:** Set environment variables inside the YAML file for easy configuration (e.g., database credentials).
    
4. **add docker compose install**
    
    * **Run the command to install**:
        
        ```bash
        sudo apt install docker-compose
        ```
        
5. **Spin up the services:** Run the following command to start all services:
    
    ```yaml
    docker-compose up -d
    ```
    
    The `-d` flag runs the services in detached mode (in the background).
    
6. **Stop the services:** Bring everything down by running:
    
    ```yaml
    docker-compose down
    ```
    

---

### 🧩 **Task 2: Running Pre-Existing Docker Images**

Let’s now move on to pulling a Docker image and running it on your local machine.

1. **Pull an image from Docker Hub:** For example, let’s pull the latest **NGINX** image:
    
    ```yaml
    docker pull nginx:latest
    ```
    
2. **Run the container as a non-root user:** Use the `usermod` command to add your user to the Docker group:
    
    ```yaml
    sudo usermod -aG docker $USER
    ```
    
    Reboot your system to apply the changes.
    
3. **Inspect the container:** After running the container, use `docker inspect` to check the running processes and exposed ports:
    
    ```bash
    docker inspect <container_id>
    ```
    
4. **View container logs:** Use `docker logs` to see the output of your container:
    
    ```bash
    docker logs <container_id>
    ```
    
5. **Stop and start the container:**
    
    * Stop the container:
        
        ```bash
        docker stop <container_id>
        ```
        
    * Start the container again:
        
        ```bash
        docker start <container_id>
        ```
        
6. **Remove the container:** Once you're done with the container, you can remove it:
    
    ```bash
    docker rm <container_id>
    ```
    

---

### 🔑 **Key Takeaways**

* Docker Compose simplifies multi-container environments.
    
* YAML is a configuration format used in Docker Compose.
    
* You can easily manage, inspect, and log containers using Docker commands without `sudo`.
    

If you’re eager to dive deeper into Docker Compose, start by building your own `docker-compose.yml` files for various applications. Automate your infrastructure and streamline DevOps tasks with ease!

---

💡 *Stay tuned for more Docker lessons as we progress through the #90DaysOfDevOps challenge!* 👨‍💻