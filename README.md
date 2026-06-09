# ☸️ Kubernetes Observability with Helm, Prometheus & Grafana

## 📖 Project Overview

This project demonstrates the implementation of a Kubernetes monitoring stack using:

- Helm
- Metrics Server
- Prometheus
- Grafana

The objective is to monitor Kubernetes cluster resources, visualize metrics, and gain hands-on experience with Kubernetes observability tools commonly used in production environments.

---

# 🏗️ Architecture

```text
Kubernetes Cluster
│
├── Helm
│   ├── Metrics Server
│   ├── Prometheus
│   └── Grafana
│
├── Metrics Server
│   └── Collects CPU & Memory Metrics
│
├── Prometheus
│   └── Stores Cluster Metrics
│
└── Grafana
    └── Visualizes Metrics Using Dashboards
```

---

# 📦 What is Helm?

Helm is the package manager for Kubernetes.

It simplifies application deployment and management by packaging Kubernetes resources into reusable units called **Charts**.

Similar to Linux package managers:

### Amazon Linux

```bash
sudo yum install git -y
```

### Ubuntu

```bash
sudo apt install git -y
```

### Kubernetes

```bash
helm install prometheus prometheus-community/kube-prometheus-stack
```

---

# 📚 Helm Terminology

## Chart

A collection of Kubernetes YAML manifests packaged together.

## Release

A deployed instance of a Helm Chart.

## Repository

A location where Helm Charts are stored and shared.

---

# 🚀 Installing Helm

