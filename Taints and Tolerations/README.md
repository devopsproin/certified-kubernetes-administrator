# Taints and Tolerations in Kubernetes
This repository contains practical questions and solutions related to taints and tolerations in Kubernetes. The questions are based on the video tutorial [Link to video](https://youtu.be/y4UarwGKZQQ).

## Question 1: Taint a node with the Noschedule taint effect and set the key-value pair to run: mypod.
Solution: Use the following command to apply the taint to the desired node:
```
kubectl taint nodes <node_name> run=mypod:NoSchedule
```

## Question 2: Create a pod named "test" and check the node on which it is scheduled.
Solution: Use the following command to create the pod and view its scheduled node:
```
kubectl create pod test
kubectl get pod test -o wide
```

## Question 3: Create a pod and add a toleration to it with the following specifications:
### Key: key1
### Operator: Equal
### Value: value1
### Effect: Noschedule
Solution: Use the following YAML definition to create the pod with the toleration:
```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: nginx
tolerations:
- key: key1
  operator: Equal
  value: value1
  effect: NoSchedule
```

### Question 4: Remove the taint effect from the node that was previously tainted.
Solution: Use the following command to remove the taint from the node:
```
kubectl taint nodes <node_name> run=mypod:NoSchedule-
```
