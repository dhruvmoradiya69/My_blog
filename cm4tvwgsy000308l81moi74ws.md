---
title: "Day 70 - Terraform Modules"
datePublished: Wed Dec 18 2024 12:44:01 GMT+0000 (Coordinated Universal Time)
cuid: cm4tvwgsy000308l81moi74ws
slug: day-70-terraform-modules
tags: aws, modules, terraform, trainwithshubham

---

### **What Are Terraform Modules?**

Terraform modules are the building blocks of your infrastructure, enabling you to group resources and manage them collectively. A module is essentially a directory containing `.tf` or `.tf.json` files that define the infrastructure for a specific purpose. Modules make your Terraform configurations more organized, reusable, and easier to maintain. They allow you to encapsulate resource definitions and reuse them across multiple projects or configurations.

Modules can also call other modules, referred to as **child modules**, creating a nested hierarchy of configurations. This modular structure simplifies complex setups by breaking them into smaller, more manageable pieces.

### **How Do Terraform Modules Work?**

To use a module, you typically define it in your Terraform configuration with a `module` block. This block references the location of the module (local, Terraform Registry, or a version control system) and passes input variables to customize its behavior. Modules can also include **outputs**, which expose values to be used by other parts of your configuration or modules.

For example, consider the `aws_instance` example provided. It shows how to create a reusable EC2 instance module. By defining the instance details and output variables in a single module, you can simply call this module whenever you need to create EC2 instances, instead of rewriting the same configuration repeatedly.

### **Why Use Terraform Modules?**

1. **Reusability:** Modules can be reused across different projects, saving time and effort.
    
2. **Simplified Management:** By grouping resources, you reduce clutter and make configurations more intuitive.
    
3. **Consistency:** Using modules ensures that your infrastructure follows standardized practices across teams.
    
4. **Scalability:** Modules can be called multiple times, making it easy to scale configurations.
    
5. **Collaboration:** Modular designs enhance team productivity by dividing responsibilities and enabling parallel development.
    

---

### **Task-01: Exploring Terraform Modules**

#### **1\. Different Types of Terraform Modules**

Terraform modules are categorized based on their scope and purpose:

1. **Root Module:**
    
    * The root module is the main configuration directory where Terraform runs. Every `.tf` file in this directory is part of the root module.
        
    * This module is where you define high-level configurations and call child modules.
        
    * Example: When you run `terraform init` or `terraform apply`, Terraform looks for configurations in the root module.
        
2. **Child Module:**
    
    * A child module is any module called by another module (including the root module).
        
    * It can reside locally or be fetched from remote sources like the Terraform Registry or GitHub.
        
    * Example: Creating an EC2 instance or setting up a VPC as separate reusable modules.
        
3. **Public Modules:**
    
    * These are pre-built modules available on the Terraform Registry for common use cases, such as creating AWS S3 buckets, EC2 instances, or Kubernetes clusters.
        
    * Example: `terraform-aws-modules/ec2-instance/aws`.
        
4. **Custom Modules:**
    
    * These are user-defined modules created for specific projects or organizational needs. They provide flexibility and customization not available in public modules.
        

---

#### **2\. Difference Between Root Module and Child Module**

| **Aspect** | **Root Module** | **Child Module** |
| --- | --- | --- |
| **Definition** | The main module where Terraform execution begins. | Any module called by the root or another module. |
| **Location** | Local directory where Terraform is run. | Can be local or fetched from a remote source. |
| **Purpose** | Orchestrates the overall infrastructure setup. | Handles specific parts of the infrastructure. |
| **Scope** | Typically broader, including high-level resources. | Narrower, focusing on a specific functionality. |
| **Dependency** | Independent, but can call child modules. | Dependent on being invoked by another module. |

---

#### **3\. Are Modules and Namespaces the Same?**

**No, modules and namespaces are not the same.**

Here’s why:

1. **Modules:**
    
    * Modules are logical groupings of resources and their configurations. They help manage and reuse infrastructure setups.
        
    * Example: A module for creating EC2 instances or VPCs.
        
2. **Namespaces:**
    
    * Namespaces are a concept used to organize and manage resource names uniquely, especially in cloud environments.
        
    * In Terraform, namespaces can be mimicked using prefixes or hierarchical names in resource definitions but are not a built-in feature.
        

**Justification for ‘No’:**

* Modules group resources for reusability and modularity, whereas namespaces are about separating resources for uniqueness and management.
    
* Modules focus on design and abstraction, while namespaces are more about resource naming and avoiding conflicts.
    

**Justification for ‘Yes’ (if necessary):**

* In some contexts, modules can be used to define namespaces implicitly by assigning unique names or tags to resources. However, this is a workaround rather than a direct equivalence.
    

---

### **Hands-On Task for Practice**

1. **Create a Root Module:**
    
    * Define a root module to manage high-level infrastructure.
        
    * Include a [`main.tf`](http://main.tf) file that calls two child modules: one for VPC creation and another for EC2 instances.
        
2. **Create a Child Module:**
    
    * Define a child module for EC2 instances with variables for AMI, instance type, and tags.
        
    * Test reusability by calling the same module twice to create two different sets of instances.
        
3. **Experiment with Reusability:**
    
    * Modify the EC2 child module to add support for instance monitoring or additional tags.
        
    * Call the updated module from your root module to verify the changes.
        
4. **Namespace Simulation:**
    
    * Use unique tags or prefixes in your child module resources to simulate namespace functionality.
        
    * Example: Add a `namespace` variable and prepend it to the resource names.
        

By completing these tasks, you will gain a deeper understanding of how Terraform modules work and how to leverage them effectively in real-world scenarios.