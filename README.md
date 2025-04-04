# 🐰 Production-Ready RabbitMQ Helm Chart on Kubernetes

## 🎯 Objective

Create a **production-ready Helm chart** to deploy **RabbitMQ in a 3-node clustered configuration** within a Kubernetes cluster. The deployment ensures **high availability**, **scalability**, and is suited for **real-world production environments**.

---

## 📁 Helm Chart Structure

rabbitmq-helm/ │ ├── Chart.yaml # Helm chart metadata ├── values.yaml # Customizable configurations ├── charts/ # (Optional) Dependencies └── templates/ # Kubernetes manifests ├── statefulset.yaml ├── secret.yaml └── service.yaml

---

## 🚀 Deployment Instructions

### 🧰 Prerequisites

1. Install Helm:
   ```bash
   curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
   echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
   sudo apt-get update
   sudo apt-get install -y helm

Create Namespace:
kubectl create namespace rabbit-namespace
Install Chart:
helm install rabbit ./rabbit --namespace rabbit-namespace
Upgrade Chart (if needed):
helm upgrade rabbit ./rabbit --namespace rabbit-namespace
Uninstall:
helm uninstall rabbit --namespace rabbit-namespace
⚙️ Configuration - values.yaml
namespace: rabbit-namespace
replicaCount: 3

image:
  repository: rabbitmq:4.0-management
  pullPolicy: IfNotPresent

service:
  type: NodePort
  ports:
    ss:
      port: 5672
      nodePort: 32501
    management:
      port: 15672
      nodePort: 32377

resources:
  limits:
    cpu: 500m
    memory: 500Mi
  requests:
    cpu: 500m
    memory: 500Mi

rabbit:
  adminUser: guest
  adminPassword: guest

📊 Accessing RabbitMQ Management Interface
URL: http://13.201.96.10:32377

Username: guest

Password: guest

📈 Scaling the Cluster
Option 1: Update values.yaml

replicaCount: 5

Then run:
helm upgrade rabbit ./rabbit --namespace rabbit-namespace
Option 2: Use kubectl:
kubectl scale statefulset rabbit --replicas=5 -n rabbit-namespace

🛠️ Troubleshooting
CNI Plugin Issue:
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml

Image Pull Errors:

Check pod status: kubectl get pods -n rabbit-namespace

Ensure correct image in values.yaml

PVC Issues or Endpoints not created:

Validate service and pod labels match

Scheduling Failures:

Pod stuck due to PVC or node resource issues

📹 Demonstration Video
🎥 Watch the deployment and clustering demo in this video.

📄 Documentation
For detailed deployment steps, visit:
📘 Documentation for Deploying RabbitMQ Using a Helm Chart on K8s.pdf

🙌 Author
Tushar More
GitHub: @more-tushar
