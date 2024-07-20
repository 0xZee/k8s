# K8S ARCHITECTURE

Sure! Below is an example of a Kubernetes (k8s) architecture with 3 namespaces and 6 deployments. This architecture includes a web application with a frontend, backend, and database components.

### Namespaces
1. **frontend**
2. **backend**
3. **database**

### Deployments
1. **frontend-deployment** in the `frontend` namespace
2. **backend-api-deployment** in the `backend` namespace
3. **backend-worker-deployment** in the `backend` namespace
4. **database-primary-deployment** in the `database` namespace
5. **database-replica-deployment** in the `database` namespace
6. **monitoring-deployment** in a new `monitoring` namespace (for monitoring purposes)

### YAML Definitions

#### 1. Namespace Definitions
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
  name: database
---
apiVersion: v1
kind: Namespace
metadata:
  name: monitoring
```

#### 2. Deployments

##### Frontend Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-deployment
  namespace: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
      - name: frontend
        image: frontend-image:latest
        ports:
        - containerPort: 80
```

##### Backend API Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-api-deployment
  namespace: backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: backend-api
  template:
    metadata:
      labels:
        app: backend-api
    spec:
      containers:
      - name: backend-api
        image: backend-api-image:latest
        ports:
        - containerPort: 8080
```

##### Backend Worker Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-worker-deployment
  namespace: backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: backend-worker
  template:
    metadata:
      labels:
        app: backend-worker
    spec:
      containers:
      - name: backend-worker
        image: backend-worker-image:latest
        ports:
        - containerPort: 8081
```

##### Database Primary Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: database-primary-deployment
  namespace: database
spec:
  replicas: 1
  selector:
    matchLabels:
      app: database-primary
  template:
    metadata:
      labels:
        app: database-primary
    spec:
      containers:
      - name: database-primary
        image: database-image:latest
        ports:
        - containerPort: 5432
```

##### Database Replica Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: database-replica-deployment
  namespace: database
spec:
  replicas: 2
  selector:
    matchLabels:
      app: database-replica
  template:
    metadata:
      labels:
        app: database-replica
    spec:
      containers:
      - name: database-replica
        image: database-image:latest
        ports:
        - containerPort: 5432
```

##### Monitoring Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: monitoring-deployment
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: monitoring
  template:
    metadata:
      labels:
        app: monitoring
    spec:
      containers:
      - name: monitoring
        image: monitoring-image:latest
        ports:
        - containerPort: 9090
```

### Services

#### Frontend Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: frontend-service
  namespace: frontend
spec:
  selector:
    app: frontend
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

#### Backend API Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend-api-service
  namespace: backend
spec:
  selector:
    app: backend-api
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
```

#### Backend Worker Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend-worker-service
  namespace: backend
spec:
  selector:
    app: backend-worker
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
```

#### Database Primary Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: database-primary-service
  namespace: database
spec:
  selector:
    app: database-primary
  ports:
    - protocol: TCP
      port: 5432
      targetPort: 5432
```

#### Database Replica Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: database-replica-service
  namespace: database
spec:
  selector:
    app: database-replica
  ports:
    - protocol: TCP
      port: 5432
      targetPort: 5432
```

#### Monitoring Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: monitoring-service
  namespace: monitoring
spec:
  selector:
    app: monitoring
  ports:
    - protocol: TCP
      port: 9090
      targetPort: 9090
```

### Ingress (Optional)

To expose the frontend application to the internet, you can use an Ingress resource.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: frontend-ingress
  namespace: frontend
spec:
  rules:
  - host: mywebapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: frontend-service
            port:
              number: 80
```

This configuration sets up a basic Kubernetes architecture with separate namespaces for frontend, backend, and database components, along with monitoring. Each namespace contains specific deployments and services to manage and expose the different parts of the application.

---
# K8S RESOURCES

Sure! Below are example outputs you might see when running the equivalent `kubectl get` commands. These outputs are illustrative and show typical data you might encounter in a Kubernetes cluster.

### 1. List all namespaces
```yaml
$ kubectl get namespaces
NAME              STATUS   AGE
default           Active   23d
frontend          Active   21d
backend           Active   21d
database          Active   21d
monitoring        Active   20d
kube-system       Active   23d
kube-public       Active   23d
kube-node-lease   Active   23d
```

### 2. List all pods in a namespace
```yaml
$ kubectl get pods -n frontend
NAME                                  READY   STATUS    RESTARTS   AGE
frontend-deployment-5b9c8d9d8d-8rjng  1/1     Running   0          5h
frontend-deployment-5b9c8d9d8d-c3vbs  1/1     Running   0          5h
frontend-deployment-5b9c8d9d8d-r8x9k  1/1     Running   0          5h

