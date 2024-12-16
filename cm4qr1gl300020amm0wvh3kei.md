---
title: "Day 69 - Mastering Meta-Arguments in Terraform: Count and For_Each"
datePublished: Mon Dec 16 2024 08:04:37 GMT+0000 (Coordinated Universal Time)
cuid: cm4qr1gl300020amm0wvh3kei
slug: day-69-mastering-meta-arguments-in-terraform-count-and-foreach
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734336220032/f286d75f-adb6-45ee-ac44-0a12630924c4.webp
tags: aws, terraform, terraformcount

---

Terraform is a powerful tool for creating and managing infrastructure as code (IaC). One of its most versatile features is **meta-arguments**, which are special arguments that modify the behavior of resource blocks. In this blog, we’ll dive into the **"what," "how," and "why"** of Terraform’s `count` and `for_each` meta-arguments, and guide you through hands-on tasks to put them into practice.

---

### **What Are Meta-Arguments?**

Meta-arguments are built-in features of the Terraform language that provide additional control over resource behavior. They enable dynamic configuration, allowing you to manage multiple instances of a resource efficiently without duplicating code.

Two commonly used meta-arguments are:

1. `count`: Allows you to define the number of resource instances to create.
    
2. `for_each`: Enables dynamic creation of resources based on a set or map of values, giving each instance unique characteristics.
    

---

### **How Do Meta-Arguments Work?**

#### **1\. The** `count` Meta-Argument

The `count` meta-argument specifies how many instances of a resource Terraform should create. Each instance is uniquely indexed, enabling you to manage them individually.

**Syntax:**

```xml
resource "resource_type" "resource_name" {
  count = <number> # Number of instances to create

  # Resource configuration here
}
```

**Example: Creating Multiple AWS EC2 Instances**

```xml
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "server" {
  count = 4
  
  ami           = "ami-08c40ec9ead489470"
  instance_type = "t2.micro"
  
  tags = {
    Name = "Server ${count.index}"
  }
}
```

**Explanation:**

* The `count` meta-argument creates four EC2 instances.
    
* Each instance gets a unique name (`Server 0`, `Server 1`, etc.) using the `count.index` property.
    

---

#### **2\. The** `for_each` Meta-Argument

The `for_each` meta-argument iterates over a set or map to create resources with unique configurations. It’s ideal when resources have different properties, as it ensures each instance corresponds to an item in the set or map.

**Syntax:**

```xml
resource "resource_type" "resource_name" {
  for_each = <set/map> # Iterates over each element in the set/map

  # Resource configuration here
}
```

**Example 1: Using a Set**

```xml
locals {
  ami_ids = toset(["ami-0b0dcb5067f052a63", "ami-08c40ec9ead489470"])
}

resource "aws_instance" "server" {
  for_each = local.ami_ids

  ami           = each.key
  instance_type = "t2.micro"
  
  tags = {
    Name = "Server ${each.key}"
  }
}
```

**Example 2: Using a Map**

```xml
locals {
  ami_ids = {
    "linux"  = "ami-0b0dcb5067f052a63",
    "ubuntu" = "ami-08c40ec9ead489470"
  }
}

resource "aws_instance" "server" {
  for_each = local.ami_ids

  ami           = each.value
  instance_type = "t2.micro"
  
  tags = {
    Name = "Server ${each.key}"
  }
}
```

**Explanation:**

* In the first example, `for_each` creates instances based on a set of AMI IDs.
    
* In the second example, a map is used to pair each instance with a specific AMI and a meaningful name (`linux`, `ubuntu`).
    

---

### **Why Use Meta-Arguments in Terraform?**

Meta-arguments simplify your Terraform configurations by:

1. **Reducing Code Duplication**: You don’t need to write repetitive resource blocks for similar resources.
    
2. **Improving Scalability**: Easily scale your infrastructure by updating the `count` or `for_each` values.
    
3. **Customizing Resources Dynamically**: Use `for_each` to assign unique attributes to each resource.
    
4. **Streamlining Updates**: Modify multiple resources simultaneously with minimal changes to your code.
    

---

### **Hands-On Task: Demonstrating Count and For\_Each**

#### **Task-01: Create Infrastructure with** `count`

1. Open your terminal and create a new directory for the project.
    
2. Create a file named [`main.tf`](http://main.tf) and add the following configuration:
    

```xml
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "server" {
  count = 4
  
  ami           = "ami-08c40ec9ead489470"
  instance_type = "t2.micro"
  
  tags = {
    Name = "Server ${count.index}"
  }
}
```

3. Run the commands:
    
    ```bash
    terraform init
    terraform apply
    ```
    
4. Verify that four EC2 instances are created in your AWS console.
    

---

#### **Task-02: Create Infrastructure with** `for_each`

1. Update [`main.tf`](http://main.tf) to include a set and a map for `for_each`:
    

```xml
locals {
  ami_ids = {
    "linux"  = "ami-0b0dcb5067f052a63",
    "ubuntu" = "ami-08c40ec9ead489470"
  }
}

resource "aws_instance" "server" {
  for_each = local.ami_ids

  ami           = each.value
  instance_type = "t2.micro"
  
  tags = {
    Name = "Server ${each.key}"
  }
}
```

2. Run the commands:
    
    ```bash
    terraform apply
    ```
    
3. Check your AWS console to see two EC2 instances with distinct tags (`linux` and `ubuntu`).
    

---

### **Best Practices for Using Meta-Arguments**

* **Use** `count` for Identical Resources: When all resources share the same configuration.
    
* **Use** `for_each` for Unique Resources: When resources require different properties.
    
* **Leverage Local Variables**: Use `locals` to store values like AMI IDs or instance types to keep your code clean.
    
* **Test and Validate**: Always test configurations in a non-production environment to ensure correctness.
    

---

### **Conclusion**

Meta-arguments like `count` and `for_each` are indispensable tools in Terraform, helping you write concise, scalable, and dynamic infrastructure code. By mastering these features, you can enhance your IaC workflows and manage complex infrastructures with ease.

### **Next Steps**

* Experiment with more complex resource configurations using `count` and `for_each`.
    
* Try combining `count` and `for_each` with conditional expressions to create even more dynamic setups.
    
* Explore additional meta-arguments, such as `depends_on` and `provider`, for advanced use cases.
    

Now that you’ve learned the "what," "how," and "why" of Terraform meta-arguments, it’s time to get your hands dirty. Open your editor, spin up some resources, and start building!