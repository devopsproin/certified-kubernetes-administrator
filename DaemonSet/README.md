# Daemonsets in Kubernetes
This README file provides an overview of Daemonsets in Kubernetes, including their creation, rolling updates, rollback, viewing running Daemonsets, and deleting Daemonsets.

## Create a Daemonset
- To create a Daemonset in Kubernetes use the following yaml file: 
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-daemonset
spec:
  selector:
    matchLabels:
      app: fluentd
  template:
    metadata:
      labels:
        app: fluentd
    spec:
      containers:
        - name: fluentd
          image: fluent/fluentd:latest
```
- Apply above file using command: 
```
kubectl apply -f fluentd-daemonset.yaml
```

- To view all the running Daemonsets, use the following command:
```
kubectl get daemonsets
```

## Update a Daemonset
- Update fluentd-daemonset.yaml:
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-daemonset
spec:
  selector:
    matchLabels:
      app: fluentd
  template:
    metadata:
      labels:
        app: fluentd
    spec:
      containers:
        - name: fluentd
          image: fluent/fluentd:v1.2.3
```

## View upadted daemonset's pod
```
kubectl get pods -l app=fluentd
```

## Check logs collected by fluentd
Once you have the pod name, you can view the logs by running the following command:
```
kubectl logs <pod_name>
```

## Rolling Update a Daemonset
- To rollback the Daemonset to a previous version, use the following command:
```
kubectl rollout undo daemonset fluentd-daemonset
```

## Delete a Daemonset
To delete the Daemonset named "fluentd-daemonset", use the following command:
```
kubectl delete daemonset fluentd-daemonset
```
