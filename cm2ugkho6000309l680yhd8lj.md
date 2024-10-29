---
title: "Day 24: Building a CI/CD Pipeline for Node.js Application with Jenkins"
datePublished: Tue Oct 29 2024 13:03:09 GMT+0000 (Coordinated Universal Time)
cuid: cm2ugkho6000309l680yhd8lj
slug: day-24-building-a-cicd-pipeline-for-nodejs-application-with-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730206930256/2b7a0680-8bf4-4ea6-bf14-3c71bec68d04.png
tags: devops, cicd, jenkins-devops, 90daysofdevops, tws

---

Today, we’re diving into a hands-on project to build a Continuous Integration and Continuous Deployment (CI/CD) pipeline for a Node.js application using **Jenkins**. If you’ve followed along with the previous days, you already have a solid foundation. Now, let’s put it all together! 🚀

---

### **What is CI/CD?** 🤔

Before we begin, let’s briefly understand what CI/CD means:

* **CI (Continuous Integration)**: A practice where developers frequently merge their code changes into a central repository, followed by automated builds and tests.
    
* **CD (Continuous Deployment)**: Automates the delivery of applications to selected infrastructure environments.
    

This project will allow you to automate your Node.js application’s testing and deployment processes, making your workflow more efficient! 💪

---

### **Task 1: Setting Up Your Project** 🛠️

#### **Step 1: Fork the Repository** 🍴

1. **Forking a Repository**:
    
    * Go to the GitHub repository you want to work with.
        
    * Click on the "Fork" button in the top right corner to create your own copy of the repository. This way, you can make changes without affecting the original project.
        

#### **Step 2: Connect Jenkins with GitHub** 🔗

1. **Set Up GitHub Integration in Jenkins**:
    
    * In your Jenkins dashboard, click on “New Item” to create a new job.
        
    * Choose “Freestyle project” and name it something like “NodeJS-CI-CD.”
        
    * Scroll down to the “Source Code Management” section and select “Git.”
        
    * Paste your forked repository URL in the repository field.
        
2. **Configure GitHub Webhooks**:
    
    * Navigate to your GitHub repository settings.
        
    * Select “Webhooks” from the sidebar and click “Add webhook.”
        
    * Enter your Jenkins server URL followed by `/github-webhook/`. This allows GitHub to send notifications to Jenkins when code is pushed.
        
    * Set the content type to “application/json” and select the events you want to trigger the webhook. The default setting for “Just the push event” is usually sufficient.
        
    * Click “Add webhook” to save.
        

#### **Step 3: Watch a Tutorial** 📹

* **Learning Resource**: It’s always a good idea to follow a tutorial if you're new to this. Check out the video linked in your task description. This will guide you through the entire setup step-by-step, making it easier to understand.
    
* check out [reference](https://www.youtube.com/live/nplH3BzKHPk?si=qasgcXauvJ3Vix0f) .
    

---

### **Task 2: Running Your Application with Docker** 🐳

#### **Step 1: Set Up Docker Compose** 📦

1. **What is Docker Compose?**:
    
    * Docker Compose is a tool that lets you define and run multi-container Docker applications. You can use a simple YAML file to configure your application’s services, networks, and volumes.
        
2. **Create a Docker Compose File**:
    
    * In the root of your Node.js project, create a file named `docker-compose.yml`.
        
    * Add the following configuration to it (make adjustments based on your application requirements):
        
    
    ```yaml
    version: '3'
    services:
      app:
        build: .
        ports:
          - "3000:3000"
        volumes:
          - .:/app
        environment:
          - NODE_ENV=production
    ```
    
    This configuration tells Docker to build your Node.js app and run it on port 3000, while also mounting your application code so changes are reflected immediately.
    

#### **Step 2: Execute Shell Commands in Jenkins** 🖥️

1. **Configure Jenkins to Use Docker Compose**:
    
    * Go back to your Jenkins job configuration.
        
    * In the “Build” section, select “Execute Shell.”
        
    * Enter the command to run your Docker Compose file:
        
    
    ```bash
    docker-compose up --build
    ```
    
    This command builds your Docker images and starts your application.
    

#### **Step 3: Celebrate Your Success! 🎊**

* **Run Your Jenkins Job**: Save the configuration and build the job. Jenkins will pull your code from GitHub, build your Docker containers, and start your Node.js application.
    
* **Check the Output**: Monitor the console output to ensure everything is running smoothly. If there are any errors, don’t worry! This is part of the learning process.
    

---

### **Conclusion** 🎓

Congratulations! You’ve successfully built a CI/CD pipeline for your Node.js application using **Jenkins** and **Docker**. This project is a fantastic addition to your resume, showcasing your ability to integrate modern development practices into real-world applications.

By automating your deployment process, you’ve taken a significant step toward becoming a proficient **DevOps** engineer. Keep practicing and exploring, and don’t hesitate to reach out if you have questions or need support. **Happy coding!** 🚀