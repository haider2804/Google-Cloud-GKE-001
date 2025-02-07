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
