Kubernetes Monitoring Project
Overview
This project sets up a monitoring stack on Kubernetes using Prometheus and Grafana. It includes:

Prometheus: A powerful open-source monitoring and alerting toolkit.
Grafana: A popular open-source platform for monitoring and observability.
Getting Started
Prerequisites
Kubernetes cluster (Minikube, kind, or managed Kubernetes)
kubectl installed and configured
git for version control
Setup Instructions
1. Create the Monitoring Namespace
First, create a namespace for monitoring:

bash
Copy code
kubectl create namespace monitoring
2. Deploy Prometheus
Apply the Prometheus ConfigMap:

bash
Copy code
kubectl apply -f manifests/prometheus/prometheus-configmap.yaml
Apply the Prometheus Deployment and Service:

bash
Copy code
kubectl apply -f manifests/prometheus/prometheus-deployment.yaml
3. Deploy Grafana
Apply the Grafana Deployment and Service:

bash
Copy code
kubectl apply -f manifests/grafana/grafana-deployment.yaml
4. Access Grafana
Forward the Grafana service port to your local machine:

bash
Copy code
kubectl port-forward svc/grafana -n monitoring 3000:3000
Once the port is forwarded, you can access Grafana at http://localhost:3000.

Default Login Credentials:

Username: admin
Password: admin
5. Port Forwarding Prometheus
To access Prometheus, you need to forward its port in a new terminal window or tab. This will allow you to interact with Prometheus directly from your local machine.

Open a new terminal and run:

bash
Copy code
kubectl port-forward svc/prometheus -n monitoring 9090:9090
Once the port forwarding is active, you can access Prometheus by opening http://localhost:9090 in your browser.

Configure Grafana
Add Prometheus as a Data Source
Log in to Grafana using the default credentials (Username: admin, Password: admin).
Go to Configuration (gear icon) > Data Sources.
Click Add data source and choose Prometheus.
In the HTTP section, set the URL to http://prometheus.monitoring.svc.cluster.local:9090 (assuming Prometheus is running in the monitoring namespace).
Click Save & Test to ensure Grafana can communicate with Prometheus.
Import Dashboards
Grafana comes with a variety of pre-built dashboards. To import one:

Go to Create (plus icon) > Import.
You can either upload a JSON file for a dashboard or enter a dashboard ID from the Grafana dashboard repository.
For example, you might import the Kubernetes cluster monitoring dashboard (ID: 315).
Create Custom Dashboards (Optional)
If you want to create custom dashboards:

Go to Create > Dashboard.
Add panels for various metrics you're interested in monitoring. Grafana provides a wide range of visualization options and queries to help you monitor your Kubernetes cluster effectively.
PromQL Queries
Below are some common examples of PromQL queries you might use to get started:

Basic Prometheus Queries
CPU Usage (Node Exporter Metrics)

promql
Copy code
rate(node_cpu_seconds_total{mode="user"}[5m])
This query shows the rate of CPU usage in user mode over the last 5 minutes.

Memory Usage (Node Exporter Metrics)

promql
Copy code
node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes * 100
This query calculates the percentage of available memory.

Disk I/O (Node Exporter Metrics)

promql
Copy code
rate(node_disk_io_time_seconds_total[5m])
This query shows the rate of disk I/O time.

Network Traffic (Node Exporter Metrics)

promql
Copy code
rate(node_network_receive_bytes_total[5m])
This query shows the rate of bytes received over the network.

Kubernetes Pod Metrics

promql
Copy code
sum(rate(container_cpu_usage_seconds_total{namespace="default"}[5m])) by (pod)
This query sums CPU usage by pod in the "default" namespace.

Kubernetes Node Metrics

promql
Copy code
node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes
This query calculates the total memory usage on nodes.

Verify and Customize Monitoring
Verify Prometheus Scraping
Ensure Prometheus is correctly scraping metrics by accessing its web UI at http://localhost:9090.

Use the Targets tab to check that Prometheus is scraping metrics from the expected endpoints.

Conclusion
These instructions cover setting up Prometheus and Grafana, as well as accessing Grafana with the default credentials. Feel free to submit issues or pull requests to improve this project.

License
This project is licensed under the MIT License. See the LICENSE file for details.
