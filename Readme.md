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