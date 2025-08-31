# Full-Stack Application Deployment on Kubernetes (Minikube)

This repository demonstrates how to containerize and deploy a **Node.js application** with a **MongoDB database** to a **local Kubernetes cluster using Minikube**.  

The setup includes:
- Dockerized services for Node.js and MongoDB
- Kubernetes manifests organized with **Kustomize** for environment management
- Steps to test and access the application locally through Minikube
- Instructions to verify data in MongoDB after submitting entries through the UI

---

## Architecture Overview
NodeJS App <--> MongoDB
│ ▲
│ │
▼ │
Kubernetes Cluster (Minikube)
Deployment │ │ StatefulSet
(node-app) │ │ (mongo)
│ ▲
│ │
▼ │
Service
(Cluster IP/NodePort)


---

## Tech Stack

| Tool/Tech       | Purpose                                    |
|----------------|--------------------------------------------|
| **Minikube**   | Local Kubernetes cluster for testing        |
| **Docker**     | Containerization of services                |
| **Kustomize**  | Base and overlay Kubernetes configuration   |
| **kubectl**    | Kubernetes CLI for managing resources       |
| **MongoDB**    | Database backend                            |

---

## Repository Structure
├── app
├── Dockerfile # Docker image for Node.js application
├── docker-compose.yml # Optional for local Docker-only testing
├── kustomize/
│ ├── base/
│ │ ├── deployment.yaml
│ │ ├── service.yaml # Node.js app Service (NodePort)
│ │ └── kustomization.yaml
│ └── overlays/
└── README.md


---

## Step-by-Step Setup (Minikube)

### Prerequisites
Make sure you have the following installed:
- [Docker]
- [Kubectl]
- [Minikube]

---

Verify installations:
```bash
docker --version
kubectl version --client
minikube version

---

### Commands Used

`minikube start --driver=docker`
![alt text](image.png)

`kubectl get nodes`
![alt text](image-1.png)

`kubectl apply -k kustomize/base`
![alt text](image-2.png)

`kubectl get pods`
![alt text](image-3.png)

`kubectl get svc`
![alt text](image-4.png)

`minikube service node-app --url`
![alt text](image-5.png)

`kubectl exec -it mongo-55f94c9bbc-l9cr2 -- mongosh`
![alt text](image-6.png)

---

# Docker and Containers
1) Docker images
![alt text](image-12.png)

2) Docker containers
![alt text](image-13.png)

---

# commands inside mongodb
`show dbs`
`use devopsdb`

---

# Environment Variables
Variable	Description
NODE_ENV	development (default)
MONGO_URI	Connection string for MongoDB

Note: This setup is for local development only.

---

# Screenshots of Application UI:
1) Profile Tab
![alt text](image-7.png)

2) New Article Tab
![alt text](image-8.png)

3) Home Screen showing different entries
![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)

---

Author: Venkatesh Tuniki 

"I have setup the Kubernetes cluster using **Minikube**. I attempted to work using EKS - An aws managed kubernetes cluster, however I'm experincing some issues with account registration step with AWS personal account as my previous one was closed. Hence deployed the app and mongo containers using Minikube."

---