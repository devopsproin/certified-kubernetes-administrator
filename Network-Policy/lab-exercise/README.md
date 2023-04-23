# Network Policy in Kubernetes Lab Exercise

This readme contains instructions and code for a lab exercise to demonstrate how to limit access to a Kubernetes service using network policies. This lab exercise is related to the video "[Network Policy in Kubernetes](https://youtu.be/-PipuYclU6Q)" on the DevOps Pro channel.

We encourage you to perform this practical alongside the video to get hands-on experience with network policies in Kubernetes.

## Lab Exercise
1. Create an nginx deployment and expose it via a service:
```
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --port=80
kubectl get svc,pod
```

This creates a deployment of the nginx image and exposes it as a service listening on port 80. The kubectl get command is used to confirm that both the service and pod were created successfully.

2. Test the service by accessing it from another Pod:
```
kubectl run busybox --rm -ti --image=busybox:1.28 -- /bin/sh
```

This creates a new Pod running the BusyBox image. Once inside the shell of the Pod, run the following command:

```
wget --spider --timeout=1 nginx
```

This command tests the connection to the nginx service. The output should confirm a successful connection to the service.

3. Limit access to the nginx service so that only Pods with the label access: true can query it, create a NetworkPolicy object as follows:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: access-nginx
spec:
  podSelector:
    matchLabels:
      app: nginx
  ingress:
  - from:
    - podSelector:
        matchLabels:
          access: "true"
```

Apply the NetworkPolicy object:

```
kubectl apply -f network-policy.yaml
```

This creates a NetworkPolicy object that specifies which pods can access the nginx service. The kubectl apply command applies the NetworkPolicy object to the cluster.

4. Test access to the service when access label is not defined:

```
kubectl run busybox --rm -ti --image=busybox:1.28 -- /bin/sh
wget --spider --timeout=1 nginx
```

This creates a new Pod running the BusyBox image. Once inside the shell of the Pod, run the wget command to access the nginx service. Since the Pod does not have the required access: true label, the output should indicate a download timeout.

5. Define the access label and test again:

```
kubectl run busybox --rm -ti --labels="access=true" --image=busybox:1.28 -- /bin/sh
wget --spider --timeout=1 nginx
```

This creates a new Pod running the BusyBox image with the required access: true label, and tests the connection to the nginx service again. The output should confirm a successful connection to the service.

## Conclusion
In this lab exercise, we learned how to use network policies in Kubernetes to limit access to a service. By creating a NetworkPolicy object, we specified which pods can access the service based on their labels. This can be useful in a production environment where security is a concern and access to certain services needs to be restricted.
