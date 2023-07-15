# StaticPods in Kubernetes
This README provides instructions on creating and managing static pods in Kubernetes. 

### Create a Static Pod with the Name "static-web" Using the Nginx Image.
To create a static pod with the name "static-web" using the Nginx image, follow these steps:

- Create a YAML file named static-web.yaml with the following contents:
```
apiVersion: v1
kind: Pod
metadata:
  name: static-web
spec:
  containers:
  - name: nginx
    image: nginx
```

- Apply the pod definition using the command:
```
kubectl apply -f static-web.yaml
```

- Verify the successful creation of the static pod using the command:
```
kubectl get pods
```

### Copy the pod YAML to the folder designated for static pod's YAML files
To copy the pod YAML to the folder designated for static pod's YAML files, complete the following steps:

- Locate the folder on the Kubernetes node that contains the static pod's YAML files, typically /etc/kubernetes/manifests/.
- Copy the static-web.yaml file into the folder using the command:
```
sudo cp static-web.yaml /etc/kubernetes/manifests/
```

### 3. How to Ensure that the Pod is Started by Kubelet?
To ensure that the pod is started by kubelet, follow these steps:

- Monitor the pod's status using the command:
```
kubectl get pods
```

Confirm that the pod's status changes to "Running," indicating that kubelet has successfully started the static pod.
