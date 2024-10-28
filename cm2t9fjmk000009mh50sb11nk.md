---
title: "Day 23: Setting Up a Jenkins Freestyle Project for DevOps Engineers 🚀"
datePublished: Mon Oct 28 2024 16:55:35 GMT+0000 (Coordinated Universal Time)
cuid: cm2t9fjmk000009mh50sb11nk
slug: day-23-setting-up-a-jenkins-freestyle-project-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730134448484/97bb7b75-cc1a-44e8-a80d-3a9ad4e217ca.png
tags: devops, jenkins, jenkins-devops, trainwithshubham, tws

---

The community is absolutely on fire with the **#90DaysOfDevOps** journey! Today’s challenge is one that will help us take our DevOps skills to the next level: **Creating a Jenkins Freestyle Project.** This project is a fantastic way to dive into CI/CD (Continuous Integration and Continuous Delivery) practices. Ready to jump in? Let’s go! 😍

---

### What is CI/CD?

Before we begin, let's clarify what CI/CD is all about.

1. **Continuous Integration (CI)**  
    CI involves automatically integrating code changes from multiple developers into a shared codebase. Imagine that you and your team members are each working on different features. As you complete a feature, you commit your code to a central repository (like GitHub). Jenkins then automatically builds this new code, checks for any errors, and runs tests to catch issues early.
    
    **Key Benefits of CI:**
    
    * **Faster bug detection:** Issues are caught early in the development process.
        
    * **Streamlined teamwork:** Everyone’s code integrates seamlessly.
        
    * **Improved software quality:** Testing regularly helps identify and fix errors early on.
        
2. **Continuous Delivery (CD)**  
    CD takes CI a step further by ensuring that the new, tested code is ready to be deployed at any moment. After code passes integration tests, CD automates additional testing and prepares it for release, allowing developers to roll out updates quickly and with confidence.
    

---

### What is a Jenkins Build Job? 🤔

A **build job** in Jenkins is a series of steps that automate different tasks like compiling code, gathering dependencies, testing, and deploying your application. Jenkins offers various job types, but today we’ll focus on **Freestyle Projects**.

### What is a Freestyle Project in Jenkins?

A **freestyle project** in Jenkins is a simple way to create, test, and deploy your application with basic configurations. You can use it for tasks like:

* Building application code
    
* Running tests to ensure code quality
    
* Deploying code to a specific environment
    

Now, let’s dive into setting up a freestyle project in Jenkins to work with Docker. We'll go through this in two main tasks.

---

## Task 1: Creating a Basic Jenkins Freestyle Project with Docker

In this task, we’ll configure Jenkins to build and run a Docker container for a basic application. This setup is perfect for testing small projects or running isolated app instances.

### Step-by-Step Guide

### Step 1: Prepare Your Application

Before you start, make sure you have:

1. **An Application Directory**: Create a new folder, `simple-python-app`.
    
2. **A Python Script**: Inside `simple-python-app`, add an [`app.py`](http://app.py) file:
    
    ```python
    # app.py
    print("Hello, Jenkins and Docker!")
    ```
    
3. **A Dockerfile**: Inside `simple-python-app`, create a `Dockerfile`:
    
    ```dockerfile
    FROM python:3.9-slim
    WORKDIR /app
    COPY . .
    CMD ["python", "app.py"]
    ```
    

This Dockerfile sets up a minimal Python environment to run your app.

### Step 2: Create a New Jenkins Freestyle Project

1. **Go to Jenkins Dashboard**.
    

Click **New Item** &gt; **Freestyle Project** &gt; **OK**.

> <mark>Note: Verify Docker Installation and Add Jenkins User to Docker Group</mark>
> 
> ```bash
> # add in group
> sudo usermod -aG docker jenkins
> # Restart Jenkins
> sudo systemctl restart jenkins
> ```

### Step 3: Configure Build Steps in Jenkins

1. Scroll to the **Build** section.
    
2. **Add the First Build Step**:
    
    * Select **Execute shell**.
        
    * Enter the command to build the Docker image:
        
        ```bash
        docker build -t myapp-image .
        ```
        
    * if do in folder:
        
        ```bash
        cd ~/project && docker build -t myapp-image .
        ```
        
    * This command builds a Docker image named `myapp-image` using your Dockerfile.
        
3. **Add a Second Build Step**:
    
    * Select **Execute shell**.
        
    * Enter the command to run the Docker container:
        
        ```bash
        docker run -d --name myapp-container myapp-image
        ```
        
    * if you do in folder:
        
        ```bash
        cd ~/project && docker run -d --name myapp-container myapp-image
        ```
        
    * This command starts a new container from the `myapp-image`.
        

### Step 4: Test Your Jenkins Job

* Save the project and click **Build Now**. In the Console Output, you should see `Hello, Jenkins and Docker!` if everything runs correctly.
    

---

## Task 2: Automating Docker Compose with Jenkins

For larger projects, multiple containers might be needed. Here, we’ll set up a Jenkins project to start and stop multiple containers with Docker Compose. We’ll add **Redis** as an example service alongside our Python app.

### Step-by-Step Guide

### Step 1: Set Up a Docker Compose File

1. **Update** [`app.py`](http://app.py) to connect with Redis:
    
    ```python
    import redis
    
    client = redis.Redis(host='redis', port=6379)
    client.set('message', 'Hello from Jenkins and Redis!')
    print(client.get('message').decode())
    ```
    
2. **Update Dockerfile** to install the Redis client:
    
    ```dockerfile
    FROM python:3.9-slim
    WORKDIR /app
    COPY . .
    RUN pip install redis
    CMD ["python", "app.py"]
    ```
    
3. **Create a** `docker-compose.yml` File in the `simple-python-app` folder:
    
    ```yaml
    version: '3'
    services:
      app:
        build: .
        depends_on:
          - redis
    
      redis:
        image: "redis:latest"
        ports:
          - "6379:6379"
    ```
    

### Step 2: Create a New Jenkins Project for Docker Compose

1. **Go to Jenkins Dashboard** and create a new **Freestyle Project**.
    
2. Name it, like **simple-python-app-compose**, and save the initial settings.
    

### Step 3: Add Build Steps for Docker Compose

1. **In the Build Section**, add a build step with:
    
    ```bash
    docker-compose up -d
    ```
    
    * This command launches all services in `docker-compose.yml` in detached mode.
        
2. **Add a Cleanup Step**:
    
    * Add another build step with:
        
        ```bash
        docker-compose down
        ```
        
    * This will stop and remove the containers after they’re no longer needed.
        

### Step 4: Test Your Docker Compose Project

* Save and click **Build Now**.
    
* Check Console Output to see the result: the Python app should connect to Redis and output `Hello from Jenkins and Redis!`.
    

---

## Wrapping Up

In these steps, you’ve created two Jenkins Freestyle Projects:

1. A project that builds and runs a Docker container for your application.
    
2. A project that uses Docker Compose to manage multiple containers, including a cleanup process.
    

### Final Thoughts 💡

Learning Jenkins Freestyle Projects provides a strong foundation in automating tasks essential to CI/CD workflows. These projects simplify the process of building, testing, and deploying code, all crucial skills for a DevOps engineer. Stay tuned for more advanced Jenkins topics as you continue your #90DaysOfDevOps journey. Keep pushing forward—you're doing amazing!