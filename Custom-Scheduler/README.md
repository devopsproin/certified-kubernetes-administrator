# Steps to Implement Custom Scheduler
The following steps outline the process of creating a custom scheduler as a pod and using it to schedule an Nginx pod. Follow these steps to set up the custom scheduler:               

- Copy the Kube-scheduler.yaml located under the /etc/kubernetes/manifests/ directory to my-scheduler.yaml file outside the /etc/kubernetes/manifests/ directory and update the my-scheduler.yaml file as mentioned in the following steps:

- Change the name under the metadata section to "my-scheduler" and create the pod under the default namespace.
```
apiVersion: v1
kind: Pod
metadata:
  labels:
    component: my-scheduler
    tier: control-plane
  name: my-scheduler
```

- Update the command field in the spec section by setting --leader-elect=false. This is because you only have a single master node in the cluster. If there were multiple master nodes, you would choose --leader-elect=true.
```
spec:
  containers:
  - command:
    - kube-scheduler
    - --authentication-kubeconfig=/etc/kubernetes/scheduler.conf
    - --authorization-kubeconfig=/etc/kubernetes/scheduler.conf
    - --bind-address=127.0.0.1
    - --kubeconfig=/etc/kubernetes/scheduler.conf
    - --leader-elect=false
```

- Find an available port to bind to the pod. You can use the following command to check for free port numbers:
```
netstat -natulp | grep 10282
```

- Set the --scheduler-name property and assign the desired name for your custom scheduler. For example, if you want to name it "my-scheduler":
```
- --port=10282
- --scheduler-name=my-scheduler
- --secure-port=0
```

- Leave other configurations as they are and change the port number in the livenessProbe section to port: 10282.
```
livenessProbe:
  failureThreshold: 8
  httpGet:
    host: 127.0.0.1
    path: /healthz
    port: 10282
```

- The final YAML file should look like the following:
```
apiVersion: v1
kind: Pod
metadata:
  labels:
    component: my-scheduler
    tier: control-plane
  name: my-scheduler
spec:
  containers:
  - command:
    - kube-scheduler
    - --authentication-kubeconfig=/etc/kubernetes/scheduler.conf
    - --authorization-kubeconfig=/etc/kubernetes/scheduler.conf
    - --bind-address=127.0.0.1
    - --kubeconfig=/etc/kubernetes/scheduler.conf
    - --leader-elect=false
    - --port=10282
    - --scheduler-name=my-scheduler
    - --secure-port=0
    image: k8s.gcr.io/kube-scheduler:v1.19.0
    imagePullPolicy: IfNotPresent
    livenessProbe:
      failureThreshold: 8
      httpGet:
        host: 127.0.0.1
        path: /healthz
        port: 10282
        scheme: HTTP
      initialDelaySeconds: 10
      periodSeconds: 10
      timeoutSeconds: 15
    name: kube-scheduler
    resources:
      requests:
        cpu: 100m
    startupProbe:
      failureThreshold: 24
      httpGet:
        host: 127.0.0.1
        path: /healthz
        port: 10282
        scheme: HTTP
      initialDelaySeconds: 10
      periodSeconds: 10
      timeoutSeconds: 15
    volumeMounts:
    - mountPath: /etc/kubernetes/scheduler.conf
      name: kubeconfig
      readOnly: true
  hostNetwork: true
  priorityClassName: system-node-critical
  volumes:
  - hostPath:
      path: /etc/kubernetes/scheduler.conf
      type: FileOrCreate
    name: kubeconfig
status: {}
```

- Save the my-scheduler.yaml file and create the pod using the following command:
```
kubectl apply -f my-scheduler.yaml
```

- This will create a custom scheduler pod in the default namespace. You can verify its creation by running the command:
```
kubectl get pods
```

- Create a pod YAML file and specify the schedulerName option as "my-scheduler" to instruct Kubernetes to use your custom scheduler for this pod. The YAML file should look like this:
```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  labels:
    name: multischeduler
spec:
  schedulerName: my-scheduler
  containers:
  - name: nginx
    image: nginx
```

- Verify whether your custom scheduler is used by checking the events section of the pod. Use the following command:
```
kubectl describe pod mypod
```

- Look for the Events section and check the output. You should see an event indicating that the pod was successfully assigned to the custom scheduler:
```
Events:
  Type        Reason      Age   From            Message
  ----        ------      ----  ----            -------
  Normal      Scheduled   16m   my-scheduler    Successfully assigned mypod to minikube
  Normal      Pulling     16m   kubelet, minikube   Pulling image "nginx"
  Normal      Pulled      16m   kubelet, minikube   Successfully pulled image "nginx"
  Normal      Created     16m   kubelet, minikube   Created container nginx
  Normal      Started     16m   kubelet, minikube   Started container nginx
```

- Congratulations! You have successfully created a custom scheduler and used it to schedule a pod.

## Conclusion:
This guide covered the implementation steps for creating a custom scheduler in Kubernetes. It explained the process of creating a custom scheduler pod, configuring its parameters, and using it to schedule a specific pod. By following these steps, you have gained insights into how the scheduler works and how to leverage custom scheduling in Kubernetes.
