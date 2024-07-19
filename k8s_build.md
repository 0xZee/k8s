> Configuration for a Kubernetes cluster that includes a set of 10 applications commonly used in a web service architecture. These applications will include web apps, databases, monitoring tools, and other essential components.
---

### Kubernetes Cluster Configuration
---

#### Applications

1. **Frontend Web Applications:**
   - `webapp1`
   - `webapp2`

2. **Database Services:**
   - `mongodb`
   - `postgres`

3. **Monitoring and Logging:**
   - `grafana`
   - `prometheus`
   - `kibana`
   - `elasticsearch`

4. **Proxy:**
   - `nginx`

5. **CI/CD Tool:**
   - `jenkins`

#### Namespaces

- `frontend`
- `backend`
- `monitoring`
- `logging`

#### Example Configuration

Here's a sample Kubernetes YAML configuration for these applications:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: frontend

---

apiVersion: v1
kind: Namespace
metadata:
  name: backend

---

apiVersion: v1
kind: Namespace
metadata:
  name: monitoring

---

apiVersion: v1
kind: Namespace
metadata:
  name: logging

---

# Frontend Web App 1
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp1-deployment
  namespace: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webapp1
  template:
    metadata:
      labels:
        app: webapp1
    spec:
      containers:
      - name: webapp1-container
        image: nginx:latest
        ports:
        - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: webapp1-service
  namespace: frontend
spec:
  selector:
    app: webapp1
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

---

# Frontend Web App 2
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp2-deployment
  namespace: frontend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: webapp2
  template:
    metadata:
      labels:
        app: webapp2
    spec:
      containers:
      - name: webapp2-container
        image: httpd:latest
        ports:
        - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: webapp2-service
  namespace: frontend
spec:
  selector:
    app: webapp2
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

---

# MongoDB
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  namespace: backend
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
      - name: mongodb-container
        image: mongo:latest
        ports:
        - containerPort: 27017

---

apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
  namespace: backend
spec:
  selector:
    app: mongodb
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
  type: ClusterIP

---

# PostgreSQL
apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres-deployment
  namespace: backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
      - name: postgres-container
        image: postgres:latest
        ports:
        - containerPort: 5432

---

apiVersion: v1
kind: Service
metadata:
  name: postgres-service
  namespace: backend
spec:
  selector:
    app: postgres
  ports:
    - protocol: TCP
      port: 5432
      targetPort: 5432
  type: ClusterIP

---

# Grafana
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
      - name: grafana-container
        image: grafana/grafana:latest
        ports:
        - containerPort: 3000

---

apiVersion: v1
kind: Service
metadata:
  name: grafana-service
  namespace: monitoring
spec:
  selector:
    app: grafana
  ports:
    - protocol: TCP
      port: 3000
      targetPort: 3000
  type: LoadBalancer

---

# Prometheus
apiVersion: apps/v1
kind: Deployment
metadata:
  name: prometheus-deployment
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: prometheus
  template:
    metadata:
      labels:
        app: prometheus
    spec:
      containers:
      - name: prometheus-container
        image: prom/prometheus:latest
        ports:
        - containerPort: 9090

---

apiVersion: v1
kind: Service
metadata:
  name: prometheus-service
  namespace: monitoring
spec:
  selector:
    app: prometheus
  ports:
    - protocol: TCP
      port: 9090
      targetPort: 9090
  type: LoadBalancer

---

# Kibana
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kibana-deployment
  namespace: logging
spec:
  replicas: 1
  selector:
    matchLabels:
      app: kibana
  template:
    metadata:
      labels:
        app: kibana
    spec:
      containers:
      - name: kibana-container
        image: kibana:latest
        ports:
        - containerPort: 5601

---

apiVersion: v1
kind: Service
metadata:
  name: kibana-service
  namespace: logging
spec:
  selector:
    app: kibana
  ports:
    - protocol: TCP
      port: 5601
      targetPort: 5601
  type: LoadBalancer

---

# Elasticsearch
apiVersion: apps/v1
kind: Deployment
metadata:
  name: elasticsearch-deployment
  namespace: logging
spec:
  replicas: 1
  selector:
    matchLabels:
      app: elasticsearch
  template:
    metadata:
      labels:
        app: elasticsearch
    spec:
      containers:
      - name: elasticsearch-container
        image: elasticsearch:latest
        ports:
        - containerPort: 9200

---

apiVersion: v1
kind: Service
metadata:
  name: elasticsearch-service
  namespace: logging
spec:
  selector:
    app: elasticsearch
  ports:
    - protocol: TCP
      port: 9200
      targetPort: 9200
  type: ClusterIP

