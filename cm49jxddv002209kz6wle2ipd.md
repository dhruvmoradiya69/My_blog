---
title: "Day 57: Hands-On with Ansible – From Setup to Execution"
datePublished: Wed Dec 04 2024 07:13:24 GMT+0000 (Coordinated Universal Time)
cuid: cm49jxddv002209kz6wle2ipd
slug: day-57-hands-on-with-ansible-from-setup-to-execution
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733296348044/eb5c965c-ecb5-47c9-ae5a-a2b0e472c2a7.webp
tags: aws, ansible, devops

---

Welcome to Day 57 of your journey! Today, we’ll explore **Ansible**, an essential tool for IT automation that simplifies the way infrastructure and applications are managed. Over the past few days, you've seen how Ansible makes complex tasks straightforward. This guide will walk you through the essentials of Ansible, from understanding what it is to setting it up, configuring servers, and running commands.

---

## **What is Ansible?**

Ansible is an open-source **automation tool** designed to simplify:

* **Configuration Management**: Maintain consistency across systems.
    
* **Application Deployment**: Automate application installations and updates.
    
* **Orchestration**: Coordinate tasks across multiple systems in an orderly manner.
    

### **Why Choose Ansible?**

* **Agentless**: No need to install additional software on target systems; it uses SSH.
    
* **Simple Syntax**: Uses YAML, making it accessible even for non-developers.
    
* **Repeatability**: Tasks are idempotent, meaning they won’t produce unintended changes when re-executed.
    

---

## **Setting Up Ansible with Servers**

Before automating tasks, you’ll need to install and configure Ansible on your control machine (the machine from which you’ll manage other servers).

### **Step 1: Install Ansible on Your Control Machine**

1. **Update System Packages**:  
    Run the following commands on your control machine (e.g., a Linux-based system):
    
    ```bash
    sudo apt-get update  
    sudo apt-get upgrade -y  
    ```
    
2. **Install Ansible**:  
    Use the package manager to install Ansible:
    
    ```bash
    sudo apt-get install ansible -y  
    ```
    
3. **Verify Installation**:  
    Confirm Ansible is installed by checking its version:
    
    ```bash
    ansible --version  
    ```
    

---

## **SSH Tutorial: Setting Up Passwordless Authentication**

Ansible uses **SSH** to communicate with remote servers. To automate processes efficiently, set up passwordless SSH between your control machine and the target servers.

### **Step 2: Configure Passwordless SSH**

1. **Generate an SSH Key**:  
    On your control machine, create an SSH key pair:
    
    ```bash
    ssh-keygen  
    ```
    
    Press Enter to accept the default file location and skip adding a passphrase.
    
2. **Copy the SSH Key to Target Servers**:  
    Send the public key to your remote server(s):
    
    ```bash
    ssh-copy-id user@target_server  
    ```
    
    Replace `user` with the username on the target server and `target_server` with its IP address or hostname.
    
3. **Test the Connection**:  
    Verify that you can log in without a password:
    
    ```bash
    ssh user@target_server  
    ```
    

---

## **Creating an Ansible Inventory**

Ansible’s inventory file defines the servers (hosts) it manages. It can be as simple as a text file listing server IPs or organized into groups for larger setups.

### **Step 3: Create the Inventory File**

1. **Navigate to the Ansible Directory**:  
    Typically located at `/etc/ansible`.
    
2. **Edit the Inventory File**:  
    Open the default inventory file using a text editor:
    
    ```bash
    sudo vim /etc/ansible/hosts  
    ```
    
3. **Add Your Hosts**:  
    List your target servers in the file. For example:
    
    ```ini
    [webservers]  
    192.168.1.10  
    192.168.1.11  
    
    [databases]  
    192.168.1.20  
    ```
    

---

## **Using Ansible Commands**

Ansible commands allow you to execute tasks directly or run playbooks for complex operations.

### **Step 4: Test Connectivity**

Use the `ping` module to test if Ansible can reach your target servers:

```bash
ansible all -m ping  
```

Expected output:

```json
192.168.1.10 | SUCCESS => {  
    "changed": false,  
    "ping": "pong"  
}  
```

### **Step 5: Execute Basic Commands**

1. **Run a Shell Command**:  
    To check disk space on all hosts:
    
    ```bash
    ansible all -m shell -a "df -h"  
    ```
    
2. **Gather System Information**:  
    Use the `setup` module to fetch system details:
    
    ```bash
    ansible all -m setup  
    ```
    

---

## **Video Tutorial**

To ensure you grasp the steps visually, watch this detailed video that walks through the process from setup to running commands.

> %[https://youtu.be/SGB7EdiP39E?si=DJ3eZssjsIGXQwf2] 

---

## **Key Takeaways**

* Ansible simplifies IT automation with its agentless approach and user-friendly syntax.
    
* Setting up Ansible is as simple as installing it on your control machine and configuring SSH access.
    
* The inventory file is the cornerstone of managing multiple servers effectively.
    
* With a few commands, you can start automating repetitive tasks and managing your infrastructure efficiently.
    

Ready to explore more? Tomorrow, we’ll dive into creating Ansible Playbooks to further streamline operations. Stay tuned!