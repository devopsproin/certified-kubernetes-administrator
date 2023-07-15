# Commands and Arguments in Kubernetes

This readme file provides information and practical examples regarding the usage of commands and arguments in Kubernetes. 

## Create a Pod with Commands and Arguments
- To create a pod named demo-pod with the Debian image and use the printenv HOSTNAME command:
```
kubectl run demo-pod --image=debian --command -- printenv HOSTNAME
```

## Apply YAML File and Checking Pod Status
To apply a YAML file and check the status of the pod:
```
kubectl apply -f your-file.yaml
kubectl get pod -o wide
```

## Verify Hostname in Pod Logs
To verify the hostname is printed in the logs of a pod, use the following commands:
```
kubectl logs demo-pod
```
