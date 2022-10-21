## To Build Docker image
`docker build -t wordpress .`

## To apply envars.yaml
`kubectl apply -f envars.yaml`

`kubectl get pods`

`kubectl exec env-var -- printenv`


## To apply envars-2.yaml
`kubectl apply -f env.yaml`

`kubectl get pods`

`kubectl logs env-var-2`

`kubectl exec env-var -- printenv`
