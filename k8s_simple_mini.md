# Kubernetes Cluster Architecture with Streamlit, MongoDB, NGINX, and Grafana

## Overview

In this guide, we will set up a Kubernetes (K8s) cluster across two locations (location_1 and location_2) to deploy a Streamlit application, MongoDB, NGINX, and Grafana. This architecture will facilitate high availability and scalability.

### Key Components

1. **Kubernetes Cluster**: A set of nodes (worker machines) that run applications.
2. **Pods**: The smallest deployable units in K8s, which can contain one or more containers.
3. **Namespaces**: Virtual clusters within a K8s cluster to organize resources.
4. **Services**: Abstract way to expose applications running on a set of Pods.
5. **Deployments**: Ensure that a specific number of Pods are running.
6. **Applications**: Streamlit app, MongoDB, NGINX, and Grafana.

## Dockerfile Example

### Streamlit App Dockerfile

```dockerfile
# Use the official Python image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the requirements file
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application code
COPY . .

# Command to run the application
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

### Explanation of Workflow

1. **Build the Docker Images**: Each component (Streamlit, MongoDB, NGINX, Grafana) will have its own Dockerfile.
2. **Push Images to Registry**: Push these images to a container registry (e.g., Docker Hub).
3. **Deploy to Kubernetes**:
   - Create deployments for each application.
   - Use services to expose the applications internally and externally as needed.
4. **Monitor with Grafana**: Use Grafana to visualize metrics from the applications and K8s cluster.

## Kubernetes Configuration

### 1. Namespace Configuration

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: streamlit-app
---
apiVersion: v1
kind: Namespace
metadata:
  name: monitoring
```

### 2. Deployment Configuration

#### Streamlit Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: streamlit-deployment
  namespace: streamlit-app
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
        image: your-dockerhub-username/streamlit-app:latest
        ports:
        - containerPort: 8501
```

#### MongoDB Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  namespace: streamlit-app
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

#### NGINX Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: streamlit-app
spec:
  replicas: 1
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
  namespace: monitoring
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

### 3. Service Configuration

#### Streamlit Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: streamlit-service
  namespace: streamlit-app
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 8501
  selector:
    app: streamlit
```

#### MongoDB Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
  namespace: streamlit-app
spec:
  ports:
    - port: 27017
  selector:
    app: mongodb
```

#### NGINX Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: streamlit-app
spec:
  ports:
    - port: 80
  selector:
    app: nginx
```

#### Grafana Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: grafana-service
  namespace: monitoring
spec:
  type: LoadBalancer
  ports:
    - port: 3000
  selector:
    app: grafana
```

## Python Code for Monitoring K8s Resources

### Functions for Resource Management

```python
import subprocess
import json

def get_resources(namespace):
    """Return all resources in a specific namespace."""
    cmd = f"kubectl get all -n {namespace} -o json"
    result = subprocess.run(cmd, shell=True, capture_output=True, text=True)
    return json.loads(result.stdout)

def list_services_and_namespaces():
    """List all services and namespaces."""
    services = subprocess.run("kubectl get services --all-namespaces -o json", shell=True, capture_output=True, text=True)
    namespaces = subprocess.run("kubectl get namespaces -o json", shell=True, capture_output=True, text=True)
    return json.loads(services.stdout), json.loads(namespaces.stdout)

def k8s_cheatsheet():
    """Return a cheatsheet of common K8s commands."""
    commands = {
        "Get all resources in a namespace": "kubectl get all -n <namespace>",
        "Get pods": "kubectl get pods",
        "Get services": "kubectl get services",
        "Get deployments": "kubectl get deployments",
        "Describe pod": "kubectl describe pod <pod-name>",
        "Logs of a pod": "kubectl logs <pod-name>",
        "Execute command in a pod": "kubectl exec -it <pod-name> -- <command>"
    }
    return commands
```

## Conclusion

This guide provides a comprehensive overview of setting up a K8s cluster with multiple applications. You can expand this framework by adding more features or scaling the applications as needed. Use the provided Python functions to monitor your K8s resources efficiently.
