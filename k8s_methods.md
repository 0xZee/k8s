# 0 Kubernetes Python API v1 Client : `list_ methods`
---

```python
from kubernetes import client, config

# Set the config file
config.load_kube_config()  # Load from kubeconfig file in your home directory (~/.kube/config)
# OR
config.load_incluster_config()  # Load from within a Kubernetes cluster

# Core V1 API
v1 = client.CoreV1Api()

# --- Namespaces ---

# Return : list of all namespaces
# Input : None
list_of_namespaces = v1.list_namespace()

# --- Events ---

# Return : list of all events in a specific namespace
# Input : namespace
list_of_events = v1.list_namespace_event(namespace="default")

# --- Nodes ---

# Return : list of all nodes
# Input : None
list_of_nodes = v1.list_node()

# --- Pods ---

# Return : list of all pods across all namespaces
# Input : None
list_of_pods_all_namespaces = v1.list_pod_for_all_namespaces()

# Return : list of all the pods in a specific namespace
# Input : namespace
pods_ns = v1.list_namespaced_pod(namespace="default")

# --- Services ---

# Return : list of all services across all namespaces
# Input : None
list_of_services_all_namespaces = v1.list_service_for_all_namespaces()

# Return : list of all the services in a specific namespace
# Input : namespace
services_ns = v1.list_namespaced_service(namespace="default")

# --- Config Maps ---

# Return : list of all the config maps in a specific namespace
# Input : namespace
config_maps_ns = v1.list_namespaced_config_map(namespace="default")

# --- Secrets ---

# Return : list of all the secrets in a specific namespace
# Input : namespace
secrets_ns = v1.list_namespaced_secret(namespace="default")

# --- Persistent Volume Claims ---

# Return : list of all the persistent volume claims in a specific namespace
# Input : namespace
pvc_ns = v1.list_namespaced_persistent_volume_claim(namespace="default")

# --- Ingresses ---

# Return : list of all the ingresses in a specific namespace
# Input : namespace
ingresses_ns = v1.list_namespaced_ingress(namespace="default")

# --- Jobs ---

# Return : list of all the jobs in a specific namespace
# Input : namespace
jobs_ns = v1.list_namespaced_job(namespace="default")

# --- Cron Jobs ---

# Return : list of all the cron jobs in a specific namespace
# Input : namespace
cron_jobs_ns = v1.list_namespaced_cron_job(namespace="default")

# --- Read Methods for CoreV1Api ---

# Return : details of a specific namespace
# Input : namespace
read_namespace = v1.read_namespace(name="default")

# Return : details of a specific node
# Input : node_name
read_node = v1.read_node(name="your-node-name")

# Return : details of a specific pod
# Input : pod_name, namespace
read_pod = v1.read_namespaced_pod(name="your-pod-name", namespace="default")

# Return : details of a specific service
# Input : service_name, namespace
read_service = v1.read_namespaced_service(name="your-service-name", namespace="default")

# Return : details of a specific config map
# Input : config_map_name, namespace
read_config_map = v1.read_namespaced_config_map(name="your-config-map-name", namespace="default")

# Return : details of a specific secret
# Input : secret_name, namespace
read_secret = v1.read_namespaced_secret(name="your-secret-name", namespace="default")

# Return : details of a specific persistent volume claim
# Input : pvc_name, namespace
read_pvc = v1.read_namespaced_persistent_volume_claim(name="your-pvc-name", namespace="default")

# Return : details of a specific ingress
# Input : ingress_name, namespace
read_ingress = v1.read_namespaced_ingress(name="your-ingress-name", namespace="default")

# Return : details of a specific job
# Input : job_name, namespace
read_job = v1.read_namespaced_job(name="your-job-name", namespace="default")

# Return : details of a specific cron job
# Input : cron_job_name, namespace
read_cron_job = v1.read_namespaced_cron_job(name="your-cron-job-name", namespace="default")

# --- Apps V1 API ---

apps_v1 = client.AppsV1Api()

# --- Deployments ---

# Return : list of all deployments across all namespaces
# Input : None
list_of_deployments_all_namespaces = apps_v1.list_deployment_for_all_namespaces()

# Return : list of all the deployments in a specific namespace
# Input : namespace
deployments_ns = apps_v1.list_namespaced_deployment(namespace="default")

# --- Replica Sets ---

# Return : list of all the replica sets in a specific namespace
# Input : namespace
replica_sets_ns = apps_v1.list_namespaced_replica_set(namespace="default")

# --- Stateful Sets ---

# Return : list of all the stateful sets in a specific namespace
# Input : namespace
stateful_sets_ns = apps_v1.list_namespaced_stateful_set(namespace="default")

# --- Daemon Sets ---

# Return : list of all the daemon sets in a specific namespace
# Input : namespace
daemon_sets_ns = apps_v1.list_namespaced_daemon_set(namespace="default")

# --- Batch V1 API ---

batch_v1 = client.BatchV1Api()

# --- Jobs ---

# Return : list of all jobs across all namespaces
# Input : None
list_of_jobs_all_namespaces = batch_v1.list_job_for_all_namespaces()

# Return : list of all the jobs in a specific namespace
# Input : namespace
jobs_ns = batch_v1.list_namespaced_job(namespace="default")

# --- Cron Jobs ---

# Return : list of all cron jobs across all namespaces
# Input : None
list_of_cron_jobs_all_namespaces = batch_v1.list_cron_job_for_all_namespaces()

# Return : list of all the cron jobs in a specific namespace
# Input : namespace
cron_jobs_ns = batch_v1.list_namespaced_cron_job(namespace="default")

# --- RBAC Authorization V1 API ---

rbac_v1 = client.RbacAuthorizationV1Api()

# --- Cluster Roles ---

# Return : list of all cluster roles
# Input : None
list_of_cluster_roles = rbac_v1.list_cluster_role()

# --- Cluster Role Bindings ---

# Return : list of all cluster role bindings
# Input : None
list_of_cluster_role_bindings = rbac_v1.list_cluster_role_binding()

# --- Roles ---

# Return : list of all the roles in a specific namespace
# Input : namespace
roles_ns = rbac_v1.list_namespaced_role(namespace="default")

# --- Role Bindings ---

# Return : list of all the role bindings in a specific namespace
# Input : namespace
role_bindings_ns = rbac_v1.list_namespaced_role_binding(namespace="default")

# --- Custom Objects API ---

custom_objects = client.CustomObjectsApi()

# --- Custom Objects ---

# Return : list of all custom objects at the cluster level
# Input : group, version, plural
list_of_cluster_custom_objects = custom_objects.list_cluster_custom_object(group="your-group", version="your-version", plural="your-plural")

# Return : list of all the custom objects in a specific namespace
# Input : group, version, plural, namespace
list_of_namespaced_custom_objects = custom_objects.list_namespaced_custom_object(group="your-group", version="your-version", plural="your-plural", namespace="default")

# --- Read Methods for CustomObjectsApi ---

# Return : details of a specific custom object at the cluster level
# Input : group, version, plural, name
read_cluster_custom_object = custom_objects.get_cluster_custom_object(group="your-group", version="your-version", plural="your-plural", name="your-custom-object-name")

# Return : details of a specific custom object in a namespace
# Input : group, version, plural, name, namespace
read_namespaced_custom_object = custom_objects.get_namespaced_custom_object(group="your-group", version="your-version", plural="your-plural", name="your-custom-object-name", namespace="default")
```

