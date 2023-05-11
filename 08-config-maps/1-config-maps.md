# ConfigMaps


### configmap as properties ane ENV variables
```s
$ kubectl apply -f dobby-config-map.yaml
$ kubectl describe cm dobby-config

$ kubectl apply -f dobby-pod.yaml
$ kubectl exec dobby -it -- sh
    $ env

$ kubeclt apply -f dobby-full-configmap-as-env.yaml
$ kubectl exec dobby -it -- sh
    $ env
```

### configmap as file and file mounted using volume
```s
$ kubectl create configmap test-config-from-file --from-file test.properties
$ kubectl describe configmap test-config-from-file
# ticky bit is updating configmap files in k8s
$ kubectl create configmap test-config-from-file --from-file test.properties -o yaml --dry-run=client | kubectl replace -f -

$ kubectl apply -f test-pod-configmap-as-volume.yaml
```




