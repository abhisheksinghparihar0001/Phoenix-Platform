# Phoenix Platform

## Overview

The **Phoenix Platform** is a scalable and modular web application. It includes a **React.js** frontend, a **Node.js** backend, and utilizes **Docker** containers orchestrated by **Kubernetes**. The platform also includes monitoring and observability features through **Prometheus** and **Grafana**.

This architecture provides a robust system for handling web traffic, API requests, and database interactions. It’s designed for ease of scaling and maintenance, ensuring high availability and performance.

---

## Project Structure Breakdown

### 1. **ui-layer/** – Frontend

The **frontend** is a React.js application that serves the user-facing part of the platform.

- **react-app/**
  - `Dockerfile`: Defines how the React app is built into a Docker container.
  - `package.json`: Contains the dependencies required by the React application.
  - `src/`: Contains the source code for the React application.
    - `index.js`: The main entry point for the React application.

- **nginx/**
  - `nginx.conf`: Configuration file for Nginx, which acts as a reverse proxy, routing traffic from the frontend to the backend.

### 2. **service-layer/** – Backend

The **backend** is built using **Node.js** to handle API requests, business logic, and database interactions.

- **backend/**
  - `Dockerfile`: Defines how the Node.js backend is containerized.
  - `package.json`: Contains the dependencies required by the backend application.
  - `app.js`: The main entry point for the Node.js application, which processes API routes and communicates with the database.

### 3. **platform-k8s/** – Kubernetes Resources

This folder contains Kubernetes configuration files for deploying the platform in a Kubernetes cluster, including deployments, services, ingress, and monitoring configurations.

- **app/**
  - `frontend-deployment.yaml`: Defines the Kubernetes Deployment for the React frontend.
  - `frontend-service.yaml`: Defines the Kubernetes Service for the React frontend.
  - `backend-deployment.yaml`: Defines the Kubernetes Deployment for the Node.js backend.
  - `backend-service.yaml`: Defines the Kubernetes Service for the Node.js backend.
  - `ingress.yaml`: Configures Ingress to handle external HTTP(S) traffic.
  - `hpa.yaml`: Defines the Horizontal Pod Autoscaler (HPA) to scale the frontend and backend services based on CPU utilization.

- **data/**
  - `mongo-deployment.yaml`: Defines the Kubernetes Deployment for MongoDB.
  - `mongo-service.yaml`: Defines the Kubernetes Service for MongoDB.
  - `redis-deployment.yaml`: Defines the Kubernetes Deployment for Redis.
  - `redis-service.yaml`: Defines the Kubernetes Service for Redis.

- **config/**
  - `configmap.yaml`: Defines a ConfigMap for storing non-sensitive configuration data.
  - `secret.yaml`: Defines a Secret for storing sensitive data (e.g., passwords, API keys).

- **monitoring/**
  - `prometheus-config.yaml`: Configures Prometheus for metric collection.
  - `prometheus-deployment.yaml`: Defines the Kubernetes Deployment for Prometheus.
  - `prometheus-service.yaml`: Defines the Prometheus Service.
  - `grafana-deployment.yaml`: Defines the Kubernetes Deployment for Grafana.
  - `grafana-service.yaml`: Defines the Grafana Service for monitoring visualization.

### 4. **README.md** – Documentation

This file provides an overview of the platform, setup instructions, deployment guides, and an explanation of the architecture.

---

## How It All Works Together

### Frontend (React.js + Nginx)

- The **React.js** frontend is served through **Nginx**, which acts as a reverse proxy. Nginx routes traffic to the backend while serving the static React app.
- The frontend is containerized using **Docker** and deployed in Kubernetes as a pod.

### Backend (Node.js)

- The **Node.js** backend handles all API requests, processes business logic, and interacts with databases (MongoDB and Redis).
- The backend is containerized with **Docker** and deployed as a Kubernetes pod.

### MongoDB & Redis

- **MongoDB** is the primary data store, used for persistent storage.
- **Redis** is used as a caching layer, improving performance by storing frequently accessed data in memory.

### Kubernetes

- **Kubernetes** orchestrates all the containers, managing deployments, scaling, and service discovery.
- The **Horizontal Pod Autoscaler (HPA)** ensures that the frontend and backend services automatically scale based on CPU utilization.

### Ingress

- **Ingress** routes external HTTP(S) traffic to the appropriate services, providing a single entry point into the platform.

### Monitoring (Prometheus + Grafana)

- **Prometheus** collects metrics such as CPU usage, memory usage, request latency, and error rates.
- **Grafana** visualizes the metrics from Prometheus, providing real-time dashboards that display platform health and performance.

### ConfigMaps and Secrets

- **ConfigMaps** store non-sensitive configuration data (e.g., environment settings).
- **Secrets** store sensitive data (e.g., database credentials, API keys) securely within the Kubernetes cluster.

---

## Project in Action

### User Interaction Flow:

1. **Frontend**: When a user accesses the platform, their request first hits **Nginx**, which serves the React frontend.
2. **Backend Interaction**: If the user interacts with the backend (e.g., fetching data), Nginx routes the request to the **Node.js** backend.
3. **Database**: The backend may query **MongoDB** to retrieve data or **Redis** to fetch cached data, improving response times.
4. **Monitoring**: **Prometheus** collects metrics from the system, and **Grafana** displays these metrics in real-time, allowing you to monitor the health and performance of the platform.

---

## Tech Stack

- **Frontend**: React.js, Nginx, Docker
- **Backend**: Node.js, Docker
- **Database**: MongoDB, Redis
- **Infrastructure**: Kubernetes
- **Monitoring**: Prometheus, Grafana

---

## Folder Structure

```plaintext
phoenix-platform/
│
├── ui-layer/
│   ├── react-app/
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── src/index.js
│   │
│   └── nginx/nginx.conf
│
├── service-layer/
│   └── backend/
│       ├── Dockerfile
│       ├── package.json
│       └── app.js
│
├── platform-k8s/
│   ├── app/
│   │   ├── frontend-deployment.yaml
│   │   ├── frontend-service.yaml
│   │   ├── backend-deployment.yaml
│   │   ├── backend-service.yaml
│   │   ├── ingress.yaml
│   │   └── hpa.yaml
│   │
│   ├── data/
│   │   ├── mongo-deployment.yaml
│   │   ├── mongo-service.yaml
│   │   ├── redis-deployment.yaml
│   │   └── redis-service.yaml
│   │
│   ├── config/
│   │   ├── configmap.yaml
│   │   └── secret.yaml
│   │
│   └── monitoring/
│       ├── prometheus-config.yaml
│       ├── prometheus-deployment.yaml
│       ├── prometheus-service.yaml
│       ├── grafana-deployment.yaml
│       └── grafana-service.yaml