**Explanation:**

- **Comments:** Each code snippet is now preceded by a comment explaining the purpose of the method and its required input parameters.
- **Consistent Format:** The code follows a consistent format, making it easier to read and understand.
- **Placeholders:** Remember to replace placeholders like `'your-group'`, `'your-version'`, `'your-plural'`, `'your-node-name'`, `'your-pod-name'`, etc., with the actual values for your specific Kubernetes cluster and resources.

This code provides a structured and well-documented list of `list_` and `read_` methods for managing Kubernetes resources using the Python client library. You can easily adapt this code to your specific needs by replacing the placeholders and using the appropriate methods for the resources you want to manage.

# 1 Kubernetes Python Client Methods
---

Certainly! Let me provide you with a plain explanation first, and then I'll give you the Python code listing the methods with explanations in comments.

Plain explanation:
The Kubernetes Python client provides various APIs to interact with different aspects of a Kubernetes cluster. The CoreV1Api is one of the most commonly used APIs, but there are several others available. Each API provides a set of methods to perform operations on specific Kubernetes resources.

Some of the main APIs include:
1. CoreV1Api: For core Kubernetes resources like pods, services, and namespaces.
2. AppsV1Api: For managing deployments, statefulsets, and daemonsets.
3. BatchV1Api: For jobs and cronjobs.
4. RbacAuthorizationV1Api: For role-based access control (RBAC) resources.
5. CustomObjectsApi: For working with custom resources.

