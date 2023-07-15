# Rollback a Kubernetes Deployment
This readme file provides step-by-step instructions on how to deploy and manage the Nginx web server using Kubernetes Deployment. It also covers the process of rolling back to previous revisions if necessary.

## Deployment Creation
To deploy the Nginx web server, follow these steps:

- Create a file named nginx-deployment.yaml:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    run: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      run: nginx
  template:
    metadata:
      labels:
        run: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

- Run the following command to deploy the Nginx server using the nginx-deployment.yaml file:
```
kubectl apply -f nginx-deployment.yaml --record=true
```

## Checking Deployment Status
To verify the deployment status, execute the following command:
```
kubectl get deployment
```

The output will display information about the deployed Nginx server, including the number of replicas.

## Upgrading the Deployment Image
If you need to upgrade the Nginx image in the deployment, follow these steps:

- Run the following command to update the image to nginx:1.16.1:
```
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1 --record=true
```

- To check the rollout status, use the following command:
```
kubectl rollout status deployment/nginx-deployment
```

## Rolling Back a Deployment
In case an upgrade causes issues and you need to roll back to a previous version, follow these steps:

- Use the command below to view the revision history of the deployment:
```
kubectl rollout history deployment/nginx-deployment
```

- To see the details of a specific revision (e.g., revision 2), run the following command:
```
kubectl rollout history deployment/nginx-deployment --revision=2
```

- To perform a general rollback to the previous revision, execute the command:
```
kubectl rollout undo deployment/nginx-deployment
```

- If you want to rollback directly to a specific revision number (e.g., revision 1), use the following command:
```
kubectl rollout undo deployment/nginx-deployment --to-revision=1
```

- To verify the rollback, you can describe the deployment using the command:
```
kubectl describe deployment nginx-deployment
```
