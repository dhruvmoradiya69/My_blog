---
title: "Day 34 Working with Services in Kubernetes 🌐"
datePublished: Fri Nov 08 2024 14:52:03 GMT+0000 (Coordinated Universal Time)
cuid: cm38uv1i9000008l4ehh9edbs
slug: day-34-working-with-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731077446047/b8447e51-3768-43d7-9b1a-1b09cc362fac.png
tags: kubernetes, devops, services, load-balancer, 90daysofdevops, k8scluster, tws

---

You've made it to **Day 34** of your Kubernetes learning journey! Yesterday, you deployed an application in Kubernetes, and today, we’re taking things further by setting up **Services** to manage how our app can be accessed. Let's dive in!

---

### 🌟 What Are Services in Kubernetes?

In **Kubernetes (K8s)**, **Services** are objects that act like a bridge, providing stable network identities to Pods (the smallest deployable units in Kubernetes). They help your app receive traffic, regardless of Pod IP changes, and ensure seamless communication between Pods, Services, and even external clients.

> 🧠 **In Simple Terms:** Imagine Services as doors that let you reach your app without worrying about which room (Pod) it's in. Services manage this for you, so traffic always reaches the right place!

---

### 🔧 Hands-On Tasks: Setting Up Services for Your `todo-app`

Let's get practical! We’ll create and use three types of Kubernetes Services to access the `todo-app` deployed on **Day 32**:

---

#### Task 1: Create a Service for Your `todo-app` Deployment 🚪

* here the project link
    
    ```bash
    git clone https://github.com/LondheShubham153/django-todo-cicd.git
    ```
    

This Service will give your app a stable identity within the cluster.

1. **Define the Service:** Create a YAML file named `service.yml` with this basic setup:
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: todo-app-service
    spec:
      selector:
        app: todo-app
      ports:
        - protocol: TCP
          port: 80
          targetPort: 8080
    ```
    
2. **Apply the Service Definition:** Use the following command to apply the Service to your Kubernetes cluster (replace `<namespace-name>` with your actual namespace):
    
    ```yaml
    kubectl apply -f service.yml -n <namespace-name>
    ```
    
3. **Verify the Service:** Check if your Service is working by accessing the `todo-app` using the Service's IP and port:
    
    ```yaml
    kubectl get svc -n <namespace-name>
    ```
    

---

#### Task 2: Create a ClusterIP Service for Internal Access 🔄

**ClusterIP** is the default Service type that only allows access within the cluster.

1. **Define the ClusterIP Service:** Create a YAML file named `cluster-ip-service.yml`:
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: todo-app-clusterip-service
    spec:
      type: ClusterIP
      selector:
        app: todo-app
      ports:
        - protocol: TCP
          port: 80
          targetPort: 8080
    ```
    
2. **Apply the ClusterIP Service Definition:**
    
    ```bash
    kubectl apply -f cluster-ip-service.yml -n <namespace-name>
    ```
    
3. **Verify the ClusterIP Service:** Access the `todo-app` from another Pod within the cluster. You can use the Pod’s terminal to confirm internal access:
    
    ```bash
    kubectl exec -it <pod-name> -n <namespace-name> -- curl todo-app-clusterip-service
    ```
    

---

#### Task 3: Create a LoadBalancer Service for External Access 🌍

A **LoadBalancer** Service allows your app to be accessed from outside the cluster.

1. **Define the LoadBalancer Service:** Create a YAML file named `load-balancer-service.yml`:
    
    ```yaml
    yamlCopy codeapiVersion: v1
    kind: Service
    metadata:
      name: todo-app-loadbalancer-service
    spec:
      type: LoadBalancer
      selector:
        app: todo-app
      ports:
        - protocol: TCP
          port: 80
          targetPort: 8080
    ```
    
2. **Apply the LoadBalancer Service Definition:**
    
    ```yaml
    kubectl apply -f load-balancer-service.yml -n <namespace-name>
    ```
    
3. **Verify the LoadBalancer Service:** Once the LoadBalancer is set up, access the `todo-app` from outside the cluster using the external IP provided:
    
    ```yaml
    kubectl get svc -n <namespace-name>
    ```
    

> 🚀 **Note:** LoadBalancer might not work on Minikube, as it's designed for cloud environments like AWS or GCP. In Minikube, you can use the `minikube service` command to access LoadBalancer Services.

---

### 📝 Summary

Here's what we've covered:

* **Kubernetes Services** provide stable access to your app within and outside the cluster.
    
* We created three types of Services for your `todo-app`:
    
    * **Standard Service** for basic access.
        
    * **ClusterIP Service** for internal access only.
        
    * **LoadBalancer Service** for external access.
        

### 👏 Congratulations on Completing Day 34!

You’re becoming a Kubernetes pro! Keep practicing and exploring more about Services in Kubernetes. The more you work with these concepts, the more confident you'll become.