$ kubectl get pods -n backend
NAME                                      READY   STATUS    RESTARTS   AGE
backend-api-deployment-7f96c8b5d8-4k2fr   1/1     Running   0          6h
backend-api-deployment-7f96c8b5d8-5s8gb   1/1     Running   0          6h
backend-api-deployment-7f96c8b5d8-p7h9k   1/1     Running   0          6h
backend-worker-deployment-2h96f8f6d8-k1x4 1/1     Running   0          6h
backend-worker-deployment-2h96f8f6d8-m4g6 1/1     Running   0          6h
backend-worker-deployment-2h96f8f6d8-q7v5 1/1     Running   0          6h

$ kubectl get pods -n database
NAME                                         READY   STATUS    RESTARTS   AGE
database-primary-deployment-0                1/1     Running   0          7h
database-replica-deployment-5c96d9d7f8-9xv3n 1/1     Running   0          7h
database-replica-deployment-5c96d9d7f8-c5h6v 1/1     Running   0          7h
```

### 3. List all services in a namespace
```yaml
$ kubectl get svc -n frontend
NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
frontend-service   ClusterIP   10.96.153.216    <none>        80/TCP    21d

$ kubectl get svc -n backend
NAME                   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
backend-api-service    ClusterIP   10.96.154.217    <none>        8080/TCP   21d
backend-worker-service ClusterIP   10.96.155.218    <none>        8081/TCP   21d

$ kubectl get svc -n database
NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
database-primary-service  ClusterIP   10.96.156.219    <none>        5432/TCP   21d
database-replica-service  ClusterIP   10.96.157.220    <none>        5432/TCP   21d
```

### 4. List all deployments in a namespace
```yaml
$ kubectl get deployments -n frontend
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
frontend-deployment   3/3     3            3           21d

$ kubectl get deployments -n backend
NAME                     READY   UP-TO-DATE   AVAILABLE   AGE
backend-api-deployment   3/3     3            3           21d
backend-worker-deployment3/3     3            3           21d

$ kubectl get deployments -n database
NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
database-primary-deployment  1/1     1            1           21d
database-replica-deployment  2/2     2            2           21d
```

### 5. List all replica sets in a namespace
```yaml
$ kubectl get rs -n frontend
NAME                             DESIRED   CURRENT   READY   AGE
frontend-deployment-5b9c8d9d8d   3         3         3       21d

$ kubectl get rs -n backend
NAME                                DESIRED   CURRENT   READY   AGE
backend-api-deployment-7f96c8b5d8   3         3         3       21d
backend-worker-deployment-2h96f8f6d8 3        3         3       21d

$ kubectl get rs -n database
NAME                                  DESIRED   CURRENT   READY   AGE
database-primary-deployment-7f96c8b5d8 1        1         1       21d
database-replica-deployment-5c96d9d7f8 2        2         2       21d
```

### 6. List all stateful sets in a namespace
```bash
$ kubectl get statefulsets -n frontend
No resources found in frontend namespace.

$ kubectl get statefulsets -n backend
No resources found in backend namespace.

$ kubectl get statefulsets -n database
NAME                         READY   AGE
database-primary-deployment  1/1     21d
database-replica-deployment  2/2     21d
```

### 7. List all daemon sets in a namespace
```bash
$ kubectl get daemonsets -n frontend
No resources found in frontend namespace.

$ kubectl get daemonsets -n backend
No resources found in backend namespace.

$ kubectl get daemonsets -n database
No resources found in database namespace.

$ kubectl get daemonsets -n monitoring
NAME               DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
monitoring-daemon  1         1         1       1            1           <none>          20d
```


These examples show the type of output you can expect when running the corresponding `kubectl get` commands for different Kubernetes resources within various namespaces. The actual output will vary based on the specific configuration and state of your Kubernetes cluster.

---


Certainly! Below is a Python script using the `kubernetes` Python client library to list all resources and to list resources for a specific namespace. I've included detailed comments to explain each part of the code.

First, ensure you have the `kubernetes` Python client installed:
```bash
pip install kubernetes
```

Here's the Python script:

```python
from kubernetes import client, config

# Load the kubeconfig file (usually located at ~/.kube/config)
config.load_kube_config()

# Create the API clients
v1 = client.CoreV1Api()
apps_v1 = client.AppsV1Api()