Each of these APIs has numerous methods for listing, creating, updating, and deleting resources, as well as for performing specific operations on these resources.

Now, let me provide you with Python code listing some of the most commonly used methods for these APIs, along with explanations in comments. Note that this is not an exhaustive list, as there are many methods available for each API.

```python
from kubernetes import client, config

config.load_kube_config()

# Core V1 API
v1 = client.CoreV1Api()

# List methods for CoreV1Api
core_methods = [
    v1.list_namespace,  # List all namespaces in the cluster
    v1.list_namespace_event,  # List events in a specific namespace
    v1.list_node,  # List all nodes in the cluster
    v1.list_pod_for_all_namespaces,  # List pods across all namespaces
    v1.list_service_for_all_namespaces,  # List services across all namespaces
    v1.read_namespace,  # Read a specific namespace
    v1.create_namespace,  # Create a new namespace
    v1.delete_namespace,  # Delete a namespace
    v1.read_node,  # Read details of a specific node
    v1.create_namespaced_pod,  # Create a pod in a specific namespace
    v1.read_namespaced_pod,  # Read details of a specific pod
    v1.delete_namespaced_pod,  # Delete a pod in a specific namespace
    v1.create_namespaced_service,  # Create a service in a specific namespace
    v1.read_namespaced_service,  # Read details of a specific service
    v1.delete_namespaced_service,  # Delete a service in a specific namespace
]

# Apps V1 API
apps_v1 = client.AppsV1Api()

# List methods for AppsV1Api
apps_methods = [
    apps_v1.list_deployment_for_all_namespaces,  # List deployments across all namespaces
    apps_v1.list_namespaced_deployment,  # List deployments in a specific namespace
    apps_v1.read_namespaced_deployment,  # Read details of a specific deployment
    apps_v1.create_namespaced_deployment,  # Create a deployment in a specific namespace
    apps_v1.delete_namespaced_deployment,  # Delete a deployment in a specific namespace
    apps_v1.list_namespaced_replica_set,  # List replica sets in a specific namespace
    apps_v1.list_namespaced_stateful_set,  # List stateful sets in a specific namespace
    apps_v1.list_namespaced_daemon_set,  # List daemon sets in a specific namespace
]

# Batch V1 API
batch_v1 = client.BatchV1Api()

# List methods for BatchV1Api
batch_methods = [
    batch_v1.list_job_for_all_namespaces,  # List jobs across all namespaces
    batch_v1.list_namespaced_job,  # List jobs in a specific namespace
    batch_v1.read_namespaced_job,  # Read details of a specific job
    batch_v1.create_namespaced_job,  # Create a job in a specific namespace
    batch_v1.delete_namespaced_job,  # Delete a job in a specific namespace
    batch_v1.list_cron_job_for_all_namespaces,  # List cron jobs across all namespaces
    batch_v1.list_namespaced_cron_job,  # List cron jobs in a specific namespace
]

# RBAC Authorization V1 API
rbac_v1 = client.RbacAuthorizationV1Api()

# List methods for RbacAuthorizationV1Api
rbac_methods = [
    rbac_v1.list_cluster_role,  # List all cluster roles
    rbac_v1.list_cluster_role_binding,  # List all cluster role bindings
    rbac_v1.list_namespaced_role,  # List roles in a specific namespace
    rbac_v1.list_namespaced_role_binding,  # List role bindings in a specific namespace
    rbac_v1.create_cluster_role,  # Create a cluster role
    rbac_v1.create_cluster_role_binding,  # Create a cluster role binding
    rbac_v1.create_namespaced_role,  # Create a role in a specific namespace
    rbac_v1.create_namespaced_role_binding,  # Create a role binding in a specific namespace
]

# Custom Objects API
custom_objects = client.CustomObjectsApi()

# List methods for CustomObjectsApi
custom_methods = [
    custom_objects.list_cluster_custom_object,  # List custom objects at the cluster level
    custom_objects.list_namespaced_custom_object,  # List custom objects in a specific namespace
    custom_objects.get_cluster_custom_object,  # Get a specific custom object at the cluster level
    custom_objects.get_namespaced_custom_object,  # Get a specific custom object in a namespace
    custom_objects.create_cluster_custom_object,  # Create a custom object at the cluster level
    custom_objects.create_namespaced_custom_object,  # Create a custom object in a specific namespace
    custom_objects.delete_cluster_custom_object,  # Delete a custom object at the cluster level
    custom_objects.delete_namespaced_custom_object,  # Delete a custom object in a specific namespace
]
```

