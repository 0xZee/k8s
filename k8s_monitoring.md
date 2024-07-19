# k8s API Method

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


# kubctl Method

```python

import argparse
import subprocess

def get_resources(namespace):
    command = f"kubectl get all -n {namespace}"
    result = subprocess.run(command, shell=True, capture_output=True, text=True)
    return result.stdout

def list_namespaces():
    command = "kubectl get namespaces"
    result = subprocess.run(command, shell=True, capture_output=True, text=True)
    return result.stdout

def list_services():
    command = "kubectl get services"
    result = subprocess.run(command, shell=True, capture_output=True, text=True)
    return result.stdout

def cheatsheet():
    command = "kubectl cheatsheet"
    result = subprocess.run(command, shell=True, capture_output=True, text=True)
    return result.stdout

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Monitor K8s resources")
    parser.add_argument("--namespace", help="Namespace to filter resources", default=None)
    args = parser.parse_args()

    if args.namespace:
        resources = get_resources(args.namespace)
    else:
        resources = get_resources("default")

    print(resources)
```
