# Environment Variables in Kubernetes Part 2: Exposing Pod Information to Containers
This repository contains the code and resources used in the YouTube video [Environment Variables in Kubernetes Part 2: Exposing Pod Information to Containers](https://youtu.be/byjjMArir_c).

## Overview
In this video, we will learn how to expose pod information to containers in Kubernetes. We will look at different methods of passing information from the pod to the container via environment variables.

## Commands Used in Video

### To apply YAML files:
```
kubectl apply -f <file-name>
```

### To see pods:
```
kubectl get pods
```

### To check logs of a pod:
```
kubectl logs <pod-name>
```

### To print environment variables of a pod:
```
kubectl exec <pod-name> -- printenv
```

## Conclusion
By the end of this video, you should have a better understanding of how to expose pod information to containers in Kubernetes.
