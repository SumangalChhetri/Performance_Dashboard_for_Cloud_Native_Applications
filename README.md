# Kubernetes Monitoring Project

## Overview

This project sets up a monitoring stack on Kubernetes using Prometheus and Grafana. It includes:

- **Prometheus**: A powerful open-source monitoring and alerting toolkit.
- **Grafana**: A popular open-source platform for monitoring and observability.

## Getting Started

### Prerequisites

- Kubernetes cluster (Minikube, kind, or managed Kubernetes)
- kubectl installed and configured
- git for version control

### Setup Instructions

1. **Create the Monitoring Namespace**

   First, create a namespace for monitoring:

   
bash
   kubectl create namespace monitoring
# Prometheus and Grafana Deployment

## Deploy Prometheus

1. **Apply the Prometheus ConfigMap:**
bash
   kubectl apply -f manifests/prometheus/prometheus-configmap.yaml
# Prometheus and Grafana Deployment Instructions

This Markdown file includes the complete instructions for deploying Prometheus and Grafana, as well as accessing Grafana with the default credentials.

## Apply the Prometheus Deployment and Service

To deploy Prometheus, run the following command:

bash
kubectl apply -f manifests/prometheus/prometheus-deployment.yaml                                                

## Deploy Grafana

To deploy Grafana, apply the Grafana Deployment and Service with the following command:
bash
kubectl apply -f manifests/grafana/grafana-deployment.yaml
# Access Grafana

To access Grafana, you need to forward the Grafana service port to your local machine. Use the following command:

bash
kubectl port-forward svc/grafana -n monitoring 3000:3000
# Access Grafana

Once the port is forwarded, you can access Grafana at [http://localhost:3000](http://localhost:3000).

## Default Login Credentials

- **Username**: admin
- **Password**: admin

## Conclusion

These instructions cover accessing Grafana and its default credentials. meger all this md file as README.md