---

# Nginx Proxy
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: frontend
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
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: frontend
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

---

# Jenkins
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jenkins-deployment
  namespace: backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  template:
    metadata:
      labels:
        app: jenkins
    spec:
      containers:
      - name: jenkins-container
        image: jenkins/jenkins:lts
        ports:
        - containerPort: 8080

---

apiVersion: v1
kind: Service
metadata:
  name: jenkins-service
  namespace: backend
spec:
  selector:
    app: jenkins
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
  type: LoadBalancer
```

### Python Code to Gather Stats

Here's the adapted Python code to interact with this setup:

```python
from kubernetes import client, config

# Load the kubeconfig file
config.load_kube_config()

v1 = client.CoreV1Api()
apps_v1 = client.AppsV1Api()

def get_all_stats():
    print("Listing all pods with their IPs:")
    ret = v1.list_pod_for_all_namespaces(watch=False)
    for i in ret.items:
        print(f"{i.metadata.namespace}\t{i.metadata.name}\t{i.status.pod_ip}")

    print("\nListing all nodes:")
    ret = v1.list_node()
    for i in ret.items:
        print(f"{i.metadata.name}\t{i.status.addresses[0].address}")

    print("\nListing all namespaces:")
    ret = v1.list_namespace()
    for i in ret.items:
        print(i.metadata.name)

def get_resources_by_namespace(namespace):
    print(f"Resources in namespace {namespace}:")

    print("\nPods:")
    ret = v1.list_namespaced_pod(namespace)
    for i in ret.items:
        print(f"{i.metadata.name}\t{i.status.pod_ip}")

    print("\nServices:")
    ret = v1.list_namespaced_service(namespace)
    for i in ret.items:
        print(f"{i.metadata.name}\t{i.spec.cluster_ip}")

    print("\nDeployments:")
    ret = apps_v1.list_namespaced_deployment(namespace)
    for i in ret.items:
        print(f"{i.metadata.name}\t{i.status.replicas} replicas")

def list_services_and_namespaces():
    print("Listing all services in all namespaces:")
    ret = v1.list_service_for_all_namespaces(watch=False)
    for i in ret.items:
        print(f"{i.metadata.namespace}\t{i.metadata.name}\t{i.spec.cluster_ip}")

    print("\nListing all namespaces:")
    ret = v1.list_namespace()
    for i in ret.items:
        print(i.metadata.name)

if __name__ == "__main__":
    get_all_stats()
    print("\n")
    namespace = "frontend"  # Example namespace
    get_resources_by_namespace(namespace)
    print("\n")
    list_services_and_namespaces()
```

### Explanation

- **Namespaces:** `frontend`, `backend`, `monitoring`, `logging` to organize different components.
- **Applications:** Various commonly used web services, databases, monitoring, and logging tools.
- **Python Code:** Interacts with the Kubernetes cluster to gather and display stats.

This setup provides a structured way to manage and monitor a web service architecture using Kubernetes. Adjust the configurations and Python functions as needed for your specific requirements.


---

> Workflow and Architecture Explanation

### Workflow and Architecture Explanation
---

#### Workflow

1. **Namespaces:**
    - **frontend:** Contains web applications and the NGINX proxy.
    - **backend:** Houses database services and the CI/CD tool Jenkins.
    - **monitoring:** Includes tools like Grafana and Prometheus for monitoring.
    - **logging:** Contains Elasticsearch and Kibana for logging and visualization.

2. **Service Load Balancing:**
    - Each service is exposed using a Kubernetes service, which can be of type `ClusterIP`, `NodePort`, or `LoadBalancer`.
    - **LoadBalancer** services (e.g., `nginx-service`, `grafana-service`) expose services to external traffic.
    - **ClusterIP** services (e.g., `mongodb-service`, `postgres-service`) are internal to the cluster.
    
3. **Replicas:**
    - The `replicas` field in a Deployment specifies the number of pod replicas to run, ensuring high availability and load distribution.
    - For example, `webapp1-deployment` and `nginx-deployment` are set to run multiple replicas.

4. **Deployment and Service Interaction:**
    - Deployments manage the lifecycle of applications (creating, updating, deleting pods).
    - Services provide a stable network endpoint for accessing these pods, with load balancing across the replicas.

#### Expected Output

Here’s an example of what you might expect from a command like `kubectl get all --all-namespaces`:

```
NAMESPACE     NAME                                          READY   STATUS    RESTARTS   AGE   IP            NODE   NOMINATED NODE   READINESS GATES
frontend      pod/webapp1-deployment-5d5f4f9d9f-abcde       1/1     Running   0          10m   10.244.0.1    node1  <none>           <none>
frontend      pod/webapp1-deployment-5d5f4f9d9f-fghij       1/1     Running   0          10m   10.244.0.2    node2  <none>           <none>
frontend      pod/nginx-deployment-6d9cfdf8d7-xyz12         1/1     Running   0          8m    10.244.0.3    node1  <none>           <none>
backend       pod/mongodb-deployment-7d9cfdf8d7-klmno       1/1     Running   0          15m   10.244.0.4    node2  <none>           <none>
backend       pod/jenkins-deployment-7d9cfdf8d7-uvwxz       1/1     Running   0          12m   10.244.0.5    node1  <none>           <none>
monitoring    pod/grafana-deployment-7d9cfdf8d7-pqrst       1/1     Running   0          11m   10.244.0.6    node2  <none>           <none>

