# Deployments


# Understand problems with just ReplicaSet
```s
# change in replicset
$ kubectl apply -f dobby-rs-env-version.yaml
$ curl "k8s-master:30003/version"

$ kubectl apply -f dobby-rs-env-version.yaml
$ curl "k8s-master:30003/version"
# observe version

# now delete RS and apply again
$ kubectl delete rs dobby-rs
$ kubectl apply -f dobby-rs-env-version.yaml
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

# how to see all revisions of dployment
$ kubectl rollout history deployment/dobby
# notice all 3 revisions deployed so far, however, the field change-cause is empty
# how to set change cause
$ kubectl annotate deployment dobby kubernetes.io/change-cause="my message" --record=false --overwrite=true
$ kubectl rollout history deployment/dobby
$ kubectl rollout history deployment/dobby --revision=3

$ export GIT_COMMIT=$(git log -1 --format=%h)
$ kubectl annotate deployment dobby kubernetes.io/change-cause="$GIT_COMMIT" --record=false --overwrite=true
$ kubectl rollout history deployment/dobby

$ kubectl apply -f dobby-deployment-with-annotation.yaml
$ kubectl rollout history deployment/dobby

# rollback
$ kubectl rollout undo deployment/dobby
$ kubectl rollout history deployment/dobby
# notice reuse of previous replicaset
$ kubectl rollout undo deployment/dobby --to-revision=1
$ kubectl rollout history deployment/dobby
$ curl "k8s-master:30003/version"

```

# Deployment strategies
```s
# increase no of pods
$ kubectl apply -f dobby-deployment-6-replicas.yaml

# RollingUpdate is default strategy
$ while true; do sleep 1; curl "k8s-master:30003/version"; echo -e '    '$(date);done
$ kubectl apply -f dobby-deployment-rolling-strategy.yaml
# notice slow updates and no downtime, however both version co-exists at given point of time

$ kubectl apply -f dobby-deployment-recreate-strategy.yaml
# notice downtime, all gone and recreated

```


# How to achieve, Canary release and True Blue-Green release with Zero Downtime?
```s


```

