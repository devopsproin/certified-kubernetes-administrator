# Environment Variables in Kubernetes
In this video, we will be discussing how to use environment variables in Kubernetes to configure your applications. Environment variables allow you to store configuration data separately from your application code, making it easier to manage and update your application.

## Prerequisites
Before getting started, you will need to have the following:
- A Kubernetes cluster up and running
- A Docker image of your application

## Commands Used in Video
Follow the commands below to use environment variables in Kubernetes:

### Step 1: Build your Docker image by running the following command:
```
docker build -t wordpress .
```

### Step 2: Apply your YAML files by running the following command:
```
kubectl apply -f <file-name>
```

### Step 3: To see the list of pods, run the following command:
```
kubectl get pods
```

### Step 4: To check the logs of a pod, run the following command:
```
kubectl logs <pod-name>
```

### Step 5: To print the environment variables of a pod, run the following command:
```
kubectl exec <pod-name> -- printenv
```

## Conclusion
By using environment variables in Kubernetes, you can easily configure your applications without having to modify your application code. This makes it easier to manage and update your application, and allows you to quickly and easily scale your application as needed.
