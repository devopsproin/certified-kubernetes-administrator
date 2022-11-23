# Commands used in video

## To create configmaps
`kubectl create configmap configmap-1 --from-literal=name=first-configmap`

`kubectl create configmap configmap-2 --from-literal=name=second-configmap --from-literal=color=blue`

`kubectl create configmap configmap-3 --from-file=data-file`

## To apply yaml files
`kubectl apply -f <file-name.yaml>`

## To see pods
`kubectl get pods`

## To see configmaps
`kubectl get cm`

## To see environment variables in running pod
`kubectl exec -it <pod-name> -- printenv`

## To go inside running pod
`kubectl exec -it <pod-name> -- bash`