def list_all_resources():
    """
    Lists all resources in all namespaces.
    """

    # List all namespaces
    namespaces = v1.list_namespace()
    for ns in namespaces.items:
        namespace = ns.metadata.name
        print(f"\nResources in namespace: {namespace}")

        # List all pods in the namespace
        pods = v1.list_namespaced_pod(namespace)
        print("\nPods:")
        for pod in pods.items:
            print(f" - {pod.metadata.name}")

        # List all services in the namespace
        services = v1.list_namespaced_service(namespace)
        print("\nServices:")
        for svc in services.items:
            print(f" - {svc.metadata.name}")

        # List all deployments in the namespace
        deployments = apps_v1.list_namespaced_deployment(namespace)
        print("\nDeployments:")
        for deploy in deployments.items:
            print(f" - {deploy.metadata.name}")

        # List all replica sets in the namespace
        replicasets = apps_v1.list_namespaced_replica_set(namespace)
        print("\nReplica Sets:")
        for rs in replicasets.items:
            print(f" - {rs.metadata.name}")

        # List all stateful sets in the namespace
        statefulsets = apps_v1.list_namespaced_stateful_set(namespace)
        print("\nStateful Sets:")
        for ss in statefulsets.items:
            print(f" - {ss.metadata.name}")

        # List all daemon sets in the namespace
        daemonsets = apps_v1.list_namespaced_daemon_set(namespace)
        print("\nDaemon Sets:")
        for ds in daemonsets.items:
            print(f" - {ds.metadata.name}")

def list_resources_for_namespace(namespace):
    """
    Lists all resources in a specified namespace.
    """

    print(f"\nResources in namespace: {namespace}")

    # List all pods in the namespace
    pods = v1.list_namespaced_pod(namespace)
    print("\nPods:")
    for pod in pods.items:
        print(f" - {pod.metadata.name}")

    # List all services in the namespace
    services = v1.list_namespaced_service(namespace)
    print("\nServices:")
    for svc in services.items:
        print(f" - {svc.metadata.name}")

    # List all deployments in the namespace
    deployments = apps_v1.list_namespaced_deployment(namespace)
    print("\nDeployments:")
    for deploy in deployments.items:
        print(f" - {deploy.metadata.name}")

    # List all replica sets in the namespace
    replicasets = apps_v1.list_namespaced_replica_set(namespace)
    print("\nReplica Sets:")
    for rs in replicasets.items:
        print(f" - {rs.metadata.name}")

    # List all stateful sets in the namespace
    statefulsets = apps_v1.list_namespaced_stateful_set(namespace)
    print("\nStateful Sets:")
    for ss in statefulsets.items:
        print(f" - {ss.metadata.name}")

    # List all daemon sets in the namespace
    daemonsets = apps_v1.list_namespaced_daemon_set(namespace)
    print("\nDaemon Sets:")
    for ds in daemonsets.items:
        print(f" - {ds.metadata.name}")

if __name__ == "__main__":
    # List all resources in all namespaces
    list_all_resources()

    # List resources in a specific namespace (e.g., 'frontend')
    list_resources_for_namespace('frontend')
```

### Explanation of the Script:

1. **Importing the necessary libraries**:
    ```python
    from kubernetes import client, config
    ```

2. **Loading the kubeconfig**:
    ```python
    config.load_kube_config()
    ```

3. **Creating the API clients**:
    ```python
    v1 = client.CoreV1Api()
    apps_v1 = client.AppsV1Api()
    ```

4. **Defining the function to list all resources in all namespaces**:
    ```python
    def list_all_resources():
    ```

5. **Defining the function to list resources in a specified namespace**:
    ```python
    def list_resources_for_namespace(namespace):
    ```

6. **Using the functions to list resources**:
    ```python
    if __name__ == "__main__":
        list_all_resources()
        list_resources_for_namespace('frontend')
    ```

### Equivalent `kubectl get` Commands

The Python script performs equivalent operations to the following `kubectl` commands:

- List all namespaces:
  ```bash
  kubectl get namespaces
  ```

- List all pods in a namespace:
  ```bash
  kubectl get pods -n <namespace>
  ```

- List all services in a namespace:
  ```bash
  kubectl get svc -n <namespace>
  ```

- List all deployments in a namespace:
  ```bash
  kubectl get deployments -n <namespace>
  ```

- List all replica sets in a namespace:
  ```bash
  kubectl get rs -n <namespace>
  ```

- List all stateful sets in a namespace:
  ```bash
  kubectl get statefulsets -n <namespace>
  ```

- List all daemon sets in a namespace:
  ```bash
  kubectl get daemonsets -n <namespace>
  ```

By running the Python script, you can automate the process of listing Kubernetes resources in all namespaces or in a specific namespace, similar to using `kubectl get` commands.
