# Flux cluster state for testing k8s setups
This repository contains the cluster state for a local test cluster.


## 1. Setup microk8s

```
brew install ubuntu/microk8s/microk8s

microk8s install

microk8s status --wait-ready

microk8s disable ha-cluster
microk8s enable dns
microk8s enable metrics-server
microk8s enable ingress
microk8s stop
microk8s start
```

## 2. Setup flux
```
flux bootstrap git \
  --url=ssh://git@github.com/HenrikDK/flux-cluster-state.git \
  --branch=main \
  --path=clusters/microk8s \
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
