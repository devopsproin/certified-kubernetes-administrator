# Multi-Node Kubernetes Cluster Setup with Kind
This repository contains the code and configuration files for setting up a multi-node Kubernetes cluster using Kind (Kubernetes in Docker).

## Steps to Setup Cluster using Kind
Follow the below steps to setup a multi-node Kubernetes cluster using Kind:

### Step 1: Install Docker Engine on Ubuntu
Before installing Kind, Docker Engine needs to be installed on Ubuntu. Follow the instructions mentioned [here](https://docs.docker.com/engine/install/ubuntu/) to install Docker Engine.

### Step 2: Install Kind
Kind can be installed using the instructions mentioned [here](https://kind.sigs.k8s.io/docs/user/quick-start/#installation).

### Step 3: Install Kubectl
Kubectl is the command-line tool for managing Kubernetes clusters. It can be installed using the following command:
```
snap install kubectl --classic
```

### Step 4:- Create Single Node Cluster
Create a Single Node Cluster by running the following command:
```
kind create cluster
```

You can check all clusters using the following command:
```
kind get clusters
```

To delete a cluster, run the following command:
```
kind delete cluster --name=<cluster-name>
```

### Bonus:
You can also create a cluster using a configuration file by running the following command:
```
kind create cluster --name=<cluster-name> --config=<file-name>
```

## Conclusion
By following these simple steps, you can easily setup a multi-node Kubernetes cluster using Kind. This is a great way to test your Kubernetes applications locally before deploying to production.