## Download Helm Installation Script

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
```

## Grant Execute Permissions

```bash
chmod 700 get_helm.sh
```

## Install Helm

```bash
./get_helm.sh
```

## Verify Installation

```bash
helm version
```

---

# 📊 Installing Metrics Server

Metrics Server provides CPU and Memory utilization information for Kubernetes nodes and pods.

## Add Metrics Server Repository

```bash
helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server/
```

## Install Metrics Server

```bash
helm upgrade --install metrics-server metrics-server/metrics-server
```

## Verify Installation

```bash
kubectl get pods -A
```

## View Resource Usage

### Node Metrics

```bash
kubectl top nodes
```

### Pod Metrics

```bash
kubectl top pods
```

---

# 📈 Prometheus & Grafana

## Prometheus

Prometheus is an open-source monitoring and alerting toolkit.

### Features

- Collects Kubernetes metrics
- Stores time-series data
- Supports alerting
- Provides powerful querying capabilities

---

## Grafana

Grafana is a visualization platform used to create monitoring dashboards.

### Features

- Real-time monitoring
- Interactive dashboards
- Historical analysis
- Alert visualization

---

# 🚀 Deploying Prometheus & Grafana Using Helm

## Add Helm Repositories

```bash
helm repo add stable https://charts.helm.sh/stable
```

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

## Update Helm Repositories

```bash
helm repo update
```

## Install kube-prometheus-stack

```bash
helm install monitoring prometheus-community/kube-prometheus-stack
```

---

# 🔍 Verify Deployment

Check Pods:

```bash
kubectl get pods -A
```

Check Services:

```bash
kubectl get svc -A
```

---

# 🌐 Exposing Prometheus & Grafana

Since this project uses a self-managed Kubernetes cluster, Prometheus and Grafana services were exposed using **NodePort**.

## Expose Prometheus

```bash
kubectl edit svc monitoring-kube-prometheus-prometheus
```

Change:

```yaml
type: ClusterIP
```

To:

```yaml
type: NodePort
```

---

## Expose Grafana

```bash
kubectl edit svc monitoring-grafana
```

Change:

```yaml
type: ClusterIP
```

To:

```yaml
type: NodePort
```

---

# 🔐 Security Group Configuration

Ensure the following ports are allowed:

| Port | Purpose |
|--------|---------|
| 22 | SSH Access |
| 6443 | Kubernetes API Server |
| 30000-32767 | NodePort Range |

---

# 🌍 Accessing Prometheus

Find the assigned NodePort:

```bash
kubectl get svc
```

Example:

```text
9090:30900/TCP
```

Access Prometheus:

```text
http://<PUBLIC-IP>:30900
```

---

# 📊 Accessing Grafana

Find the assigned NodePort:

```bash
kubectl get svc
```

Example:

```text
80:32000/TCP
```

Access Grafana:

```text
http://<PUBLIC-IP>:32000
```

---

# 🔑 Grafana Login Credentials

```text
Username: admin
Password: prom-operator
```

---

# 📈 Grafana Dashboards

After login:

```text
Dashboards → Browse
```

Available dashboards include:

- Kubernetes Cluster
- Kubernetes API Server
- Node Monitoring
- Pod Monitoring
- Resource Utilization

Metrics Available:

- CPU Usage
- Memory Usage
- Network Usage
- Pod Health
- Node Health

---

# 📸 Screenshots

## Helm Installation

<img width="1919" height="242" alt="1" src="https://github.com/user-attachments/assets/1626794f-30de-41d1-9ec2-c661767c3574" />


---

## Metrics Server Installation

<img width="1919" height="403" alt="2" src="https://github.com/user-attachments/assets/5d75ee7c-5bc5-4a1d-96a8-3cf43cfe01f1" />


---

## Node Metrics & Pod Metrics
<img width="1919" height="238" alt="3" src="https://github.com/user-attachments/assets/75a527d1-67eb-4b97-a299-da66bebb6e67" />


---
## Prometheus Pods
<img width="1919" height="780" alt="4" src="https://github.com/user-attachments/assets/46c57b4e-345d-4e0e-863e-9e2818bb760a" />
<img width="1919" height="577" alt="4_1" src="https://github.com/user-attachments/assets/f31d696b-0a41-4672-a7b9-2994c0937997" />

---
## Service Editing
<img width="1919" height="409" alt="5" src="https://github.com/user-attachments/assets/ac9693b1-aaaf-4c7e-946d-2f9240b75c3f" />

---
## Prometheus Dashboard
<img width="1919" height="1079" alt="6" src="https://github.com/user-attachments/assets/993a8581-04a2-4f1c-901c-53474a197ca6" />


---

## Grafana Login

<img width="1919" height="1079" alt="7" src="https://github.com/user-attachments/assets/023ca2ef-7849-4766-a7ff-e6a05c091a02" />
<img width="1919" height="1079" alt="7_1" src="https://github.com/user-attachments/assets/4385dcf9-449c-4fae-bfab-02b190d616e1" />
<img width="1915" height="1079" alt="7_2" src="https://github.com/user-attachments/assets/e8898e23-30b4-486b-a7f1-258870d9c151" />


---

## Grafana Dashboard

<img width="1919" height="1079" alt="7_3" src="https://github.com/user-attachments/assets/bcf2286f-fd34-4ee6-9fc5-28fcc0ae884f" />


---

## Cluster Monitoring Dashboard

<img width="1919" height="1079" alt="8" src="https://github.com/user-attachments/assets/0971708f-a95d-4a3c-be1b-99f5f8532694" />


---
## 🚨 Issues that may occur

### Issue

While accessing the Grafana dashboard, the login attempt fails with the following error:

```text
Invalid username or password
```

### Cause

The default Grafana credentials may have been changed during installation, or the password stored in the Kubernetes Secret differs from the expected default value.

### Resolution

Retrieve the Grafana username from the Kubernetes Secret:

```bash
kubectl get secret monitoring-grafana \
-o jsonpath="{.data.admin-user}" | base64 --decode
```

Retrieve the Grafana password:

```bash
kubectl get secret monitoring-grafana \
-o jsonpath="{.data.admin-password}" | base64 --decode
```

If the secret name is different, first list all available secrets:

```bash
kubectl get secrets
```

Identify the Grafana secret and use its name in the commands above.

### Verification

Verify that the Grafana pod is running correctly:

```bash
kubectl get pods -A | grep grafana
```

Expected output:

```text
grafana-xxxxxxxxxx-xxxxx   1/1   Running   0   <age>
```

### Result

After retrieving the correct credentials from the Kubernetes Secret, log in to the Grafana dashboard again using the decoded username and password.

---
# 🛠️ Helm Command Cheat Sheet

## List Repositories

```bash
helm repo ls
```

## Update Repositories

```bash
helm repo update
```

## List Releases

```bash
helm list
```

## Install Chart

```bash
helm install <release-name> <chart-name>
```

## Upgrade Chart

```bash
helm upgrade <release-name> <chart-name>
```

## Delete Release

```bash
helm delete <release-name>
```

## Check Helm Version

```bash
helm version
```

---

# 🎯 Learning Outcomes

Through this project, I gained hands-on experience with:

- Helm Package Management
- Helm Charts & Releases
- Metrics Server Deployment
- Kubernetes Resource Monitoring
- Prometheus Installation & Configuration
- Grafana Dashboard Management
- Kubernetes Observability
- Service Exposure Using NodePort
- Monitoring Production-Style Kubernetes Workloads

---
