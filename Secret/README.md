# Commands used in video

## To create different types of secrets
### Generic Secret
kubectl create secret generic db-secret --from-literal=username=dbuser --from-literal=password=Y4nys7f11

### Docker-registry Secret
kubectl create secret docker-registry docker-secret \
  --docker-email=example@gmail.com \
  --docker-username=dev \
  --docker-password=pass1234 \
  --docker-server=my-registry.example:5000

### TLS Secret
kubectl create secret tls my-tls-secret \
  --cert=data/serverca.crt \
  --key=data/servercakey.pem


## To apply yaml files
`kubectl apply -f <file-name.yaml>`

## To check running pods
`kubectl get pods`

## To check created secrets
`kubectl get secret`

## To describe a secret
`kubectl describe secret <secret-name>`

## To check environment variables in running pod
`kubectl exec -it <pod-name> -- printenv`

## To go inside running pod
`kubectl exec -it <pod-name> -- bash`

## To extract pod's yaml file
kubectl get pod pod-name -o yaml

## To decode the encrypted data
echo "data" | base64 -d
