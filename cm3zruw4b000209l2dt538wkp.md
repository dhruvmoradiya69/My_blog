---
title: "Day 53: Your CI/CD Pipeline on AWS - Part 4 🚀☁"
datePublished: Wed Nov 27 2024 10:57:44 GMT+0000 (Coordinated Universal Time)
cuid: cm3zruw4b000209l2dt538wkp
slug: day-53-your-cicd-pipeline-on-aws-part-4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1732704914344/b00ec2bd-1a5d-4ae5-92ea-e63299b4ad91.webp
tags: aws, devops, 90daysofdevops, tws, aws-codepipeline-devops-cicd-cloudcomputing-automation-learningjourney

---

Congratulations on reaching the final stage of building your CI/CD pipeline on AWS! So far, you’ve worked with **AWS CodeCommit**, **CodeBuild**, and **CodeDeploy**. Today, you’ll bring it all together with **AWS CodePipeline**, the service that orchestrates the entire pipeline. Let’s finish strong!

---

## What is AWS CodePipeline?

**AWS CodePipeline** automates your release process by building, testing, and deploying your code whenever changes are made. It integrates seamlessly with tools like CodeCommit, CodeBuild, and CodeDeploy to create an efficient and reliable CI/CD pipeline.

Key benefits of CodePipeline:

* Automated workflows for faster delivery.
    
* Integration with various AWS services and third-party tools.
    
* Continuous monitoring for deployment success or failure.
    

---

## Task 01: Set Up a Deployment Group

### **Steps**:

1. **Prepare Your EC2 Instances**:
    
    * Ensure the CodeDeploy agent is installed and running (refer to **Day 52** for details).
        
    * Tag the EC2 instances (e.g., `Key=Environment, Value=Production`) for grouping.
        
2. **Create a Deployment Group in CodeDeploy**:
    
    * Go to **AWS CodeDeploy** in the AWS Management Console.
        
    * Select the application you created earlier.
        
    * Click **Create Deployment Group** and provide:
        
        * **Name**: e.g., `MyDeploymentGroup`.
            
        * **Service Role**: Select the CodeDeploy IAM role.
            
        * **Deployment Settings**: Choose your deployment type (e.g., `In-place` or `Blue/Green`).
            
        * **Environment Configuration**: Choose `Amazon EC2 instances` and filter by tags.
            
3. **Save the Deployment Group**.
    

---

## Task 02: Create a CodePipeline

### **Steps**:

1. **Go to CodePipeline in AWS Console**:
    
    * Navigate to **AWS CodePipeline** and click **Create Pipeline**.
        
2. **Configure Pipeline Settings**:
    
    * **Pipeline Name**: e.g., `MyCICDPipeline`.
        
    * **Service Role**: Select an existing role or create a new one.
        
3. **Add Source Stage**:
    
    * Select **CodeCommit** as the source provider.
        
    * Choose your repository and branch (e.g., `main`).
        
4. **Add Build Stage**:
    
    * Select **AWS CodeBuild** as the build provider.
        
    * Choose your existing build project or create a new one.
        
5. **Add Deploy Stage**:
    
    * Select **AWS CodeDeploy** as the deploy provider.
        
    * Choose your application and deployment group created in Task 01.
        
6. **Review and Create Pipeline**:
    
    * Review all settings, then click **Create Pipeline**.
        
    * The pipeline will automatically trigger on code changes in CodeCommit.
        

---

### Key Takeaways

* **CodePipeline** ties together the CI/CD workflow, automating the entire process from source to deployment.
    
* By integrating CodeCommit, CodeBuild, and CodeDeploy, you achieve a fully automated, reliable release pipeline.
    
* Congratulations on completing your AWS CI/CD pipeline journey!
    

---

Stay tuned for more AWS tutorials, and keep building! 🌟