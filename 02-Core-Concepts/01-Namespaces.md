# Kubernetes Namespace Explained

## What is a Namespace?

A **Namespace** in Kubernetes is a logical partition used to divide cluster resources among multiple users or teams. It helps isolate and manage resources more effectively within the same cluster.

---

## Why Use Namespaces?

Namespaces are especially useful in:

- Multi-team environments: Prevents teams from interfering with each other’s resources.
- Environment separation: Separate dev, staging, and prod environments.
- Resource organization: Makes it easier to manage and monitor grouped resources.

---

## Key Characteristics

- Each resource in Kubernetes belongs to a namespace (except cluster-wide resources like Nodes, PersistentVolumes).
- You can apply resource quotas and policies at the namespace level.
- Namespaces come with their own service discovery scope.

---

## Common Use Cases

- Creating isolated environments for CI/CD pipelines
- Running multiple versions of an application side-by-side
- Assigning different RBAC rules for different teams or workloads

---

## Default Namespaces Created when Kubernetes enabled

- `default`: The default namespace for objects without a namespace
- `kube-system`: Used for Kubernetes system components
- `kube-public`: Readable by all users (public cluster info)
- `kube-node-lease`: Tracks node heartbeat for faster failure detection

---

## Basic Commands

```sh
# Create a new namespace
kubectl create namespace dev

# List all namespaces
kubectl get namespaces

NAME              STATUS   AGE
default           Active   1d
kube-node-lease   Active   1d
kube-public       Active   1d
kube-system       Active   1d


# Run a pod in a specific namespace
kubectl run nginx --image=nginx -n dev

# Set the current namespace context
kubectl config set-context --current --namespace=dev

kubectl delete namespace dev

kubectl delete namespace qa prod
```

---

## YAML Definition Example

namespace.yaml
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
---
apiVersion: v1
kind: Namespace
metadata:
  name: qa
---
apiVersion: v1
kind: Namespace
metadata:
  name: prod


kubectl apply -f namespace.yaml
```
---

## Best Practices

- Use meaningful and consistent naming conventions.
- Apply RBAC and NetworkPolicies to secure namespaces.
- Avoid using `default` namespace for production workloads.
- Use labels and annotations for better visibility and automation.

---

## Conclusion

Namespaces are a powerful way to logically separate and manage Kubernetes workloads. They are essential for scaling, security, and team collaboration in larger clusters.