NAMESPACE     NAME                  TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
frontend      service/nginx         LoadBalancer   10.96.0.1       <pending>     80:32000/TCP     8m
backend       service/mongodb       ClusterIP      10.96.0.2       <none>        27017/TCP        15m
monitoring    service/grafana       LoadBalancer   10.96.0.3       <pending>     3000:32001/TCP   11m

NAMESPACE     NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
frontend      deployment.apps/webapp1-deployment  2/2     2            2           10m
frontend      deployment.apps/nginx-deployment    2/2     2            2           8m
backend       deployment.apps/mongodb-deployment  1/1     1            1           15m
backend       deployment.apps/jenkins-deployment  1/1     1            1           12m
monitoring    deployment.apps/grafana-deployment  1/1     1            1           11m
```

### Python Code Cheat Sheet

Here’s a Python cheat sheet for common tasks using `client.CoreV1Api` and `client.AppsV1Api`:

```python
from kubernetes import client, config

# Load kubeconfig
config.load_kube_config()

v1 = client.CoreV1Api()
apps_v1 = client.AppsV1Api()

# List all pods in all namespaces
def list_all_pods():
    pods = v1.list_pod_for_all_namespaces(watch=False)
    for pod in pods.items:
        print(f"Namespace: {pod.metadata.namespace}, Pod: {pod.metadata.name}, IP: {pod.status.pod_ip}")

# List all services in all namespaces
def list_all_services():
    services = v1.list_service_for_all_namespaces(watch=False)
    for service in services.items:
        print(f"Namespace: {service.metadata.namespace}, Service: {service.metadata.name}, IP: {service.spec.cluster_ip}")

# List all deployments in all namespaces
def list_all_deployments():
    deployments = apps_v1.list_deployment_for_all_namespaces(watch=False)
    for deployment in deployments.items:
        print(f"Namespace: {deployment.metadata.namespace}, Deployment: {deployment.metadata.name}, Replicas: {deployment.status.replicas}")

# List all nodes
def list_all_nodes():
    nodes = v1.list_node(watch=False)
    for node in nodes.items:
        print(f"Node: {node.metadata.name}, IP: {node.status.addresses[0].address}")

# Get all resources in a specific namespace
def get_resources_by_namespace(namespace):
    print(f"\nResources in namespace: {namespace}")

    # List Pods
    pods = v1.list_namespaced_pod(namespace)
    for pod in pods.items:
        print(f"Pod: {pod.metadata.name}, IP: {pod.status.pod_ip}")

    # List Services
    services = v1.list_namespaced_service(namespace)
    for service in services.items:
        print(f"Service: {service.metadata.name}, IP: {service.spec.cluster_ip}")

    # List Deployments
    deployments = apps_v1.list_namespaced_deployment(namespace)
    for deployment in deployments.items:
        print(f"Deployment: {deployment.metadata.name}, Replicas: {deployment.status.replicas}")

if __name__ == "__main__":
    # Example usages
    list_all_pods()
    list_all_services()
    list_all_deployments()
    list_all_nodes()
    get_resources_by_namespace('frontend')  # Replace 'frontend' with any namespace
```

### Explanation of Python Code

- **list_all_pods():** Lists all pods in all namespaces with their namespace, name, and IP.
- **list_all_services():** Lists all services in all namespaces with their namespace, name, and cluster IP.
- **list_all_deployments():** Lists all deployments in all namespaces with their namespace, name, and replicas.
- **list_all_nodes():** Lists all nodes with their name and IP.
- **get_resources_by_namespace(namespace):** Lists pods, services, and deployments in a specific namespace.

This cheat sheet provides a handy reference for interacting with Kubernetes resources via the Python client library. Adjust the functions as needed to fit your specific requirements.
