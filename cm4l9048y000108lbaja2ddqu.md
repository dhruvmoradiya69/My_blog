---
title: "Day 65: Working with Terraform Resources 🚀"
datePublished: Thu Dec 12 2024 11:40:51 GMT+0000 (Coordinated Universal Time)
cuid: cm4l9048y000108lbaja2ddqu
slug: day-65-working-with-terraform-resources
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734003361892/5a32e676-f22f-494a-8f0d-70a97761e31a.webp
tags: aws, devops, terraform

---

Welcome to Day 65 of your Terraform journey! Yesterday, we explored how to create a Terraform script using blocks and resources. Today, we’re diving deeper into **Terraform resources**, understanding what they are, how they work, and why they’re essential in Infrastructure as Code (IaC).

This hands-on tutorial will cover the following:

* What Terraform resources are and their significance.
    
* Step-by-step tasks to create essential infrastructure components: a security group and an EC2 instance.
    
* How to access your deployed resources.
    

Let’s get started!

---

## Understanding Terraform Resources

### What are Terraform Resources?

In Terraform, a **resource** represents a component of your infrastructure. This could be:

* Physical servers
    
* Virtual machines
    
* DNS records
    
* Storage buckets (e.g., AWS S3)
    

Each resource has attributes that define its **properties** and **behavior**. For instance, the attributes of a virtual machine could include its size, location, and operating system. Similarly, a DNS record's attributes might include its domain name and IP address.

### Why Use Terraform Resources?

Terraform resources allow you to define, provision, and manage your infrastructure declaratively. Instead of manually setting up resources in cloud provider dashboards, you can:

1. **Automate Deployments**: Write reusable configurations to deploy resources consistently.
    
2. **Track Changes**: Easily manage updates and revisions to your infrastructure.
    
3. **Collaborate**: Share configurations across teams for improved collaboration.
    

### How to Define a Terraform Resource?

In Terraform, resources are defined using the `resource` block. Each resource block specifies:

1. **Resource Type**: The type of resource to create, such as `aws_instance` or `aws_security_group`.
    
2. **Name**: A unique identifier for the resource.
    
3. **Attributes**: Specific properties for the resource, such as `ami` for an EC2 instance or `from_port` for a security group.
    

Here’s a generic structure:

```xml
resource "<resource_type>" "<resource_name>" {
  # Attributes defining the resource properties
}
```

---

## Hands-On Tasks

To reinforce the concepts, let’s build an AWS infrastructure. You’ll create:

1. A security group to allow HTTP traffic.
    
2. An EC2 instance with a simple website.
    

### **Task 1: Create a Security Group**

A security group acts as a virtual firewall for your EC2 instance. Here’s how to create one:

#### Steps:

1. Open your [`main.tf`](http://main.tf) file and add the following code:
    
    ```xml
    resource "aws_security_group" "web_server" {
      name_prefix = "web-server-sg"
    
      ingress {
        from_port   = 80
        to_port     = 80
        protocol    = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
      }
    }
    ```
    
    * **Explanation**:
        
        * `name_prefix`: Creates a security group name with the prefix `web-server-sg`.
            
        * `ingress`: Configures inbound traffic to allow HTTP (port 80) from any IP (`0.0.0.0/0`).
            
        * `protocol`: Specifies `tcp`, the transport protocol for HTTP.
            
2. Initialize the project:
    
    ```bash
    terraform init
    ```
    
3. Apply the configuration:
    
    ```bash
    terraform apply
    ```
    
    Once applied, Terraform creates a security group that permits HTTP traffic.
    

---

### **Task 2: Create an EC2 Instance**

Now that the security group is ready, let’s deploy an EC2 instance. This instance will host a simple website.

#### Steps:

1. Add the following code to your [`main.tf`](http://main.tf) file:
    
    ```xml
    resource "aws_instance" "web_server" {
      ami           = "ami-0557a15b87f6559cf"
      instance_type = "t2.micro"
      key_name      = "my-key-pair"
      security_groups = [
        aws_security_group.web_server.name
      ]
    
      user_data = <<-EOF
        #!/bin/bash
        echo "<html><body><h1>Welcome to my website!</h1></body></html>" > index.html
        nohup python -m SimpleHTTPServer 80 &
      EOF
    }
    ```
    
    * **Explanation**:
        
        * `ami`: The Amazon Machine Image (AMI) to use for the instance. Replace it with a valid AMI for your region.
            
        * `instance_type`: Specifies the EC2 instance type. `t2.micro` is free-tier eligible.
            
        * `key_name`: The SSH key pair for accessing the instance. Replace this with your key pair.
            
        * `security_groups`: Attaches the previously created security group.
            
        * `user_data`: Configures the instance to serve a simple HTML website.
            
2. Apply the configuration:
    
    ```bash
    terraform apply
    ```
    
    Once applied, Terraform will provision the EC2 instance and automatically execute the startup script to host a website.
    

---

### **Task 3: Access Your Website**

After deployment, retrieve the public IP of the EC2 instance:

1. Run:
    
    ```bash
    terraform output
    ```
    
    Or find the instance’s public IP in the AWS Management Console.
    
2. Open the IP address in your browser. You should see:
    
    ```xml
    Welcome to my website!
    ```
    

---

## Wrapping Up

Today, you’ve successfully deployed critical AWS infrastructure using Terraform. Here’s what we covered:

1. **Understanding Resources**: Resources are foundational to Terraform’s infrastructure-as-code model.
    
2. **Creating a Security Group**: Configured inbound HTTP traffic for your EC2 instance.
    
3. **Deploying an EC2 Instance**: Launched a virtual machine hosting a simple web page.
    

By automating these tasks with Terraform, you’ve taken a big step toward efficient and scalable cloud management. Repeat these steps with different configurations to deepen your understanding!