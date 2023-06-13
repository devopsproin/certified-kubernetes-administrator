# Security Context Implementation
This repository contains YAML files and commands to implement security context in Kubernetes pods and containers, ensuring secure deployments of your applications. 

## File 1: sc-demo-1.yaml
This YAML file demonstrates the implementation of security context at the pod level.

```
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  volumes:
  - name: demo-vol
    emptyDir: {}
  containers:
  - name: sc-demo
    image: busybox:1.28
    command: [ "sh", "-c", "sleep 1h" ]
    volumeMounts:
    - name: demo-vol
      mountPath: /data/demo
```

To apply this file, use the following command:
```
kubectl apply -f sc-demo-1.yaml
```

To access the shell inside the pod, run the following command:
```
kubectl exec -it security-context-demo -- /bin/sh
```

This command executes an interactive shell inside the pod named "security-context-demo". It allows you to access the command line interface of the pod.

To check the user ID, group ID, and filesystem ID, run the following commands:
```
id
ps aux
```

The id command displays the user ID and group ID of the current user running inside the pod. The ps aux command shows the processes running inside the pod along with their details.

Since a volume is mounted, you can navigate to the mounted directory and perform file operations:

```
cd /data/demo
echo hello devopspro >> myfile
ls -l
```

These commands change the directory to "/data/demo", appends the text "hello devopspro" to a file named "myfile", and lists the files in the directory.

## File 2: sc-demo-2.yaml

This YAML file demonstrates the implementation of security context at both the pod and container level.

```
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo-2
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: sc-demo-2
    image: gcr.io/google-samples/node-hello:1.0
    securityContext:
      runAsUser: 2000
```

To apply this file, use the following command:
```
kubectl apply -f sc-demo-2.yaml
```

To access the shell inside the pod, run the following command:
```
kubectl exec -it security-context-demo-2 -- /bin/sh
```

This command executes an interactive shell inside the pod named "security-context-demo-2".

To check the applied security context on the container, run the following commands:
```
ps aux
id
```

The ps aux command displays the running processes inside the container. The id command shows the user ID and group ID of the current user running inside the container.

## File 3: sc-demo-3.yaml
This YAML file demonstrates the addition of the NET_ADMIN capability to a container.

```
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo-3
spec:
  containers:
  - name: sc-demo-3
    image: ubuntu
    command: [ "sh", "-c", "sleep 1h" ]
    securityContext:
      capabilities:
        add: ["NET_ADMIN"]
```

To apply this file, use the following command:
```
kubectl apply -f sc-demo-3.yaml
```

To access the shell inside the pod, run the following command:
```
kubectl exec -it security-context-demo-3 -- /bin/bash
```

This command executes an interactive bash shell inside the pod named "security-context-demo-3".

To install the required package, run the following commands inside the pod:
```
apt update
apt install iproute2
```

These commands update the package lists and install the "iproute2" package, which provides advanced IP routing and network devices configuration.

To check the network interfaces, run the following command:
```
ip link show
```

This command displays the network interfaces and their details, such as name, state, and MAC address.

To add an IP address to the eth0 network interface, use the following command:
```
ip addr add 192.168.0.10/24 dev eth0
```

This command assigns the IP address "192.168.0.10" with a subnet mask of "/24" to the "eth0" network interface.

To check the added IP address, run the following command:
```
ip addr show eth0
```

This command displays the details of the "eth0" network interface, including the assigned IP address.
