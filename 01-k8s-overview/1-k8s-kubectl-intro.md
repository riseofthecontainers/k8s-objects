# Kubernetes Introduction

### basic version check
```s
$ kubectl version --short
$ kubectl cluster-info
```

### coomands related to kube configs

```s
$ echo $KUBECONFIG
$ kubectl config view   # show context: users, clusters & contexts

$ export KUBECONFIG=~/.kube/config:~/.kube/configs/sunitp-k8s.conf
$ kubectl config view
$ kubectl config get-contexts
$ kubectl config current-context
$ kubectl config set-context sunitp@kubernetes
```

### kubectl commands to interact with 3 node cluster
```s
$ kubectl get nodes -o wide
$ kubectl get nodes -v
$ kubectl get pods -A -o wide
$ kubeclt get namespaces
$ kubectl get all --all-namespaces
```

### kubectl commands to interact with minikube (one that particiapnts are going to use)
```s
$ minikube start --memory=16000m --cpus=4
$ kubectl get nodes -o wide
$ ubectl config set-context minikube
$ kubectl get pods -A -o wide

# if you like to connect to docker inside minikube
$ eval $(minikube docker-env)

# minikube ALL BATTERIES INLCUDED for learning K8S Objects & Workloads
# End of workshop, I will show how to setup multinode cluster using VirtualBox
```
