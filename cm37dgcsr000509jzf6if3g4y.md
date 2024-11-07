---
title: "Day 33: Mastering Namespaces and Services in Kubernetes 🚀"
datePublished: Thu Nov 07 2024 13:56:58 GMT+0000 (Coordinated Universal Time)
cuid: cm37dgcsr000509jzf6if3g4y
slug: day-33-mastering-namespaces-and-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730987743842/56041332-9273-4c19-887f-2bf468c86882.png
tags: kubernetes, devops, 90daysofdevops, namespaces, k8scluster, tws

---

Hey Devs! 🎉 You've made great progress by updating your Deployment yesterday. Today, we’re diving deeper into the essential concepts of **Namespaces** and **Services** in Kubernetes. Let’s break down these topics and walk you through a hands-on task! 🛠️

---

## 🤔 What are Namespaces and Services in Kubernetes?

* **Namespaces**: Think of a Namespace as a unique environment within your cluster that allows you to organize and manage resources separately. This is like having multiple mini-clusters within your main cluster for better isolation and resource allocation.
    
* **Services**: These are essential for exposing your **Pods** and **Deployments** to the network, enabling communication both inside and outside the cluster. Services ensure that your applications are accessible and maintain consistent network traffic.
    

---

### Task 1: Create a Namespace for Your Deployment

Let’s create a Namespace and link your existing deployment to it:

1. **Create a Namespace**: Run the following command to create a new Namespace:
    
    ```bash
    kubectl create namespace <namespace-name>
    ```
    
    📝 *Example*:
    
    ```bash
    kubectl create namespace my-app-space
    ```
    
2. **Update** `deployment.yml`: Add the `namespace` field to your `deployment.yml` to specify where the deployment will reside.
    
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: todo-app
      labels:
        app: todo
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: todo
      template:
        metadata:
          labels:
            app: todo
        spec:
          containers:
          - name: todo
            image: rishikeshops/todo-app
            ports:
            - containerPort: 3000
    ```
    
3. **Apply the Deployment**: Deploy your updated `deployment.yml` using the command:
    
    ```bash
    kubectl apply -f deployment.yml -n <namespace-name>
    ```
    
    📝 *Example*:
    
    ```bash
    kubectl apply -f deployment.yml -n my-app-space
    ```
    
4. **Verify Your Namespace**: Ensure your Namespace has been created by running:
    
    ```bash
    kubectl get namespaces
    ```
    
    You should see your newly created Namespace listed.
    

---

### Task 2: Dive into Services, Load Balancing, and Networking

🔗 **Read the Kubernetes official documentation on Services** here. Learn how Services facilitate load balancing and expose your deployments to handle traffic smoothly. Here are a few key points to understand:

* **Types of Services**:
    
    * `ClusterIP`: Exposes the service on a cluster-internal IP.
        
    * `NodePort`: Exposes the service on each Node’s IP at a static port.
        
    * `LoadBalancer`: Creates an external load balancer in supported cloud environments.
        
    * `ExternalName`: Maps a service to a DNS name.
        
* **Networking in Kubernetes**: Kubernetes manages complex networking using a combination of internal and external mechanisms, enabling pods to communicate seamlessly.
    

---

## 🌈 Wrapping Up

These hands-on tasks will help you grasp how Namespaces enhance resource management and how Services ensure reliable networking for your applications. Go ahead and experiment with creating Namespaces and exploring the different types of Services in Kubernetes! 🚀

👋 See you tomorrow for more Kubernetes magic!