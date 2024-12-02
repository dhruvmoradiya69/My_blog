---
title: "Day 55: Understanding Configuration Management with Ansible"
datePublished: Mon Dec 02 2024 11:51:21 GMT+0000 (Coordinated Universal Time)
cuid: cm46yz3of000a09la9j2lg5lx
slug: day-55-understanding-configuration-management-with-ansible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733140099850/612ccb59-2845-4b19-9220-b6e6ec1533b4.webp
tags: aws, ansible, devops, 90daysofdevops, tws

---

Configuration management is a crucial part of modern IT operations, ensuring systems remain consistent and automated for efficient management. Today, we dive into **Ansible**, a powerful open-source tool for automation. By the end of this blog, you’ll learn **what Ansible is**, **how to install it**, and perform basic tasks like configuring nodes and testing connectivity.

## What is Ansible?

**Ansible** is an open-source automation tool that simplifies IT operations like:

1. **Configuration Management**: Maintaining consistency across servers by automating configurations.
    
2. **Application Deployment**: Quickly deploying apps across multiple servers with minimal manual effort.
    
3. **Orchestration**: Managing complex multi-service workflows.
    
4. **Provisioning**: Preparing the infrastructure for deployment.
    

### Why Use Ansible?

* **Agentless**: No need to install additional software on managed systems; uses SSH for communication.
    
* **Simple YAML Syntax**: Configuration files (playbooks) are written in easy-to-read YAML.
    
* **Scalable**: Efficiently handles hundreds or thousands of nodes.
    
* **Community Support**: Regular updates and extensive documentation.
    

Now, let’s dive into a practical walkthrough with **three tasks** to explore Ansible’s capabilities.

---

## **Task 01: Installing Ansible on AWS EC2 (Master Node)**

Ansible installation is straightforward. Here’s how to set it up on your **AWS EC2 Master Node**:

1. **Launch an EC2 Instance**
    
    * Use a Linux AMI, such as Ubuntu 20.04, for the master node.
        
    * Open port 22 for SSH access.
        
2. **Update the System**
    
    ```bash
    sudo apt-get update
    ```
    
3. **Add Ansible Repository**
    
    ```bash
    sudo apt-get-add-repository ppa:ansible/ansible
    ```
    
4. **Install Ansible**
    
    ```bash
    sudo apt-get update
    sudo apt-get install ansible -y
    ```
    
5. **Verify Installation**
    
    ```bash
    ansible --version
    ```
    
    This will confirm that Ansible is successfully installed.
    

---

## **Task 02: Understanding and Modifying the Hosts File**

The **hosts file** tells Ansible which nodes (servers) it will manage. Let’s configure it:

### Step 1: Edit the Hosts File

Ansible's default inventory file is located at:

```bash
sudo vim /etc/ansible/hosts
```

### Example Configuration:

```ini
[webservers]
192.168.1.10 ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private-key.pem

[databases]
192.168.1.20 ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private-key.pem
```

* **\[webservers\]**: Group name for related servers (e.g., web servers).
    
* **IP Addresses**: Replace with your actual node IPs.
    
* **Private Key**: Path to your private key for SSH access.
    

### Step 2: Test Inventory

Run the following command to verify:

```bash
ansible-inventory --list -y
```

This outputs the parsed inventory in YAML format, ensuring your setup is correct.

---

## **Task 03: Adding and Testing Additional EC2 Nodes**

In this task, you’ll set up two additional EC2 instances (nodes) and connect them to your Ansible master node.

### Step 1: Create Two EC2 Nodes

* Launch two new EC2 instances with the same **private key** used for the master node.
    
* Ensure they have SSH access enabled and use Ubuntu as the base OS.
    

### Step 2: Copy the Private Key to Master Server

There is no need to provide the path because both use the same AWS EC2 instance.

Move your private key file to the master node:

```bash
scp /path/to/node-key.pem ubuntu@<master-node-ip>:~/node-key.pem
```

### Step 3: Update Hosts File

Add the new EC2 instances to your `/etc/ansible/hosts` file under appropriate groups. Example:

```ini
[webservers]
<node1-private-ip> ansible_user=ubuntu ansible_ssh_private_key_file=~/node-key.pem

[databases]
<node2-private-ip> ansible_user=ubuntu ansible_ssh_private_key_file=~/node-key.pem
```

### Step 4: Test Connectivity with Ping

Run a ping command to test Ansible connectivity:

```bash
ansible all -m ping
```

Expected Output:

```yaml
<node-ip> | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

This confirms that Ansible can communicate with your nodes.

---

## SEO Tips for "Understanding Configuration Management with Ansible"

1. **Keywords**: Use target phrases like *Ansible tutorial*, *Ansible configuration management*, and *install Ansible AWS*.
    
2. **Headings**: Structure with H1, H2, and H3 tags for clarity and ranking.
    
3. **Internal Links**: Link to related posts about AWS, EC2, or automation tools.
    
4. **External Links**: Include trusted references to Ansible documentation.
    
5. **Meta Description**: Create a concise meta summary (e.g., *Learn Ansible configuration management with step-by-step tasks on AWS EC2.*).
    
6. **Alt Tags**: Add descriptive alt text for images (e.g., *Ansible hosts file example*).
    
7. **Readable URL**: Use a clear URL slug like `/ansible-configuration-management`.
    

---

## Conclusion

By following these steps, you’ve installed Ansible, configured a hosts file, and successfully set up communication with multiple nodes. Ansible’s simplicity and efficiency make it a must-have tool for IT automation.

Stay tuned for more advanced topics like writing Ansible Playbooks and scaling infrastructure with ease!