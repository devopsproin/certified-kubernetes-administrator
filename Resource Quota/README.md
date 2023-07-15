# Resource Quota Creation

## Introduction
This README provides instructions on how to create, verify, view, and delete Resource Quotas in Kubernetes using YAML files. It also explains how to check the resource utilization of a specific namespace. The steps mentioned below can be followed to perform these operations.

Video Link: https://youtu.be/nia8nreVmBg

## Creating a Resource Quota
Create a YAML file, for example, resource-quota.yaml, with the desired specifications for the Resource Quota.
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-resources
  namespace: my-first-ns
spec:
  hard:
    pods: "4"
    requests.cpu: "1"
    requests.memory: 1Gi
    limits.cpu: "2"
    limits.memory: 2Gi
```

Apply the Resource Quota using the following command:
```
kubectl apply -f resource-quota.yaml
```

## Verify Resource Quota Creation
To verify that the Resource Quota has been successfully created, run the following command:
```
kubectl get resourcequota compute-resources -n my-first-ns
```

## View Existing Resource Quotas
To view the existing Resource Quotas in the my-first-ns namespace, use the following command:
```
kubectl get resourcequota -n my-first-ns
```

## Delete a Resource Quota
To delete a Resource Quota from the my-first-ns namespace, execute the following command:
```
kubectl delete resourcequota compute-resources -n my-first-ns
```

## Checking Resource Utilization
To check the resource utilization of the my-first-ns namespace, run the following command:
```
kubectl top namespace my-first-ns
```

For more detailed explanations and examples, please watch the accompanying YouTube video.
