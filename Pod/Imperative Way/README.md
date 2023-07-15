# Pod Creation using Imperative Way

## Introduction
This readme file provides step-by-step instructions for the practical questions on pod creation using the imperative way. These questions were covered in the YouTube video [https://youtu.be/ODJwFsdK2oU]. Each question focuses on a specific task related to creating pods using imperative commands in Kubernetes. Follow the instructions below to perform each task and gain hands-on experience with pod creation.

### Question 1: Create a pod with name "mypod" using nginx:alpine image.
To create a pod with the name "mypod" and using the nginx:alpine image, use the following command:
```
kubectl run mypod --image=nginx:alpine
```
This command will create the pod with the specified name and image.

### Question 2: Create a pod with name "pod-2" using the redis image with label name=pod-2
To create a pod named "pod-2" using the Redis image and assigning the label "name=pod-2", use the following command:
```
kubectl run pod-2 --image=redis --labels=name=pod-2
```
This command will create the pod with the specified name, image, and label.

### Question 3: Create a pod with name "nginx" and image nginx, expose it on Port 8080
To create a pod with the name "nginx" using the nginx image and expose it on port 8080, use the following command:
```
kubectl run nginx --image=nginx --port=8080
```
This command will create the pod with the specified name, image, and port.
