# Jobs

### test Job
```s
kubectl apply -f job.yaml
# show them that the pods are coming into completion state
kubectl get pods
# check for the logs
kubectl logs test-job
```

### Parallel Job
```s
kubectl apply -f parallel-job.yaml
# show them the parallel job
kubectl get pods
```

### Cron Job
```s
kubectl apply -f cron-job.yaml
# watch for the pods
kubectl get pods -w
```