# NodeSelector in Kubernetes
This readme provides a quick recap of NodeSelector in Kubernetes, including practical examples and questions.

## Practical Questions and Answers
### Question 1: Label the node with key=capacity and value=low
To label a node with the key "capacity" and value "low," use the following command:
```
kubectl label nodes <node-name> capacity=low
```

### Question 2: Create a pod and use NodeSelector to schedule it onto the labeled node
To create a pod and schedule it onto a labeled node using NodeSelector, follow these steps:

- Create a YAML file with the following content:
```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: my-image
  nodeSelector:
    capacity: low
```

- Apply the YAML file using the following command:
```
kubectl apply -f pod.yaml
```

## Additional Commands
- To verify the node labels, use the following command:
```
kubectl get node --show-labels
```
This command will display a list of nodes along with their labels.

## Additional Practical Questions
### Question1 : Label all nodes in your Kubernetes cluster with a key-value pair "environment=production".
To label all nodes with the key-value pair "environment=production" use the following command:
```
kubectl label nodes --all environment=production
```

### Question2 : How can you remove a label from a node?
To remove a label from a node use the kubectl label command with the key and node name. For example:
```
kubectl label node <node-name> capacity-
```
