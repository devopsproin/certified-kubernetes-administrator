# Commands used in video

## To Build Docker image
`docker build -t wordpress .`

## To apply yaml files
`kubectl apply -f <file-name>`

## To see pods
`kubectl get pods`

## To check logs of a pod
`kubectl logs <pod-name>`

## To print environment variables of a pod
`kubectl exec <pod-name> -- printenv`
