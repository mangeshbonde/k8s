# 🚀 Kubernetes Cluster Setup on EC2 using Kind

This project demonstrates how to set up a Kubernetes cluster on an EC2 instance using Docker and Kind, and deploy an application on it.

---

## 📌 Prerequisites

* AWS EC2 Instance (Ubuntu recommended)
* SSH access to the instance
* Basic knowledge of Linux commands

---

## 🔐 Step 1: Connect to EC2 Instance

```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

---

## ⚙️ Step 2: Install Required Tools

### Create installation script

```bash
vim install.sh
```

Paste the content of your `install.sh` file.

---

### Change permission

```bash
chmod 777 install.sh
```

---

### Run the script

```bash
./install.sh
```

---

## ✅ Step 3: Verify Installation

Check if all tools are installed successfully:

```bash
docker --version
kubectl version
kind version
```

If versions are displayed, installation is successful.

---
## 🐳 Fix Docker Permission Issue for KIND

If you see an error like:

permission denied while trying to connect to the docker API


Follow these steps:

---

### 1️⃣ Add user to Docker group

```bash
sudo usermod -aG docker ubuntu

You are logged in as ubuntu, so use that instead of $USER.

2️⃣ Apply group changes ⚠️ (VERY IMPORTANT)

Run:

newgrp docker

OR

Logout and login again (recommended)

3️⃣ Test Docker access (this MUST work)
docker ps

✅ If it works → You’re ready to use KIND
❌ If not → Repeat steps or check Docker service


---

## 📁 Step 4: Create Kind Cluster Configuration

```bash
mkdir kind-cluster
cd kind-cluster
vim kind-config.yaml
```

Paste your `kind-config.yaml` content.

---

## ☸️ Step 5: Create Kubernetes Cluster

```bash
kind create cluster --name=tws-cluster --config=kind-config.yaml
```

---

## 🔍 Step 6: Verify Cluster Status

```bash
kubectl cluster-info --context kind-tws-cluster
```

---

### Check Nodes

```bash
kubectl get nodes
```

If nodes are in `Ready` state, your cluster is successfully created.

---

## 🚀 Step 7: Deploy Application

Create a deployment file:

```bash
vim deployment.yaml
```

Paste your Kubernetes deployment configuration.

---

### Apply Deployment

```bash
kubectl apply -f deployment.yaml
```

---

## 🎯 Result

* Kubernetes cluster is up and running using Kind
* Application is deployed successfully
* Ready for DevOps / Cloud practice

---
## Create ingress Controller for Nginx
* simply copy this link and paste it in EC2 in /home/ubuntu  or /home/ec2-user
```bash
kubectl apply -f https://kind.sigs.k8s.io/examples/ingress/deploy-ingress-nginx.yaml
```
* After that check namespace by using :
```bash
kubectl get ns
```

* You can see namespace i.e  ingress-nginx

## 💡 Notes

* Ensure ports (80/443) are open in EC2 Security Group if exposing apps
* Use `kubectl get pods` to monitor application status
* Use `kubectl logs <pod-name>` for debugging

---

## 🧠 Learning Outcome

* EC2 setup and SSH access
* Docker & Kubernetes installation
* Kind cluster creation
* Application deployment on Kubernetes

---

## 📌 Author

DevOps Learning Project 🚀


