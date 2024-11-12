---
title: "Day 38: Getting Started with AWS Basics ☁"
datePublished: Tue Nov 12 2024 12:52:51 GMT+0000 (Coordinated Universal Time)
cuid: cm3egd63n000l09mebpiwakhb
slug: day-38-getting-started-with-aws-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731415912579/95252821-4608-4409-ad2a-d26651f05fa1.png
tags: aws, devops, aws-iam, 90daysofdevops, aws-iam-policies, tws

---

Welcome to Day 38 of your cloud journey! You've come a long way, and it’s inspiring to see your dedication. Don’t let any setbacks break your consistency—each day brings you closer to becoming a cloud expert. Today, we’re diving into Amazon Web Services (AWS) fundamentals, focusing on IAM (Identity and Access Management) and creating hands-on tasks to apply your learning.

---

### What is AWS?

**Amazon Web Services (AWS)** is a comprehensive cloud platform offering a range of services, from computing power to storage and databases. AWS is popular among developers, enterprises, and students alike because it provides a **free tier** for beginners. If you haven't signed up yet, consider creating a free AWS account to explore its tools and get hands-on experience!

**Learn More:** [AWS Documentation](https://aws.amazon.com/documentation)

---

### Understanding IAM (Identity and Access Management)

AWS **Identity and Access Management (IAM)** is crucial for controlling access to AWS resources securely. With IAM, you can:

* Centrally manage permissions and control which AWS resources users can access.
    
* Authenticate and authorize users, ensuring that only specific individuals or applications have the necessary permissions.
    

IAM is essential for creating secure AWS environments, especially when working in teams or managing sensitive data.

**Deep Dive into IAM:** [IAM Documentation](https://aws.amazon.com/iam/)

---

### Hands-On Tasks for Day 38

#### Task 1: Create an IAM User and Launch an EC2 Instance

1. **Create an IAM User**:
    
    * Go to the **IAM dashboard** in AWS.
        
    * Click on **Users** and create a new user with a username of your choice.
        
    * Assign the necessary permissions for **EC2 access** to this user.
        
    * Download or note the **Access Key ID** and **Secret Access Key** for this user to use later in your setup.
        
    * This permission you need to give for your user\_1:  
        
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Sid": "EC2BasicOperations",
                    "Effect": "Allow",
                    "Action": [
                        "ec2:Describe*",
                        "ec2:RunInstances",
                        "ec2:StartInstances",
                        "ec2:StopInstances",
                        "ec2:TerminateInstances",
                        "ec2:CreateTags",
                        "ec2:CreateKeyPair",
                        "ec2:DeleteKeyPair"
                    ],
                    "Resource": "*",
                    "Condition": {
                        "StringEquals": {
                            "aws:RequestedRegion": "ap-south-1"
                        }
                    }
                },
                {
                    "Sid": "SecurityGroupAndVolumes",
                    "Effect": "Allow",
                    "Action": [
                        "ec2:CreateSecurityGroup",
                        "ec2:DeleteSecurityGroup",
                        "ec2:AuthorizeSecurityGroup*",
                        "ec2:RevokeSecurityGroup*",
                        "ec2:CreateVolume",
                        "ec2:DeleteVolume",
                        "ec2:AttachVolume",
                        "ec2:DetachVolume"
                    ],
                    "Resource": "*",
                    "Condition": {
                        "StringEquals": {
                            "aws:RequestedRegion": "ap-south-1"
                        }
                    }
                },
                {
                    "Sid": "EC2Connect",
                    "Effect": "Allow",
                    "Action": [
                        "ec2-instance-connect:SendSSHPublicKey",
                        "ec2-instance-connect:SendSerialConsoleSSHPublicKey"
                    ],
                    "Resource": "arn:aws:ec2:ap-south-1:*:instance/*"
                }
            ]
        }
        ```
        
2. **Launch a Linux Instance**:
    
    * Log in as the newly created IAM user.
        
    * Open the **EC2 dashboard** and launch a Linux instance (e.g., Amazon Linux 2).
        
    * Choose the instance type and configure the necessary network settings.
        
3. **Install Jenkins and Docker Using a Shell Script**:
    
    * SSH into your new EC2 instance.
        
    * Use the following shell script to install **Jenkins** and **Docker** in one go:
        
        ```bash
        #!/bin/bash
        # Update packages
        sudo apt-get update
        
        # Install Docker
        sudo apt-get install -y docker.io
        
        # Install docker compose
        sudo apt-get install docker-compose-v2
        
        # Install java-17
        sudo apt install fontconfig openjdk-17-jre -y
        
        # Install Jenkins
        sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
          https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
        echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
          https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
          /etc/apt/sources.list.d/jenkins.list > /dev/null
        sudo apt-get update
        sudo apt-get install -y jenkins
        
        # It start automatic when sererv restart
        sudo systemctl enable jenkins
        sudo systemctl enable docker
        
        # Add all permission to user and jenkins
        sudo usermod -aG docker $USER 
        sudo usermod -aG docker jenkins  
        newgrp docker
        
        echo "Jenkins and Docker have been installed successfully!"
        ```
        
    * Save the script, make it executable, and run it:
        
        ```bash
        chmod +x install.sh
        ./install.sh
        ```
        
    * This script will update the instance, install Docker, and set up Jenkins. You should now have Jenkins and Docker running on your EC2 instance!
        

---

#### Task 2: Create a DevOps Team of Avengers

In this task, you’ll set up a team by creating IAM users with custom permissions for a **DevOps group**.

1. **Create DevOps Group**:
    
    * In the **IAM dashboard**, go to **Groups**.
        
    * Create a new group named **DevOps**.
        
    * Attach the necessary IAM policies to grant permissions related to DevOps tasks, such as EC2 management, S3 access, etc.
        
2. **Create Avengers Users**:
    
    * Go back to **Users** in IAM and create three users. Name them something fun, like **IronMan**, **Thor**, and **CaptainAmerica**.
        
    * When creating each user, add them to the **DevOps** group you created earlier.
        
    * Ensure that each user has programmatic access by downloading their **Access Key ID** and **Secret Access Key**.
        
3. **Verify Permissions**:
    
    * To ensure your setup is correct, log in as one of the users and try launching an EC2 instance or accessing S3. This will confirm that the permissions assigned to the **DevOps** group are working as intended.
        

---

### Key Takeaways

* **AWS IAM** is vital for securely managing users and access to AWS resources, helping you build secure cloud infrastructures.
    
* **Hands-on tasks** provide a practical way to understand IAM policies, user roles, and EC2 instance management, essential skills for cloud-based DevOps.
    
* Keep experimenting with IAM policies to gain more control over permissions and ensure your AWS environments are secure and organized.
    

With today’s tasks, you’ve learned the basics of IAM and practiced creating users, groups, and assigning permissions. Each task brings you closer to mastering cloud management on AWS! ☁