# Deployments


# Understand problems with just ReplicaSet
```s
# change in replicset
$ curl "k8s-master:30003/version"

$ kubectl apply -f dobby-rs-env-version-2.yaml
$ curl "k8s-master:30003/version"
# observe version

# now delete RS and apply again
$ kubectl delete rs dobby-rs
$ kubectl apply -f dobby-rs-env-version-2.yaml
$ curl "k8s-master:30003/version"
# observe version
```

# Deploy deployment
```s
$ kubectl apply -f dobby-deployment.yaml
# observe deployment, replicaset and pods - along with our previous service and endpoints getting attached to new pods


$ curl "k8s-master:30003/version"
# change version to 2.0
$ kubectl apply -f dobby-deployment.yaml
$ curl "k8s-master:30003/version"
# change version to 3.0
$ kubectl apply -f dobby-deployment.yaml
$ curl "k8s-master:30003/version"

```
