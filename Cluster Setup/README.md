# Multi-Node Kubernetes Cluster Setup Using Kubeadm
This readme provides step-by-step instructions for setting up a multi-node Kubernetes cluster using Kubeadm.

## Overview
This guide provides detailed instructions for setting up a multi-node Kubernetes cluster using Kubeadm. The guide includes instructions for installing and configuring containerd and Kubernetes, disabling swap, initializing the cluster, installing Flannel, and joining nodes to the cluster.

## Prerequisites
Before starting the installation process, ensure that the following prerequisites are met:

- You have at least two Ubuntu 18.04 or higher servers available for creating the cluster.
- Each server has at least 2GB of RAM and 2 CPU cores.
- The servers have network connectivity to each other.
- You have root access to each server.

## Installation Steps
The following are the step-by-step instructions for setting up a multi-node Kubernetes cluster using Kubeadm:

Update the system's package list and install necessary dependencies using the following commands:

```
sudo apt-get update
sudo apt install apt-transport-https curl -y
```

## Install containerd
To install Containerd, use the following commands:

```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install containerd.io -y
```

## Create containerd configuration
Next, create the containerd configuration file using the following commands:

```
sudo mkdir -p /etc/containerd
sudo containerd config default | sudo tee /etc/containerd/config.toml
```

## Edit /etc/containerd/config.toml
Edit the containerd configuration file to set SystemdCgroup to true. Use the following command to open the file:

```
sudo nano /etc/containerd/config.toml
```

Set SystemdCgroup to true:
```
SystemdCgroup = true
```

Restart containerd:
```
sudo systemctl restart containerd
```

## Install Kubernetes
To install Kubernetes, use the following commands:

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt install kubeadm kubelet kubectl kubernetes-cni
```

## Disable swap
Disable swap using the following command:

```
sudo swapoff -a
```

If there are any swap entries in the /etc/fstab file, remove them using a text editor such as nano:
```
sudo nano /etc/fstab
```

Enable kernel modules
```
sudo modprobe br_netfilter
```

Add some settings to sysctl
```
sudo sysctl -w net.ipv4.ip_forward=1
```
## Initialize the Cluster (Run only on master)
Use the following command to initialize the cluster:
```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

Create a .kube directory in your home directory:
```
mkdir -p $HOME/.kube
```

Copy the Kubernetes configuration file to your home directory:
```
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
```

Change ownership of the file:
```
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## Install Flannel (Run only on master)
Use the following command to install Flannel:
```
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/v0.20.2/Documentation/kube-flannel.yml
```

## Verify Installation
Verify that all the pods are up and running:

```
kubectl get pods --all-namespaces
```

## Join Nodes
To add nodes to the cluster, run the kubeadm join command with the appropriate arguments on each node. The command will output a token that can be used to join the node to the cluster.
