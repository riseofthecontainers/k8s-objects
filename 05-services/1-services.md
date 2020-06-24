# Services

# create a 3 separate terminal split pane with watch on pods
```s
$ watch kubectl get pods -o wide        #00f7ff
$ watch kubectl get svc                 #69f675
$ watch kubectl get endpoints           #ffeb00
```

### ClusterIP

```s
$ $ kubectl apply -f ../03-replicasets/dobby-rs.yaml
$ kubectl apply -f dobby-svc.yaml
$ kubectl describe svc dobbysvc
$ kubectl describe endpoints dobbysvc

# increase # of replicas to 3, followed by 4 and upto 6
$ kubectl apply -f ../03-replicasets/dobby-rs.yaml
$ kubectl describe svc dobbysvc
$ kubectl describe endpoints dobbysvc


# goto node and access pod via service
$ curl dobbysvc:4444/meta

# access dobby in loop and observe request going to different pods
$ while true; do sleep 2; curl "http://10.10.10.3:30003/meta"; echo -e '    '$(date);done


# to access via DNS name, get inside containers
$ kubectl exec hello-node -it -- sh
$ wget -qO- dobbysvc:4444/meta
$ while true; do sleep 2; wget -qO- "http://dobbysvc:4444/meta"; echo -e '    '$(date);done
$ ping dobbysvc

```

### NodePort
```s
$ kubectl apply -f ../03-replicasets/dobby-rs.yaml
$ kubectl apply -f dobby-svc-nodeport.yaml
$ minikube ip   # vagrant box IP - 10.10.10.2, 10.10.10.3, 10.10.10.4, 10.10.10.5
$ while true; do sleep 2; curl "k8s-master:30003/meta"; echo -e '    '$(date);done
# run on another node using same port
```


### LoadBalancer, connect to K8S cluster on Cloud Service provider like Digital Ocean
```s
# connect to digital ocean cluster
$ kubectl apply -f ../03-replicasets/dobby-rs.yaml
$ kubectl apply -f dobby-svc-lb.yaml
# get ip from Load Balancer
$ while true; do sleep 2; curl "10.10.10.2:4444/meta"; echo -e '    '$(date);done
# run on another node using same port
```