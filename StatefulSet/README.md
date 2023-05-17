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

### To apply the Headless Service YAML file
```
kubectl apply -f service.yaml
```

### To retrieve the information about the "headless-svc" service.
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

### To apply the StatefulSet YAML file.
```
kubectl apply -f sts.yaml
```

### To retrieve the information about the "web" StatefulSet, including the number of replicas and their current status.
```
kubectl get sts web
```

### To retrieve the information about the pods associated with the "nginx" application and continuously monitors their status.
```
kubectl get pods -w -l app=nginx
```

### To scale the "web" StatefulSet
```
kubectl scale sts web --replicas=4
```

### To delete the "web" StatefulSet and all associated pods.
```
kubectl delete sts web
```

## Storage with StatefulSet
The Storage with StatefulSet YAML file extends the previous StatefulSet example by adding a PersistentVolumeClaim (PVC) for storage. It mounts a volume to the nginx containers in the StatefulSet.

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
       
```

### To apply the Storage with StatefulSet YAML file to create the StatefulSet with persistent storage in the Kubernetes cluster.
```
kubectl apply -f sts.yaml
```

