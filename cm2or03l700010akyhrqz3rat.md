---
title: "Day 20: Docker Command Cheat-Sheet for DevOps Engineers"
datePublished: Fri Oct 25 2024 13:08:37 GMT+0000 (Coordinated Universal Time)
cuid: cm2or03l700010akyhrqz3rat
slug: day-20-docker-command-cheat-sheet-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1729861607436/a0d31f2f-cfc0-41ad-a907-059bb711f7da.png
tags: docker, 90daysofdevops, tws, dockercheatsheet, twscommunity

---

**Introduction:** **Day 20 of #90DaysOfDevOps** 🗓️ has arrived! After several hands-on sessions with Docker, I’m excited to share a comprehensive cheat-sheet covering the essential Docker and Docker Compose commands. Whether you’re diving into containerization for the first time or need a quick reference, this guide will help you manage containers like a pro. 🐳✨

> **Bonus:** For easy access and sharing, I’ve created a GitHub repository with the cheat-sheet!  
> **GitHub Repository:** [Cheat-Sheet for DevOps Engineers](https://github.com/dhruvmoradiya69000/Cheetsheet_For_Devops.git)

---

### **Why Docker is Useful (In Simple Terms)**

Docker is like a portable app environment that keeps everything an application needs in one place, making it run consistently across different computers. Here’s a simple and complete list of commands to help you master Docker!

---

### **Docker Commands Cheat-Sheet**

#### 🚀 **1\. Basic Commands for Everyday Use**

These commands help you get started with Docker, like pulling images (the base file of a container) and starting/stopping containers.

* 🔍 `docker --version`  
    *Check which version of Docker is installed.*
    
* 🌐 `docker pull <image>`  
    *Download an image (app package) from Docker Hub.*  
    **Example:**
    
    ```bash
    docker pull nginx
    ```
    
    > Imagine this as downloading an app installer. Here, "nginx" is a web server image that will be used to create containers.
    
* ▶️ `docker run <image>`  
    *Start a container from an image.*  
    **Example:**
    
    ```bash
    docker run nginx
    ```
    
    > This is like launching an app you downloaded—now the web server runs inside a container!
    
* 🛑 `docker stop <container>`  
    *Stop a running container.*  
    **Example:**
    
    ```bash
    docker stop my-nginx
    ```
    
    > Useful if you need to pause a running app without deleting it.
    

---

#### 🖼️ **2\. Image Management (Your App Library)**

Think of images as pre-configured app templates. These commands help you organize, create, and remove these images.

* 📜 `docker images`  
    *See all images you have downloaded.*
    
* 🛠️ `docker build -t <image-name> <path>`  
    *Create an image from a Dockerfile (a recipe for your container).*  
    **Example:**
    
    ```bash
    docker build -t my-app .
    ```
    
    > This creates an image from a Dockerfile, a script with instructions on how to set up your app.
    
* 🗑️ `docker rmi <image>`  
    *Delete an image you no longer need.*  
    **Example:**
    
    ```bash
    docker rmi nginx
    ```
    
    > If you’re done with an app version, delete it to save space!
    

---

#### 🌐 **3\. Networking Commands**

When containers need to “talk” to each other, these commands help you set up networks so containers can connect.

* 🌐 `docker network ls`  
    *List all available networks.*
    
* ➕ `docker network create <network-name>`  
    *Create a custom network for containers.*  
    **Example:**
    
    ```bash
    docker network create my-network
    ```
    
    > Think of this as setting up a virtual network that your containers can join.
    
* 🔗 `docker network connect <network> <container>`  
    *Connect a container to a network.*  
    **Example:**
    
    ```bash
    docker network connect my-network my-nginx
    ```
    
    > This lets the "my-nginx" container communicate with others on "my-network."
    

---

### **Docker Compose Commands Cheat-Sheet**

Docker Compose lets you define and run multiple containers at once. Imagine needing a web server and a database—Docker Compose starts both with one command.

* ▶️ `docker-compose up`  
    *Start all services defined in your docker-compose.yml file.*  
    **Example:**
    
    ```bash
    docker-compose up
    ```
    
    > Like turning on a workspace with all the apps needed for your project.
    
* 🛑 `docker-compose down`  
    *Stop and remove containers, networks, and volumes set up by Compose.*
    
* 📜 `docker-compose ps`  
    *List services defined in the docker-compose file.*
    

---

### **Real-Life Example of Docker & Docker Compose:**

Let’s say you’re creating an online shop with a **web server** and a **database** (e.g., PostgreSQL). You could use Docker Compose to start both the web server and the database with one simple command, making setup fast and consistent!

**Example docker-compose.yml:**

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
```

**To start both services, simply run:**

```bash
docker-compose up
```

> Now both the web server (for your shop) and the database (to store data) start at once. No need for individual commands!

---

### **Why Keep a Docker Cheat-Sheet?**

This cheat-sheet is a go-to for keeping Docker commands at your fingertips. Whether you’re launching containers, managing images, or connecting services, this will save you time and make Docker simpler.

### **Conclusion:**

Wrapping up **Day 20** of #90DaysOfDevOps with this Docker command cheat-sheet! 🎉 Bookmark it for easy access, and if you have any tips or favorite commands, let me know in the comments below. 🚀 Happy Docker-ing!