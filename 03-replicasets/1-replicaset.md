# ReplicSet commands


# create a 2 separate terminal split pane with watch on pods
```s
$ watch kubectl get pods -o wide
$ kubectl get rs -w
```

```s
$ kubectl apply -f dobby-rs.yaml
$ kubectl get rs -o wide
# observe CURRENT, DESIRED column along with SELECTOR
$ kubectl get pods -o wide --show-labels
$ kubectl describe rs dobby-rs

# fun part - add Pod with same label
$ kubectl apply -f dobby-with-labels.yaml
# remove label and apply again
$ kubectl apply -f dobby-with-labels.yaml

# increase replica count to 6 and apply again
$ kubectl apply -f dobby-rs.yaml
# decrease replica count to 2 and apply again

$ kubectl delete pod dobby-rs-????
# notice new pods spin up immediately

# shutdown one worker node and see pods are recreated on remaining nodes

$ kubectl delete rs dobby-rs
```