# Environment Variables in Kubernetes Part 3: Exposing Pod Information to Containers Through Files
This repository contains the YAML files used in the video tutorial [Environment Variables in Kubernetes Part 3: Exposing Pod Information to Containers Through Files](https://youtu.be/fYjYzyZeaXM). In this video, you will learn how to expose pod information to containers through files in Kubernetes.

## Prerequisites
Before starting with this tutorial, you should have a basic understanding of Kubernetes and how to create a pod, service, and deployment. You should also have the kubectl command-line tool installed and configured to interact with your Kubernetes cluster.

## Commands used in the video
To apply the YAML files provided in this repository, use the following command:
```
kubectl apply -f volume.yaml
```

To see the pods running in your Kubernetes cluster, use the following command:
```
kubectl get pods
```

To see the volume files created by the downwardapi-volume pod, use the following command:
```
kubectl exec -it downwardapi-volume -- sh
```

## Summary
In this tutorial, you learned how to expose pod information to containers through files in Kubernetes. By using the downward API and a volume mount, you can expose various metadata about the pod to the containers running within it. This can be useful in many scenarios, such as passing environment variables or providing container-specific configuration files.

Thank you for watching this tutorial. If you have any questions or feedback, please don't hesitate to open an issue or submit a pull request to this repository.
