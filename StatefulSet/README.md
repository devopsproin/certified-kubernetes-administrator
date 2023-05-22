# Kubernetes StatefulSet Guide
## Headless Service
The Headless Service YAML file defines a Kubernetes Service that does not assign an IP address to the pods. It is used for discovering and connecting to individual pods directly.

service.yaml:
```
apiVersion: v1
kind: Service
metadata:
  name: headless-svc
spec:
  selector:
    app: nginx
  ports:
  - port: 80
    name: web
  clusterIP: None
```

### To apply the Headless Service YAML file, use the following command:
```
kubectl apply -f service.yaml
```

### To retrieve the information about the "headless-svc" service, use the following command:
```
kubectl get service headless-svc
```

## StatefulSet
The StatefulSet YAML file defines a Kubernetes StatefulSet, which manages the deployment and scaling of stateful applications. In this example, it creates and manages two replicas of an nginx application.

sts.yaml:
```
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "headless-svc"
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: registry.k8s.io/nginx-slim:0.8
        ports:
        - containerPort: 80
          name: web
```

### To apply the StatefulSet YAML file, use the following command:
```
kubectl apply -f sts.yaml
```

### To retrieve the information about the "web" StatefulSet, including the number of replicas and their current status, use the following command:
```
kubectl get sts web
```

### To retrieve the information about the pods associated with the "nginx" application and continuously monitors their status, use the following command:
```
kubectl get pods -w -l app=nginx
```

### To scale the "web" StatefulSet, use the following command:
```
kubectl scale sts web --replicas=4
```

### To delete the "web" StatefulSet and all associated pods, use the following command:
```
kubectl delete sts web
```

## Storage with StatefulSet
The Storage with StatefulSet YAML file extends the previous StatefulSet example by adding a PersistentVolumeClaim (PVC) for storage using volumeClaimTemplates field. It mounts a volume to the nginx containers in the StatefulSet.

sts.yaml:-
```
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "headless-svc"
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: registry.k8s.io/nginx-slim:0.8
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: web-pvc
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: web-pvc
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
      storageClassName: ebs-sc
       
```

### To apply the Storage with StatefulSet YAML file to create the StatefulSet with persistent storage in the Kubernetes cluster, use the following command:
```
kubectl apply -f sts.yaml
```

In conclusion, this Kubernetes StatefulSet Guide provides a set of YAML files and commands to help you deploy and manage stateful applications in a Kubernetes cluster. It covers the creation of a Headless Service for direct pod discovery and connection, the deployment and scaling of a StatefulSet with replicas, and the integration of persistent storage using a PersistentVolumeClaim (PVC). By following the instructions and using the provided examples, you can effectively utilize StatefulSets and leverage the power of Kubernetes for your stateful application needs.
