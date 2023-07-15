# Kubernetes Service Creation

## Introduction
This README provides step-by-step instructions on how to create and manage Kubernetes services. The instructions cover four specific questions related to creating and deleting services for pods. This guide accompanies a YouTube video tutorial demonstrating the practical implementation of these questions.

Video Tutorial: [Link to YouTube Video](https://youtu.be/YZ-jXnNw0sk)

### Question 1: Create two pods named "blue" and "red" using nginx image. The "blue" pod should be exposed on port 80.

To create execute the following commands:
```
kubectl run blue --image=nginx --port=80
kubectl run red --image=nginx
```

### Question 2: Create a nodeport service to expose the "blue" pod. The service should allow external access to the pod on the same port (port 80).

To create execute the following command:
```
kubectl expose pod blue --type=NodePort --port=80
```

### Question 3: Create a clusterip service to expose the "red" pod. This service allows internal access within the Kubernetes cluster.

To create execute the following command:
```
kubectl expose pod red --type=ClusterIP --port=80
```

### Question 4: Delete the nodeport service that was created for the "blue" pod.

To delete execute the following command:
```
kubectl delete service blue
```

### Question 5: Recreate a nodeport service for the "blue" pod, this time using the following custom port settings:
#### Port: 8080
#### NodePort: 32711
#### TargetPort: 80

To recreate execute the following command:
- Create a file named blue-service.yaml.
```
apiVersion: v1
kind: Service
metadata:
  name: blue-service
spec:
  selector:
    app: blue
  type: NodePort
  ports:
    - port: 8080
      targetPort: 80
      nodePort: 32711
```
- Apply the configuration using below command:
```
kubectl apply -f blue-service.yaml
```

This will create the NodePort service for the "blue" pod with the specified custom port settings.
