# Kubernetes RBAC Setup

This guide provides instructions for creating roles, cluster roles, role bindings, and cluster role bindings in a Kubernetes cluster. RBAC (Role-Based Access Control) allows you to control access to resources within the cluster based on user roles and permissions.

## Role
The role.yaml file contains the configuration for creating a role named pod-reader. The role allows the user to perform actions like get, watch, and list on pods resources.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]

```

### To apply this role:

```
kubectl apply -f role.yaml
```

### To check the created role:
```
kubectl get role
```

## Role Binding
The rolebinding.yaml file defines a role binding named read-pods that binds the pod-reader role to the user jack in the default namespace.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: jack
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io

```

### To apply this role binding:

```
kubectl apply -f rolebinding.yaml
```

### To check the created role binding:

```
kubectl get rolebinding
```

### To check the permissions of the jack user:

```
kubectl auth can-i get pod --as jack
```

## Cluster Role
The clusterrole.yaml file contains the configuration for creating a cluster role named secret-reader. This cluster role allows the user to perform actions like get, watch, and list on secrets resources.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: secret-reader
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "watch", "list"]

```

### To apply this cluster role:

```
kubectl apply -f clusterrole.yaml
```

### To check the created cluster role:

```
kubectl get clusterrole
```

## Role Binding (Namespace-level)
The rolebinding.yaml file defines a role binding named read-secrets that binds the secret-reader cluster role to the user dev in the development namespace.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-secrets
  namespace: development
subjects:
- kind: User
  name: dev
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io

```

### To apply this role binding:

```
kubectl apply -f rolebinding.yaml
```

### To check the created role binding:

```
kubectl get rolebinding
```

### To check the permissions of the dev user in the development namespace:

```
kubectl auth can-i get secret --as dev -n development
```

## Cluster Role Binding
The clusterrolebinding.yaml file contains the configuration for creating a cluster role binding named read-secrets-global. This cluster role binding binds the secret-reader cluster role to the user riya globally.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-secrets-global
subjects:
- kind: User
  name: riya
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io

```

### To apply this cluster role binding:

```
kubectl apply -f clusterrolebinding.yaml
```

### To check the created cluster role binding:

```
kubectl get clusterrolebinding
```

### To check the permissions of the riya user across all namespaces:

```
kubectl auth can-i get secret --as riya -A
```

## Conclusion
In this guide, we have learned how to implement RBAC (Role-Based Access Control) in a Kubernetes cluster by creating roles, cluster roles, role bindings, and cluster role bindings. By applying the provided YAML files and using the kubectl commands, you can easily set up and manage access control and permissions for users within your Kubernetes environment. 
