# Flux cluster state for testing k8s setups
This repository contains the cluster state for a local test cluster, using minikube.


## 1. Setup minikube

```
brew install podman
brew install minikube
podman machine init --cpus 2 --memory 4096 --rootful 
podman machine start
minikube start --driver=podman
```

## 2. Setup flux
```
flux bootstrap git \
  --url=ssh://git@github.com/HenrikDK/flux-cluster-state.git \
  --branch=main \
  --path=clusters/minikube \
  --private-key-file=/path/to/private/key
```

# ingress
This repository creates an ingress for the prometheus service for testing purposes, exposed by the ingress controller, while the ip listed in k8s says 127.0.0.1 this ip is incorrect as it is viewed from inside the VM. 

To find the ip of the microk8s VM running on a machine run the multipass command:
```
multipass list
``

the first ip of the vm can then be used in a host file
<ip>    prometheus.test
