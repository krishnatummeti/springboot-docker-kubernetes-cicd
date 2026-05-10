# Springboot - Docker- Kubernetes- CICD

## 📌 Project Overview
This repository contains a fully automated CI/CD pipeline built with **Jenkins** to deploy the **Spring Petclinic** application to a **Kubernetes** cluster. The pipeline handles everything from fetching the source code and building the application via Maven, to containerizing the artifact with Docker and deploying it to a live Kubernetes environment.

## 🏗️ Architecture & Workflow
1. **Source Code Management:** Code is pulled from GitHub.
2. **Continuous Integration (Build):** Maven compiles the code, runs tests, and packages the application.
3. **Containerization:** A Docker image is built using the Maven artifact.
4. **Registry Push:** The Docker image is pushed to Docker Hub securely.
5. **Continuous Deployment:** Kubernetes manifests (`deploymentservice.yaml`) are applied to deploy the new image to the cluster.

## 🛠️ Technology Stack
* **CI/CD:** Jenkins (Declarative Pipeline)
* **Containerization:** Docker, Docker Hub
* **Orchestration:** Kubernetes
* **Build Tool:** Maven
* **Version Control:** Git & GitHub

## 📋 Prerequisites
To replicate this pipeline, you will need:
* A running Jenkins server with the following plugins installed:
  * Docker Pipeline
  * Kubernetes CLI Plugin
  * Git Plugin
* A configured Kubernetes cluster (e.g., Minikube, Kubeadm, or managed cloud K8s).
* A Docker Hub account.
* Configured Jenkins Credentials:
  * `docker-hub`: Username and Password for Docker Hub.
  * `k8s-config`: Kubernetes `kubeconfig` file uploaded as a Secret File in Jenkins.

## 🚀 Pipeline Stages
The `Jenkinsfile` in this repository executes the following stages:

* `Build Maven`: Checks out the main branch and runs `mvn clean install`.
* `Build a Docker Image`: Builds the Docker image tagging it as `tummetikrishna/spring-petclinic`.
* `Push to Docker Hub`: Authenticates with Docker Hub and pushes the latest image.
* `Deploy to Kubernetes`: Connects to the Kubernetes cluster API and applies the deployment and service configurations.

## 📂 Project Structure
```text
.
├── Jenkinsfile              # Declarative Jenkins pipeline script
├── Dockerfile               # Instructions to build the application image
├── deploymentservice.yaml   # Kubernetes Deployment and Service definitions
└── README.md                # Project documentation
