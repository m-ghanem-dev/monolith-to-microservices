# Udagram Microservices Architecture

## Overview
This project demonstrates the transition from a monolithic application to a microservices-based architecture. It leverages Kubernetes (K8s) for container orchestration, a reverse proxy for routing, and CI/CD pipelines for automated deployments. The application consists of multiple services, including a frontend, backend services, and a reverse proxy.

It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

---

## Architecture Components

### 1. **Frontend**
- **Technology**: Angular
- **Description**: The frontend is a single-page application (SPA) that interacts with the backend services via REST APIs.
- **Deployment**: Packaged as a Docker container and deployed in Kubernetes.
- **Kubernetes Resources**:
  - `application-deployment.yaml`: Defines the deployment for the frontend.
  - `application-service.yaml`: Exposes the frontend as a service within the cluster.

### 2. **Backend Services**
#### a. **Feed Service**
- **Technology**: Node.js with Sequelize ORM
- **Description**: Handles operations related to user feeds, such as creating and retrieving feed items.
- **Deployment**: Packaged as a Docker container and deployed in Kubernetes.
- **Kubernetes Resources**:
  - `application-deployment.yaml`: Defines the deployment for the feed service.
  - `application-service.yaml`: Exposes the feed service within the cluster.
  - `configmap.yaml` and `secrets.yaml`: Store environment variables and sensitive data.

#### b. **User Service**
- **Technology**: Node.js with Sequelize ORM
- **Description**: Manages user authentication and profile data.
- **Deployment**: Packaged as a Docker container and deployed in Kubernetes.
- **Kubernetes Resources**:
  - `application-deployment.yaml`: Defines the deployment for the user service.
  - `application-service.yaml`: Exposes the user service within the cluster.
  - `configmap.yaml` and `secrets.yaml`: Store environment variables and sensitive data.

#### c. **Image Filtering Service**
- **Technology**: Python with Flask
- **Description**: Applies filters to images posted by users.
- **Deployment**: Packaged as a Docker container and deployed in Kubernetes.
- **Kubernetes Resources**:
  - `application-deployment.yaml`: Defines the deployment for the image filtering service.
  - `application-service.yaml`: Exposes the image filtering service within the cluster.
  - `configmap.yaml` and `secrets.yaml`: Store environment variables and sensitive data.

### 3. **Reverse Proxy**
- **Technology**: Nginx
- **Description**: Acts as a gateway to route requests to the appropriate backend services.
- **Deployment**: Packaged as a Docker container and deployed in Kubernetes.
- **Kubernetes Resources**:
  - `reverseproxy-deployment.yaml`: Defines the deployment for the reverse proxy.
  - `reverseproxy-service.yaml`: Exposes the reverse proxy to external traffic.

---

## Kubernetes (K8s) Overview
- **Cluster Management**: Kubernetes is used to manage the lifecycle of the application containers.
- **Key Features**:
  - **Deployments**: Ensure the desired state of the application is maintained.
  - **Services**: Enable communication between microservices and expose them to external traffic.
  - **ConfigMaps and Secrets**: Manage configuration and sensitive data securely.

---

## CI/CD Pipeline
- **Tool**: GitHub Actions
- **Description**: Automates the build, test, and deployment processes.
- **Pipeline Steps**:
  1. **Build**: Docker images are built for each service.
  2. **Test**: Unit and integration tests are executed.
  3. **Deploy**: Images are pushed to a container registry, and Kubernetes manifests are applied to the cluster.

---

## Horizontal Pod Autoscaler (HPA) and Metrics Service

This project leverages Kubernetes' Horizontal Pod Autoscaler (HPA) to ensure the application can scale dynamically based on resource usage. The HPA monitors CPU and memory usage and adjusts the number of pods to maintain optimal performance.

The metrics service is deployed to provide resource usage data to the HPA. It collects and exposes metrics from the application pods, enabling the HPA to make informed scaling decisions.

---

## How It Works
1. **Frontend**: The user interacts with the Angular frontend.
2. **Reverse Proxy**: Requests are routed through the Nginx reverse proxy.
3. **Backend Services**: The reverse proxy forwards requests to the appropriate backend service (Feed, User, or Image Filtering).
4. **Database**: Backend services interact with the database to fetch or store data.

---

## Folder Structure
- **udagram-feed/**: Contains the feed service code and Kubernetes manifests.
- **udagram-user/**: Contains the user service code and Kubernetes manifests.
- **udagram-frontend/**: Contains the frontend code and Kubernetes manifests.
- **udagram-reverseproxy/**: Contains the reverse proxy configuration and Kubernetes manifests.
- **k8s/**: Contains Kubernetes manifests for deployments, services, and configurations.

---

## Infrastructure Repository

The infrastructure for this project is managed using Terraform. You can find the repository here:
[monolith-to-microservices-infrastructure](https://github.com/m-ghanem-dev/monolith-to-microservices-infrastructure)

---

## Conclusion
This project showcases a modern microservices architecture with Kubernetes, CI/CD pipelines, and a reverse proxy. It is designed to be scalable, maintainable, and secure.