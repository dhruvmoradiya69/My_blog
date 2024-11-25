---
title: "Day 51: Your CI/CD Pipeline on AWS - Part 2 🚀☁"
datePublished: Mon Nov 25 2024 11:43:08 GMT+0000 (Coordinated Universal Time)
cuid: cm3wylkqn000609kvbhji4rrj
slug: day-51-your-cicd-pipeline-on-aws-part-2
tags: aws, pipeline, ci-cd, 90daysofdevops, trainwithshubham, tws, aws-cicd

---

Welcome to Part 2 of building your CI/CD pipeline on AWS! Yesterday, you set up **AWS CodeCommit** as your version control system. Today, we’ll dive into **AWS CodeBuild**, a powerful tool to compile your code, run tests, and prepare deployment artifacts. Let’s continue the journey step by step.

---

## What is AWS CodeBuild?

**AWS CodeBuild** is a fully managed **build service** that eliminates the need to maintain your own build servers. It helps you:

* Compile source code and run **unit tests**.
    
* Produce **build artifacts** ready for deployment.
    
* Automatically scale based on your build requirements.
    
* Easily integrate with AWS services like CodePipeline and CodeDeploy for CI/CD.
    

---

## Tasks for Today

### **Task 01: Learn About Buildspec File and Set Up CodeBuild**

#### Requirements:

* A valid **AWS IAM role** with permissions for CodeBuild.
    
* A basic understanding of Nginx.
    

#### Steps:

1. **Read About the** `buildspec.yml` File:
    
    * The `buildspec.yml` file is the heart of AWS CodeBuild. It defines:
        
        * **Phases** like install, build, and post-build.
            
        * **Commands** to execute during the build process.
            
        * The location of your output **artifacts**.
            
    * Example structure:
        
        ```yaml
        version: 0.2
        phases:
          install:
            commands:
              - echo "Installing dependencies"
          build:
            commands:
              - echo "Building project"
        artifacts:
          files:
            - '**/*'
        ```
        
2. **Create an** `index.html` File in CodeCommit:
    
    * In your local cloned repository, add an `index.html` file:
        
        ```xml
        <!DOCTYPE html>
        <html>
        <head>
          <title>AWS CodeBuild Example</title>
        </head>
        <body>
          <h1>Hello from AWS CodeBuild!</h1>
        </body>
        </html>
        ```
        
    * Commit and push the file to CodeCommit:
        
        ```bash
        git add index.html
        git commit -m "Added index.html"
        git push origin main
        ```
        
3. **Set Up an Nginx Server**:
    
    * You’ll configure CodeBuild to serve `index.html` using Nginx during the build process.
        

---

### **Task 02: Add** `buildspec.yml` and Complete the Build

#### Steps:

1. **Create the** `buildspec.yml` File:
    
    * In your local repository, add a `buildspec.yml`:
        
        ```yaml
        version: 0.2
        phases:
          install:
            commands:
              - echo "Installing Nginx"
              - yum install -y nginx
          build:
            commands:
              - echo "Copying index.html to Nginx root"
              - cp index.html /usr/share/nginx/html/index.html
        artifacts:
          files:
            - '**/*'
        ```
        
    * Commit and push it to CodeCommit:
        
        ```bash
        git add buildspec.yml
        git commit -m "Added buildspec.yml for Nginx setup"
        git push origin main
        ```
        
2. **Create a Build Project in AWS CodeBuild**:
    
    * Go to **CodeBuild** in the AWS Console.
        
    * Click **Create Build Project** and provide details:
        
        * **Source**: Select your CodeCommit repository.
            
        * **Buildspec**: Choose "Use a buildspec file" and specify the file path (default: `buildspec.yml`).
            
        * **Environment**: Use a managed image (e.g., Amazon Linux).
            
    * Start the build process.
        
3. **Verify the Build**:
    
    * Check the build logs for successful execution of the `buildspec.yml`.
        
    * Artifacts should be generated as specified in the file.
        

---

### Key Takeaways

* **CodeBuild** automates your build process, eliminating manual effort.
    
* The `buildspec.yml` file is essential for defining your build phases and commands.
    
* Today, you integrated Nginx into your build process, preparing for seamless deployment in the next steps.
    

---

Stay tuned for **Part 3**, where we’ll move on to **AWS CodeDeploy**!