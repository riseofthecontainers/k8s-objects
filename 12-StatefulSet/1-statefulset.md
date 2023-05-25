# StatefulSet & Headless Service

### Statefulset
```s
kubectl apply -f StatefulSet.yaml
kubectl get pods,pv,pvc

# increase the replicas
kubectl get pods

# Decreate the replicas
kubectl get pods,pv,pvc
```

### Headless Service
```s
kubectl apply -f headless-service.yaml
kubectl get svc
# Do a curl request for headless service using some busybox pod.
```