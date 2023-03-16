# Ingress demonstration 
This is a demonstration of how to use Kubernetes Ingress to route traffic to different services in your cluster based on different paths.

## Install nginx-ingress controller :
To get started, you will need to install the nginx-ingress controller in your Kubernetes cluster by running the following command:

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

This will deploy the nginx-ingress controller as a Deployment in your cluster.

## Create Deployments
Next, you will need to create some sample Deployments to route traffic to. Run the following commands to create the Deployments:

```
kubectl create deploy sample-1 --image=devopsprosamples/next-path-sample-1
kubectl create deploy sample-2 --image=devopsprosamples/next-path-sample-2
kubectl create deploy sample-3 --image=devopsprosamples/next-sample-1
kubectl create deploy sample-4 --image=devopsprosamples/next-sample-2
```

These commands will create four sample Deployments with different images.

## Create services
After you have created the Deployments, you will need to create Services for each of them. Run the following commands to create the Services:

```
kubectl expose deploy sample-1 --type=ClusterIP --port=3000
kubectl expose deploy sample-2 --type=ClusterIP --port=3000
kubectl expose deploy sample-3 --type=ClusterIP --port=3000
kubectl expose deploy sample-4 --type=ClusterIP --port=3000
```

These commands will create four Services with ClusterIP type for each of the sample Deployments.

## Create Ingress resource
Now that you have created the Services, you can create an Ingress resource to route traffic to them based on different paths. To create the Ingress resource, run the following command:

```
kubectl apply -f ingress-resource.yaml
```

This will create an Ingress resource with rules to route traffic to the sample Services based on different paths.

## Install certificate manager
If you want to use HTTPS with your Ingress, you will need to install a certificate manager. Run the following command to install the Jetstack cert-manager:

```
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.7.1/cert-manager.yaml
```

This will install the cert-manager as a Deployment in your cluster.

## Create Clusterissuer
After you have installed the cert-manager, you can create a Clusterissuer to issue SSL certificates for your Ingress. Run the following commands to create the staging and production Clusterissuers:

```
kubectl apply -f staging_issuer.yaml
kubectl apply -f prod_issuer.yaml
```

These commands will create two Clusterissuers, one for staging and one for production.

## Other Commands
Here are some other useful commands to help you manage your Kubernetes cluster:

#### To view deployments
```
kubectl get deploy
```
#### To view services
```
kubectl get svc
```
#### To view ingress
```
kubectl get ing
```
#### To describe ingress
```
kubectl describe ing <ing-name>
```
#### To view clusterissuer
```
kubectl get clusterissuer
```
#### To view certificate
```
kubectl get certificate
```
#### To describe certificate
```
kubectl describe certificate
```
