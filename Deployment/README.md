# Deployment Creation
This README file provides step-by-step instructions to perform various deployment operations using Kubernetes. The following practical questions are covered in this guide.

Video Link: https://youtu.be/-uO400iEuKo

### Question 1: Create a deployment named my-deploy with the image nginx.
To create a deployment named "my-deploy" with the nginx image, use the following command:
```
kubectl create deployment my-deploy --image=nginx
```

### Question 2: Scale my-deploy to 3 replicas.
To scale the "my-deploy" deployment to 3 replicas, use the following command:
```
kubectl scale deployment my-deploy --replicas=3
```

### Question 3: Replace the image in my-deploy from nginx to nginx:alpine.
To replace the image in the "my-deploy" deployment from "nginx" to "nginx:alpine", use the following command:
```
kubectl set image deployment my-deploy nginx=nginx:alpine
```

### Question 4: Scale down the replicas of my-deploy to 2.
To scale down the replicas of the "my-deploy" deployment to 2, use the following command:
```
kubectl scale deployment my-deploy --replicas=2
```

### Question 5: Rollback to the previous version of my-deploy.
To rollback the "my-deploy" deployment to the previous version, use the following command:
```
kubectl rollout undo deployment my-deploy
```

### Question 6: Delete the deployment, replicaset, and pod created by my-deploy.
To delete the deployment, replicaset, and pods created by the "my-deploy" deployment, use the following command:
```
kubectl delete deployment my-deploy
```

That's it! You've learned how to perform various deployment operations in Kubernetes. For a visual demonstration, refer to the video link provided above.
