---
title: "Day 68 - Scaling with Terraform 🚀"
datePublished: Sun Dec 15 2024 11:29:48 GMT+0000 (Coordinated Universal Time)
cuid: cm4pixh16000209kygd5aev6a
slug: day-68-scaling-with-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734262042272/eab5f0e8-1fe0-4005-b1da-7f34c33018eb.webp
tags: scaling, aws, terraform

---

Scaling infrastructure is a critical aspect of modern cloud-based application management. Today, we’ll focus on *what scaling is*, *how Terraform simplifies the process*, and *why it is a crucial skill for cloud developers*. By following the hands-on tasks provided, you’ll gain practical experience in setting up and testing scaling mechanisms using Terraform.

---

### **What is Scaling?**

Scaling involves dynamically adding or removing resources to meet the changing demands of your application. This ensures optimal performance during peak times and cost savings during low-usage periods.

There are two main types of scaling:

1. **Vertical Scaling:** Increasing the capacity of a single resource (e.g., upgrading to a larger EC2 instance).
    
2. **Horizontal Scaling:** Adding or removing multiple instances of a resource (e.g., adding more EC2 instances).
    

Terraform provides a declarative syntax to define scaling policies, enabling you to efficiently manage your infrastructure without manual intervention.

---

### **Why is Scaling Important?**

1. **Cost Optimization:** Avoid over-provisioning resources by scaling down during low-traffic periods.
    
2. **Performance Management:** Prevent downtime and maintain optimal performance by scaling up during high demand.
    
3. **Automation:** Minimize manual intervention with automated scaling, saving time and effort.
    

---

### **How to Scale Infrastructure with Terraform**

Terraform simplifies the creation and management of scaling setups using declarative configurations. Today, we’ll focus on setting up an **Auto Scaling Group (ASG)** for EC2 instances. An ASG ensures that your application dynamically adjusts to traffic loads by launching or terminating EC2 instances as needed.

---

### **Hands-On Tasks**

#### **Task 1: Create an Auto Scaling Group**

An Auto Scaling Group (ASG) automatically manages the number of EC2 instances based on predefined conditions. Follow these steps:

1. **Define a Launch Configuration:** Add the following code snippet in your [`main.tf`](http://main.tf) file. This defines the EC2 instance configuration, including the AMI, instance type, and user data script.
    
    ```xml
    resource "aws_launch_configuration" "web_server_as" {
      image_id        = "ami-005f9685cb30f234b"
      instance_type   = "t2.micro"
      security_groups = [aws_security_group.web_server.name]
    
      user_data = <<-EOF
                  #!/bin/bash
                  echo "<html><body><h1>You're doing really Great</h1></body></html>" > index.html
                  nohup python -m SimpleHTTPServer 80 &
                  EOF
    }
    ```
    
2. **Set Up the Auto Scaling Group:** This configuration specifies the desired capacity, minimum and maximum number of instances, and the load balancer integration.
    
    ```xml
    resource "aws_autoscaling_group" "web_server_asg" {
      name                 = "web-server-asg"
      launch_configuration = aws_launch_configuration.web_server_as.name
      min_size             = 1
      max_size             = 3
      desired_capacity     = 2
      health_check_type    = "EC2"
      load_balancers       = [aws_elb.web_server_lb.name]
      vpc_zone_identifier  = [aws_subnet.public_subnet_1a.id, aws_subnet.public_subnet_1b.id]
    }
    ```
    
3. **Apply the Changes:** Run the following command to provision the infrastructure:
    
    ```bash
    terraform apply
    ```
    

---

#### **Task 2: Test Scaling**

Once your Auto Scaling Group is set up, it's time to test the scaling functionality.

1. **Access the AWS Management Console:** Navigate to the **Auto Scaling Groups** section in the AWS Management Console.
    
2. **Increase Desired Capacity:**
    
    * Select your Auto Scaling Group.
        
    * Click on the "Edit" button.
        
    * Increase the **Desired Capacity** to `3`.
        
    * Save the changes and wait a few minutes.
        
3. **Verify Scaling:**
    
    * Go to the **EC2 Instances** section and confirm that new instances have been launched.
        
    * Ensure they match the settings specified in your Launch Configuration.
        
4. **Reduce Desired Capacity:**
    
    * Decrease the **Desired Capacity** back to `1`.
        
    * Wait for Terraform to terminate the extra instances.
        
5. **Validate Results:**
    
    * Return to the EC2 Instances section and confirm that only one instance is running.
        

---

### **Practical Insights**

* **Dynamic Scaling:** The ASG dynamically adjusts the number of instances based on the `desired_capacity`. For real-world scenarios, you can integrate **CloudWatch Alarms** to automate scaling decisions based on CPU utilization or other metrics.
    
* **Cost Control:** By setting a `min_size` and `max_size`, you can ensure your infrastructure doesn’t exceed budget constraints.
    
* **Error Handling:** If instances fail to launch or terminate, AWS provides detailed logs for debugging.
    

---

### **Conclusion**

Scaling infrastructure with Terraform is a game-changer for managing dynamic workloads. By understanding the concepts and following the hands-on tasks outlined above, you’ll be equipped to scale your applications efficiently and cost-effectively. Keep exploring Terraform’s capabilities to automate and optimize other aspects of your cloud infrastructure.

**What’s Next?** Tomorrow, we’ll explore integrating CloudWatch Alarms with your Auto Scaling Groups for automated scaling decisions. Stay tuned! 🌟