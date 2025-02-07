# Google-Cloud-GKE-001
A comprehensive demo project that shows how to deploy a containerized web application on Google Kubernetes Engine (GKE) with integrated node-level monitoring using Prometheus Node Exporter. This project covers GCP environment, GKE, Docker, Kubernetes YAML files, and DaemonSet.


# GKE-001

## Overview

**GKE-001** is a demonstration project that guides you through deploying a containerized web application on Google Kubernetes Engine (GKE) and setting up node-level monitoring using Prometheus Node Exporter. This project covers the entire process from setting up your Google Cloud environment to deploying your application and monitoring each node in your cluster.

**Key Features:**
- **GCP Environment Setup:** Create and configure a Google Cloud project with the required APIs.
- **GKE Cluster Creation:** Build a GKE cluster with multiple nodes.
- **Containerization:** Package a simple web application using Docker.
- **Kubernetes Deployment:** Deploy the application with Deployment and Service YAML files.
- **Node Monitoring:** Use a DaemonSet to run Prometheus Node Exporter on every node.
- **Version Control:** Organize and document the project on GitHub.

---

## Prerequisites

- **Google Cloud Platform Account:** With billing enabled and the Kubernetes Engine API activated.
- **Google Cloud SDK:** Installed locally or access to Cloud Shell.
- **Docker:** Installed locally for building container images.
- **Basic Knowledge:** Familiarity with Docker, Kubernetes, and Git.
- **GitHub Account:** For hosting the repository.

---

## Project Structure

```plaintext
GKE-001/
├── Dockerfile
├── deployment.yaml
├── service.yaml
├── node-exporter-daemonset.yaml
├── html/
│   └── index.html
└── README.md

**Step-by-Step Project Explanation
1. Google Cloud Environment Setup**
Project Creation:
A new GCP project (named HaiderTesting with project ID haidertesting) was created to serve as the workspace.

API Enablement:
The Kubernetes Engine API was enabled so that you can manage clusters using the Google Cloud Console or the gcloud CLI.

Billing:
Billing was confirmed to be active, ensuring resource provisioning without interruptions.

**2. Creating the GKE Cluster**
Cluster Creation Command:
A cluster named my-gke-cluster was created in the us-central1-c zone with 3 nodes. Because of regional quota limits, the disk size per node was reduced to 50GB:
            gcloud container clusters create my-gke-cluster \
                --zone us-central1-c \
                --num-nodes=3 \
                --disk-size=50
Verification:
The cluster’s nodes were checked with:
          kubectl get nodes

**3. Containerizing the Application**
Application Files:
A simple static web application was created. The html/index.html file contains a welcome message.

**Dockerfile:**
A Dockerfile was written to build an image using the Nginx base image. It copies the HTML files into Nginx's.

**Building & Pushing the Image:**
The Docker image is built and then pushed to Google Container Registry (GCR):

        docker build -t gcr.io/haidertesting/gke-demo-app:latest .
        gcloud auth configure-docker
        docker push gcr.io/haidertesting/gke-demo-app:latest

**4. Deploying the Application on GKE**
**Deployment YAML (deployment.yaml):**
Defines a Deployment to run 3 replicas of the containerized application.

**Service YAML (service.yaml):**
Exposes the Deployment externally via a LoadBalancer

Applying the YAML Files:
Deploy the application using:
        kubectl apply -f deployment.yaml
        kubectl apply -f service.yaml

Verification:
Check the status with:
        kubectl get pods
        kubectl get svc


**5. Setting Up Node-Level Monitoring**
DaemonSet for Node Exporter (node-exporter-daemonset.yaml):
A DaemonSet ensures that Prometheus Node Exporter runs on every node, collecting metrics such as CPU, memory, and disk usage.

**Deploying the DaemonSet:**
Apply the configuration with:
        kubectl apply -f node-exporter-daemonset.yaml

**Verification:**
Confirm that a Node Exporter pod is running on each node:
        kubectl get pods -n kube-system -l k8s-app=node-exporter
