# Kubernetes Cluster Deployment Guide
---

## 1. Dockerfiles for Applications

### Streamlit App Dockerfile

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

EXPOSE 8501

CMD ["streamlit", "run", "app.py"]
```

### MongoDB Dockerfile

```dockerfile
FROM mongo:latest

EXPOSE 27017
```

### Nginx Dockerfile

```dockerfile
FROM nginx:latest

COPY ./nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
```

### Grafana Dockerfile

```dockerfile
FROM grafana/grafana:latest

EXPOSE 3000
```

## 2. Kubernetes Configuration

### Workflow Explanation

1. **Deployment**: Streamlit, MongoDB, Nginx, and Grafana are deployed in the K8S cluster.
2. **Services**: Each deployment is exposed via services to enable communication within the cluster and external access.
3. **Namespaces**: Different namespaces are used for logical separation and resource management.
4. **Pods**: Each application runs in its own pod(s).
5. **Nodes**: The cluster is spread across two locations (`location_1` and `location_2`), with worker nodes in each location.

### Kubernetes YAML Files

#### Namespace Configuration

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```

#### Streamlit Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: streamlit-deployment
  namespace: my-namespace
spec:
  replicas: 2
  selector:
    matchLabels:
      app: streamlit
  template:
    metadata:
      labels:
        app: streamlit
    spec:
      containers:
      - name: streamlit
        image: my-streamlit-app:latest
        ports:
        - containerPort: 8501
```

#### MongoDB Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  namespace: my-namespace
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers:
      - name: mongodb
        image: mongo:latest
        ports:
        - containerPort: 27017
```

#### Nginx Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: my-namespace
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

#### Grafana Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment
  namespace: my-namespace
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
      - name: grafana
        image: grafana/grafana:latest
        ports:
        - containerPort: 3000
```

#### Services Configuration

```yaml
apiVersion: v1
kind: Service
metadata:
  name: streamlit-service
  namespace: my-namespace
spec:
  selector:
    app: streamlit
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8501
  type: LoadBalancer
---
apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
  namespace: my-namespace
spec:
  selector:
    app: mongodb
  ports:
    - protocol: TCP
      port: 27017
  type: ClusterIP
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: my-namespace
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
  type: LoadBalancer
---
apiVersion: v1
kind: Service
metadata:
  name: grafana-service
  namespace: my-namespace
spec:
  selector:
    app: grafana
  ports:
    - protocol: TCP
      port: 3000
  type: LoadBalancer
```

## 3. Python Code for Kubernetes Monitoring

### Dependencies

```bash
pip install kubernetes
```

### Code Implementation

```python
from kubernetes import client, config

config.load_kube_config()

def get_all_stats():
    v1 = client.CoreV1Api()
    print("Listing pods with their IPs:")
    ret = v1.list_pod_for_all_namespaces(watch=False)
    for i in ret.items:
        print(f"{i.status.pod_ip}\t{i.metadata.namespace}\t{i.metadata.name}")

def get_namespace_resources(namespace):
    v1 = client.CoreV1Api()
    print(f"Resources in namespace: {namespace}")
    pods = v1.list_namespaced_pod(namespace)
    services = v1.list_namespaced_service(namespace)
    
    print("Pods:")
    for pod in pods.items:
        print(f"{pod.metadata.name}")

    print("Services:")
    for svc in services.items:
        print(f"{svc.metadata.name}")

def list_all_services_and_namespaces():
    v1 = client.CoreV1Api()
    namespaces = v1.list_namespace()
    services = v1.list_service_for_all_namespaces()
    
    print("Namespaces:")
    for ns in namespaces.items:
        print(f"{ns.metadata.name}")

    print("Services:")
    for svc in services.items:
        print(f"{svc.metadata.name} in {svc.metadata.namespace}")

def k8s_commands_cheatsheet():
    commands = [
        "kubectl get pods",
        "kubectl get services",
        "kubectl get deployments",
        "kubectl get nodes",
        "kubectl describe pod <pod_name>",
        "kubectl describe service <service_name>",
        "kubectl describe deployment <deployment_name>",
        "kubectl logs <pod_name>",
        "kubectl exec -it <pod_name> -- /bin/bash"
    ]
    for cmd in commands:
        print(cmd)

# Example usage
get_all_stats()
get_namespace_resources("my-namespace")
list_all_services_and_namespaces()
k8s_commands_cheatsheet()
```

## 4. Kubernetes Monitoring Cheatsheet

- **Get Pods:** `kubectl get pods`
- **Get Services:** `kubectl get services`
- **Get Deployments:** `kubectl get deployments`
- **Get Nodes:** `kubectl get nodes`
- **Describe Pod:** `kubectl describe pod <pod_name>`
- **Describe Service:** `kubectl describe service <service_name>`
- **Describe Deployment:** `kubectl describe deployment <deployment_name>`
- **View Logs:** `kubectl logs <pod_name>`
- **Execute Command in Pod:** `kubectl exec -it <pod_name> -- /bin/bash`

This guide provides a comprehensive overview of setting up and monitoring a Kubernetes cluster with multiple applications. Each section is designed to help you understand and implement the necessary components for a robust and scalable deployment.
