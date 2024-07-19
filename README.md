# k8s
---
## Kubernetes Python CheatSheet

### `K8S PYTHON MONITORING` : [K8S Python](k8s_monitoring.md)
`kubectl` vs `API Calls`

### `K8S PYTHON API METHODS` : [K8S API](k8s_methods.md)

---
## Kubernetes Simple Architecture Build and monitoring

### `CHATGPT 4o Mini` : [K8S ARCHITECTURE (Streamlit, nginx, mongodb)](k8s_simple_mini.md)
### `CLAUDE SONNET 3.5` : [K8S ARCHITECTURE (Streamlit, nginx, mongodb)](k8s_simple_sonnet.md)
### `CHATGPT 4o` : [K8S ARCHITECTURE (Streamlit, nginx, mongodb)](k8s_simple_gpt.md)

---

## Kubernetes Simple Architecture Build and monitoring

[K8S ARCHITECTURE (WebService, LoadBalancing, DataBases, MonitoringTools](k8s_build.md)

---

# Kubernetes API v1 Client 

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

