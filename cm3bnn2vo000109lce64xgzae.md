---
title: "Day 36 Managing Persistent Volumes in Kubernetes 🚀"
datePublished: Sun Nov 10 2024 13:53:13 GMT+0000 (Coordinated Universal Time)
cuid: cm3bnn2vo000109lce64xgzae
slug: day-36-managing-persistent-volumes-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731246727199/a3249608-704a-4bc6-b3b5-4ff77dcee822.png
tags: kubernetes, devops, k8s, 90daysofdevops, volume, tws, persistentvolumes

---

### **Introduction**

Yesterday, you mastered ConfigMaps and Secrets in Kubernetes. Today, we’re diving deeper into Kubernetes storage with **Persistent Volumes (PV)** and **Persistent Volume Claims (PVC)**—essential components for managing data in Kubernetes deployments.

Persistent Volumes allow you to store data independently of the lifecycle of a pod, ensuring data remains available even if the pod is deleted or re-created. Let’s walk through how to set up and use Persistent Volumes with hands-on examples.

### **What are Persistent Volumes in Kubernetes?**

* **Persistent Volume (PV)**: A storage resource provisioned by an admin within the Kubernetes cluster. Think of it as a piece of disk storage available for any pod that requests it.
    
* **Persistent Volume Claim (PVC)**: A user request for storage, connecting pods with the PV. The PVC specifies the amount of storage and access mode, binding it to a specific node.
    

📖 For more in-depth information, check the official Kubernetes Persistent Volumes documentation.

---

## **Task 1: Adding a Persistent Volume to Your Todo App Deployment**

* here the link of repo: [https://github.com/LondheShubham153/node-todo-cicd.git](https://github.com/LondheShubham153/node-todo-cicd.git)
    

In this task, we’ll add a Persistent Volume to the Todo app to store data persistently.

### **Step-by-Step Instructions**

1. **Create a Persistent Volume (**`pv.yml`):
    
    * The Persistent Volume is set up using a file on the node itself. Here’s a template to create `pv.yml`:
        
        ```yaml
        apiVersion: v1
        kind: PersistentVolume
        metadata:
          name: pv-todo-app
        spec:
          capacity:
            storage: 1Gi
          accessModes:
            - ReadWriteOnce
          persistentVolumeReclaimPolicy: Retain
          hostPath:
            path: "/tmp/data"
        ```
        
    * **Explanation**:
        
        * **capacity.storage**: Allocates 1Gi of storage for the volume.
            
        * **accessModes**: The volume can be read from and written to by a single node (ReadWriteOnce).
            
        * **hostPath**: Specifies the path where data will be stored on the node.
            
2. **Create a Persistent Volume Claim (**`pvc.yml`):
    
    * A PVC allows the app to claim the storage from the PV. Use this template for `pvc.yml`:
        
        ```yaml
        apiVersion: v1
        kind: PersistentVolumeClaim
        metadata:
          name: pvc-todo-app
        spec:
          accessModes:
            - ReadWriteOnce
          resources:
            requests:
              storage: 500Mi
        ```
        
    * **Explanation**:
        
        * **accessModes**: Same as PV, allowing single-node access.
            
        * **requests.storage**: Specifies that the Todo app will use up to 500Mi of storage from the PV.
            
3. **Update** `deployment.yml` to Include the Persistent Volume Claim:
    
    * Add the PVC to the deployment file so the Todo app can access the Persistent Volume.
        
        ```yaml
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: todo-app-deployment
        spec:
          replicas: 1
          selector:
            matchLabels:
              app: todo-app
          template:
            metadata:
              labels:
                app: todo-app
            spec:
              containers:
                - name: todo-app
                  image: rishikeshops/todo-app
                  ports:
                    - containerPort: 8000
                  volumeMounts:
                    - name: todo-app-data
                      mountPath: /app
              volumes:
                - name: todo-app-data
                  persistentVolumeClaim:
                    claimName: pvc-todo-app
        ```
        
    * **Explanation**:
        
        * **volumeMounts**: Mounts the volume under `/app` in the container.
            
        * **volumes.persistentVolumeClaim**: Connects the volume to the PVC.
            
4. **Apply Your Files in Kubernetes**:
    
    * Apply each YAML file to create the PV, PVC, and updated deployment:
        
        ```bash
        kubectl apply -f pv.yml
        kubectl apply -f pvc.yml
        kubectl apply -f deployment.yml
        ```
        
5. **Verify the Persistent Volume in the Deployment**:
    
    * Check if the Persistent Volume is successfully added:
        
        ```bash
        kubectl get pods
        kubectl get pv
        ```
        

---

## **Task 2: Accessing Data in the Persistent Volume**

Once the Persistent Volume is connected, you can access and manage the data within the app.

1. **Connect to a Pod in the Deployment**:
    
    * Use the following command to enter the pod’s bash shell:
        
        ```yaml
        kubectl exec -it <pod-name> -- /bin/bash
        ```
        
2. **Verify Data Accessibility**:
    
    * Navigate to the mounted directory (`/app` in this case) and confirm you can access the data stored in the Persistent Volume.
        

---

### **Important Reminders**

* **Applying Files Separately**: In Kubernetes, each file (PV, PVC, Deployment) must be applied individually.
    
* **Commands Recap**:
    
    * To apply files: `kubectl apply -f <file-name>.yml`
        
    * To check pods: `kubectl get pods`
        
    * To check PVs: `kubectl get pv`
        
    * To connect to a pod: `kubectl exec -it <pod-name> -- /bin/bash`
        

---

### **Conclusion**

Persistent Volumes in Kubernetes provide a stable way to handle data storage in your applications. With this setup, your Todo app’s data will persist even if the pod restarts.

Keep up the great work on the #90DaysOfDevOps journey! 💪