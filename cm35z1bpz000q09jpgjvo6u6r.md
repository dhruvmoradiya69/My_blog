---
title: "🚀 Day 32: Launch Your First Kubernetes Cluster with a Deployment"
datePublished: Wed Nov 06 2024 14:25:36 GMT+0000 (Coordinated Universal Time)
cuid: cm35z1bpz000q09jpgjvo6u6r
slug: day-32-launch-your-first-kubernetes-cluster-with-a-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730902926833/e627d1ba-a65a-4bce-b27e-a68757789fd2.png
tags: kubernetes, devops, 90daysofdevops, kubernetes-pods, tws

---

Congratulations on reaching Day 32 of your Kubernetes (K8s) learning journey! 🎉 Yesterday, you explored the basics of K8s on Day 31, and today, we’re diving into the **Deployment** feature. This post is for anyone looking to set up a simple Kubernetes deployment, even if you're not a developer!

Let’s break it down step-by-step so you can get hands-on experience. By the end of this guide, you’ll have deployed a sample "To-Do App" on a K8s cluster with auto-scaling and self-healing features!

---

## 🌟 What is a Deployment in Kubernetes?

In Kubernetes, a **Deployment** allows you to set up configurations for managing updates to Pods and ReplicaSets. A Deployment helps you manage the **desired state** of an application, scaling it up or down as needed. It also lets you use **auto-healing** to ensure that if any part of your app crashes, it automatically recovers!

With Deployments, you can:

* **Scale** applications up or down by creating or deleting replicas.
    
* **Auto-heal** crashed containers, maintaining app stability.
    
* **Update** your app by replacing old versions with new ones without downtime.
    

---

## 👷 Task 1: Deploy a Simple To-Do App Using Kubernetes Deployment

Let’s keep this simple and focus on just one task for today.

### 🔹 Step 1: Create a Deployment YAML File

To get started, we need a **deployment.yml** file that defines how to deploy the app. This file describes the app, including how many replicas (instances) to create, what container image to use, and other configurations for auto-scaling and auto-healing.

<mark>project app link</mark>

Here’s a sample deployment file you can use. Copy this into a new file named `deployment.yml` in your project folder.

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: todo
  template:
    metadata:
      labels:
        app: todo
    spec:
      containers:
        - name: todo-app
          image: your-docker-image-for-todo-app:latest  # replace this with your image
          ports:
            - containerPort: 80
          resources:
            limits:
              cpu: "500m"
              memory: "512Mi"
            requests:
              cpu: "200m"
              memory: "256Mi"
```

#### 📝 Explanation of Key Sections

* **apiVersion** and **kind**: Specifies this is a `Deployment` using API version `apps/v1`.
    
* **metadata**: Defines the name of the deployment (`todo-app`).
    
* **spec**:
    
    * **replicas**: Sets the number of app replicas. Here, we’re creating 3 instances to handle multiple requests.
        
    * **selector**: Matches labels for the app (in this case, `app: todo`).
        
    * **template**: Configures the app’s container image, port, and resource limits (e.g., CPU, memory).
        

### 🔹 Step 2: Deploy the App to Your K8s (Minikube) Cluster

Once you have your `deployment.yml` file ready, it’s time to deploy it to your Kubernetes cluster.

> **Note:** Make sure you have Minikube or another Kubernetes setup ready and running on your machine.

#### 🚀 Deploying the App

1. Open your terminal.
    
2. Navigate to the folder where `deployment.yml` is saved.
    
3. Run the following command:
    

```bash
kubectl apply -f deployment.yml
```

#### ✅ What This Command Does:

This command tells Kubernetes to read the `deployment.yml` file and create the defined resources in your cluster. After a moment, your app should be up and running on K8s with **auto-healing** and **auto-scaling**.

### 🔹 Step 3: Check Your Deployment Status

After deploying, you’ll want to confirm that everything is running as expected. Use these commands to monitor the deployment:

```bash
kubectl get deployments
kubectl get pods
```

* **kubectl get deployments**: Shows the status of the deployment (e.g., replicas running).
    
* **kubectl get pods**: Lists all active pods, which are the individual instances of your app.
    

---

## 🎉 Congratulations!

You’ve successfully deployed a sample "To-Do App" on Kubernetes with basic auto-scaling and auto-healing features! 🚀 With this hands-on task, you've taken a significant step forward in your Kubernetes journey.

### 💡 Key Takeaways:

* Kubernetes **Deployments** manage the state and scaling of your app.
    
* **Auto-scaling** lets K8s automatically handle traffic demands.
    
* **Auto-healing** keeps your app stable by recovering crashed pods.
    

Happy deploying, and keep up the fantastic learning!