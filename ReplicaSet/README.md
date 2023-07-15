# Replicaset Creation

## Introduction
This README provides a step-by-step guide to create and manage a Replicaset in Kubernetes. It covers the creation of a Replicaset using the declarative approach, scaling the Replicaset imperatively, deleting a pod from the Replicaset, and finally, deleting the entire Replicaset. 

The instructions mentioned in this readme are based on a practical demonstration given in the following YouTube video: [Link to Video](https://youtu.be/ODJwFsdK2oU).

### Question 1: Create a Replicaset with 1 replica
To create a Replicaset named "myfirstrs" with the Nginx image and 1 replica using the declarative way, follow these steps:

- Create a YAML file, e.g., myfirstrs.yaml.
- Open the file and add the following YAML content:
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myfirstrs
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myfirstrs
  template:
    metadata:
      labels:
        app: myfirstrs
    spec:
      containers:
      - name: nginx
        image: nginx
```

- Save the file and apply the configuration using the following command:
```
kubectl apply -f myfirstrs.yaml
```

### Question 2: Scale the Replicaset to 5 pods
To scale the Replicaset named "myfirstrs" to 5 pods using the imperative way, execute the following command:
```
kubectl scale replicaset myfirstrs --replicas=5
```

### Question 3: Delete one of the pods
To delete one of the pods from the Replicaset, you can choose any of the pods in the Replicaset and delete it manually. Use the following command to list the pods:
```
kubectl get pods
```

- Once you have identified the pod you want to delete, use the following command:
```
kubectl delete pod <pod-name>
```
- Replace <pod-name> with the name of the pod you wish to delete.

### Question 4: Delete the Replicaset
To delete the entire Replicaset named "myfirstrs," execute the following command:
```
kubectl delete replicaset myfirstrs
```
This command will delete the Replicaset and all associated pods.
