# Namespace Creation

## Introduction
This README file provides a step-by-step guide to performing practical tasks related to Namespace creation in Kubernetes. The questions covered in this guide will help you understand and practice creating namespaces and working with pods within those namespaces.

Link to YouTube Video: https://youtu.be/dBjWCOwcTvM

### Question 1: Create a namespace named "my-first-ns".
```
kubectl create namespace my-first-ns
```
This will create a new namespace called "my-first-ns" in your Kubernetes cluster.

### Question 2: Create a pod named "red" with the image "nginx" within the "my-first-ns" namespace.
```
kubectl create pod red --image=nginx --namespace=my-first-ns
```
This will create a pod named "red" with the nginx image specifically within the "my-first-ns" namespace.

### Question 3: Count all the pods across all namespaces
```
kubectl get pods --all-namespaces --no-headers | wc -l
```
This will provide the count of all the pods present in all namespaces in your Kubernetes cluster.

### Question 4: Permanently switch the namespace to "my-first-ns"
```
kubectl config set-context --current --namespace=my-first-ns
```
This will set the namespace to "my-first-ns" as the default namespace for all subsequent commands.
