# Kubernetes Manual Scheduling using nodename Property

## Introduction
This readme file provides instructions on manually scheduling Kubernetes pods using the nodename property.  Please refer to the following YouTube video for a practical demonstration of the concepts discussed in this readme: 

YouTube Video: [Manual Scheduling in Kubernetes](https://youtu.be/ARHfMpiBv-4)

### Question 1: Create a pod named mypod and manually schedule it onto the master node. 
- Create a file named mypod.yaml.
```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  labels:
    color: blue
spec:
  nodeName: master
  containers:
  - name: mycontainer
    image: nginx
```

- Apply the pod manifest using the following command:
```
kubectl apply -f mypod.yaml
```

- To check the node where mypod is scheduled, you can use the following command:
```
kubectl get pods mypod -o wide
```

This command will provide detailed information about the mypod, including the node it is scheduled on.

### Question 2: Reschedule the mypod pod onto the worker-1 node.

- Edit the mypod.yaml file and change the nodeName property to the following:
```
nodeName: worker-1
```

- Apply the modified pod manifest using the following command:
```
kubectl apply -f mypod.yaml
```

- To check the node where mypod is scheduled, you can use the following command:
```
kubectl get pods mypod -o wide
```

### Question 3: Create two pods and label them with the label color: blue imperatively

- Run the following command to create the first and second pod:
```
kubectl run first-pod --image=nginx --labels=color=blue
kubectl run second-pod --image=nginx --labels=color=blue 
```

### Question 4: Select all pods with the label color: blue using the selector keyword.
- Run the following command to select the pods with label color: blue.
```
kubectl get pods --selector=color=blue
```
