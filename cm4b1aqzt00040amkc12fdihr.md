---
title: "Day 58: Ansible Playbooks"
datePublished: Thu Dec 05 2024 08:07:28 GMT+0000 (Coordinated Universal Time)
cuid: cm4b1aqzt00040amkc12fdihr
slug: day-58-ansible-playbooks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733386014418/9dc0cd1a-4e7e-496c-9a6b-eea7c052d01d.webp
tags: linux, aws, devops, ansible-playbook

---

Ansible is a powerful IT automation tool that simplifies tasks such as configuration management, application deployment, and orchestration. Central to its functionality is the *playbook*—a structured way to define tasks, manage configurations, and execute actions across multiple servers.

In this blog, we’ll dive deep into **what Ansible playbooks are**, **how to write them effectively**, and **the best practices to follow**. Additionally, we’ll include practical hands-on tasks to reinforce learning.

---

## **What is an Ansible Playbook?**

An Ansible playbook is essentially a YAML file that describes a series of tasks to be executed on a group of hosts. Think of playbooks as instruction manuals that dictate how servers should be configured or actions performed.

Playbooks are:

1. **Human-readable**: Written in YAML syntax.
    
2. **Reusable and modular**: Can be broken down into roles and tasks for better organization.
    
3. **Declarative**: You specify the desired state, and Ansible ensures the system matches it.
    

---

## **How to Write Ansible Playbooks**

To write a playbook, you need:

* **YAML syntax knowledge**: YAML (Yet Another Markup Language) is simple but indentation-sensitive.
    
* **An understanding of modules**: Modules are prebuilt functions (like creating files, users, or installing software).
    
* **Inventory file**: A list of hosts (servers) the playbook targets.
    

Here’s the basic structure of a playbook:

```yaml
---
- name: Name of the playbook (describes its purpose)
  hosts: target_group_or_hosts  # Can be 'all', a specific host, or a group
  become: true  # Use elevated privileges
  tasks:
    - name: Description of the task
      module_name:
        parameter1: value1
        parameter2: value2
```

---

### **Task 1: Practical Hands-On Examples**

#### **1\. Write an Ansible Playbook to Create a File on a Remote Server**

Here’s how you can create a file using the `file` module:

```yaml
---
- name: Create a file on a remote server
  hosts: all
  become: true

  tasks:
    - name: Create a file named 'example.txt'
      file:
        path: /tmp/example.txt  # Path to the file
        state: touch           # 'touch' ensures the file exists
        owner: root            # File owner
        group: root            # File group
        mode: '0644'           # Permissions
```

Run the playbook using:

```bash
ansible-playbook create_file.yml -i inventory_file
```

---

#### **2\. Write an Ansible Playbook to Create a New User**

To create a new user, you can use the `user` module:

```yaml
---
- name: Create a new user
  hosts: all
  become: true

  tasks:
    - name: Add a user named 'new_user'
      user:
        name: new_user         # Username
        state: present         # Ensure the user exists
        uid: 1050              # Optional: Specify user ID
        home: /home/new_user   # User's home directory
        shell: /bin/bash       # Default shell
```

Run the playbook using:

```bash
ansible-playbook create_user.yml -i inventory_file
```

---

#### **3\. Write an Ansible Playbook to Install Docker on a Group of Servers**

The following playbook installs Docker on multiple servers using the `yum` module for Red Hat-based distributions:

```yaml
---
- name: Install Docker on servers
  hosts: docker_hosts
  become: true

  tasks:
    - name: Install prerequisites
      yum:
        name: "{{ item }}"
        state: present
      with_items:
        - yum-utils
        - device-mapper-persistent-data
        - lvm2

    - name: Add Docker repository
      yum_repository:
        name: docker
        description: Docker Repository
        baseurl: https://download.docker.com/linux/centos/docker-ce.repo
        gpgcheck: yes
        enabled: yes

    - name: Install Docker
      yum:
        name: docker-ce
        state: latest

    - name: Start and enable Docker service
      service:
        name: docker
        state: started
        enabled: true
```

Run the playbook using:

```bash
ansible-playbook install_docker.yml -i inventory_file
```

---

### **Task 2: Best Practices for Writing Ansible Playbooks**

To make your playbooks efficient, scalable, and maintainable, follow these best practices:

#### **1\. Use Descriptive Names**

Every play and task should have a clear, human-readable name. This helps in debugging and understanding the purpose of the playbook.

#### **2\. Group Hosts by Roles**

Use the inventory file to organize servers by roles (e.g., `web_servers`, `db_servers`). This ensures targeted execution and easier management.

#### **3\. Keep Variables Organized**

Store variables in separate files for reusability. Use the `vars_files` keyword to include them:

```yaml
vars_files:
  - vars/main.yml
```

#### **4\. Break Playbooks into Roles**

Use the `roles` feature to modularize tasks. A role typically contains:

* `tasks`: Tasks to execute.
    
* `handlers`: Actions triggered by tasks (e.g., restarting a service).
    
* `vars`: Role-specific variables.
    
* `files`: Static files needed for tasks.
    

Roles ensure that playbooks are reusable and easier to debug.

#### **5\. Use Handlers for Idempotency**

Handlers are used to perform an action only when triggered. For example, restarting a service after configuration changes:

```yaml
tasks:
  - name: Update configuration file
    copy:
      src: new_config.conf
      dest: /etc/app/config.conf
    notify: Restart app service

handlers:
  - name: Restart app service
    service:
      name: app
      state: restarted
```

#### **6\. Test Playbooks**

Use testing tools like `ansible-lint` and `molecule` to validate syntax and ensure functionality.

#### **7\. Use Version Control**

Store your playbooks in version control systems (e.g., Git) for collaboration and versioning.

#### **8\. Document Everything**

Include comments and README files with your playbooks to explain their purpose and usage.

---

### **Conclusion**

Ansible playbooks are a cornerstone of automation, enabling system administrators and DevOps engineers to manage infrastructure at scale. By mastering playbook syntax and adhering to best practices, you can create efficient, maintainable, and reusable automation scripts.

Whether it's creating files, adding users, or deploying complex systems like Docker, Ansible makes the process seamless. Start small, experiment with tasks, and gradually modularize your playbooks into roles for optimal scalability.

---

### **Additional Resources**

* Official Ansible Documentation: [docs.ansible.com](https://docs.ansible.com/)
    
* Video Tutorial: [Learn Ansible Playbooks](https://chatgpt.com/c/67515e0f-ccb8-8006-9121-aeb72fda3a88#)