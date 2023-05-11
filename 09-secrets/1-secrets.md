# Secrets

### passwords
```s
kubectl create secret generic mysecret --from-literal=password=mypassword
kubectl get secret mysecret -o yaml
kubectl apply -f test-pod-secret.yaml
kubectl exec pod/test-pod -it -- sh
# env
kubectl create secret generic mysecret --from-file=password=./password.txt
echo -n "mypassword" | base64
kubectl apply -f secret.yaml

```

### certificates
```s



```


