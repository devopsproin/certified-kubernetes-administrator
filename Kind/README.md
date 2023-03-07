# Steps to setup Cluster using kind 

## Step 1:- Install Docker Engine on Ubuntu
### [Click Here](https://docs.docker.com/engine/install/ubuntu/)

## Step 2:- Install Kind
### [Click Here](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

## Step 3:- Install Kubectl
`snap install kubectl --classic`

## Step 4:- Create Single Node Cluster
`kind create cluster`

## Other Commands
### To check all clusters
`kind get clusters`

### To delete a clusters
`kind delete cluster --name=<cluster-name>`

### Create cluster using config file
`kind create cluster --name=<cluster-name> --config=<file-name>`