This code provides an overview of some of the most commonly used methods for each API. Each method is accompanied by a comment explaining its purpose. Remember that there are many more methods available for each API, and you can explore them further in the Kubernetes Python client documentation or by using code completion in your IDE.


# 2 Kubernetes Python Client Methods
---

The Kubernetes Python client allows you to interact with your K8s cluster programmatically. After loading your K8s configuration with `config.load_kube_config()`, you can access various API classes to manage different resources. Here's a breakdown of some key APIs and their methods, along with explanations.

## CoreV1Api

This API is used for core K8s resources like Pods, Services, and Namespaces.

### Common Methods

```python
from kubernetes import client, config

config.load_kube_config()
v1 = client.CoreV1Api()

# Get a list of all Pods in a specific namespace
pods = v1.list_namespaced_pod(namespace='default')  # List all Pods in 'default' namespace

# Get a specific Pod by name
pod = v1.read_namespaced_pod(name='pod-name', namespace='default')  # Get details of a specific Pod

# Create a new Pod
v1.create_namespaced_pod(namespace='default', body=pod_body)  # pod_body is a Pod object

# Delete a specific Pod
v1.delete_namespaced_pod(name='pod-name', namespace='default')  # Delete a Pod by name

# Get a list of all Services in a specific namespace
services = v1.list_namespaced_service(namespace='default')  # List all Services in 'default'

# Get a specific Service by name
service = v1.read_namespaced_service(name='service-name', namespace='default')  # Get details of a Service

# Create a new Service
v1.create_namespaced_service(namespace='default', body=service_body)  # service_body is a Service object

# Delete a specific Service
v1.delete_namespaced_service(name='service-name', namespace='default')  # Delete a Service by name

# Get a list of all Namespaces
namespaces = v1.list_namespace()  # List all Namespaces

# Get a specific Namespace by name
namespace = v1.read_namespace(name='namespace-name')  # Get details of a specific Namespace
```

## AppsV1Api

This API is used for managing applications, including Deployments and StatefulSets.

### Common Methods

```python
apps_v1 = client.AppsV1Api()

# Get a list of all Deployments in a specific namespace
deployments = apps_v1.list_namespaced_deployment(namespace='default')  # List all Deployments

# Get a specific Deployment by name
deployment = apps_v1.read_namespaced_deployment(name='deployment-name', namespace='default')  # Get details of a Deployment

# Create a new Deployment
apps_v1.create_namespaced_deployment(namespace='default', body=deployment_body)  # deployment_body is a Deployment object

# Delete a specific Deployment
apps_v1.delete_namespaced_deployment(name='deployment-name', namespace='default')  # Delete a Deployment

# Get a list of all StatefulSets in a specific namespace
statefulsets = apps_v1.list_namespaced_stateful_set(namespace='default')  # List StatefulSets
```

## NetworkingV1Api

This API is for managing network resources like Ingress and NetworkPolicies.

### Common Methods

```python
networking_v1 = client.NetworkingV1Api()

# Get a list of all Ingresses in a specific namespace
ingresses = networking_v1.list_namespaced_ingress(namespace='default')  # List Ingress resources

# Get a specific Ingress by name
ingress = networking_v1.read_namespaced_ingress(name='ingress-name', namespace='default')  # Get details of an Ingress

# Create a new Ingress
networking_v1.create_namespaced_ingress(namespace='default', body=ingress_body)  # ingress_body is an Ingress object

# Delete a specific Ingress
networking_v1.delete_namespaced_ingress(name='ingress-name', namespace='default')  # Delete an Ingress
```

## Summary

- **CoreV1Api**: Manages core resources like Pods, Services, and Namespaces.
- **AppsV1Api**: Manages application resources like Deployments and StatefulSets.
- **NetworkingV1Api**: Manages network resources like Ingress and NetworkPolicies.

These methods allow for comprehensive control over your Kubernetes resources through Python. You can perform CRUD (Create, Read, Update, Delete) operations on various K8s components, enabling automation and integration into your applications.
