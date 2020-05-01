# Pod commands

## Pod basic commands

create a separate terminal split pane with watch on pods
```s
$ watch kubectl get pods -o wide
```

### Applicaiton overview
1. Nginx                
2. Hello World NodeJS   (one that we used during Docker module)
3. Dobby                (built by TW Chennai team, Krishana and others)

```s
$ kubectl get pods
$ kubectl apply -f nginx.yaml
$ kubectl apply -f dobby.yaml
$ kubectl apply -f hello-node.yaml

$ kubectl get pods -o wide
$ kubeclt describe pod dobby
$ kubectl logs dobby

# get inside container of a pod
$ kubectl exec dobby -it -- bash
    $ ps -aux   # notice the PID 1

# get into the node to hit API endpoints
$ minikube ssh 
$ curl -i 172.17.0.4:4444/health
$ curl -i 172.17.0.4:4444/meta

# get into the hello-node pod to hit API endpoints
$ kubectl exec hello-node -it -- sh
$ wget -qO- 172.17.0.4:4444/health
$ wget -qO- 172.17.0.4:4444/meta
$ wget -qO- 172.17.0.4:4444/version

# add ENV variable to POD and see the change
$ kubectl apply -f dobby-with-version.yaml
$ kubectl exec dobby -it -- bassh
    $ echo $VERSION

$ kubectl exec hello-node -it -- sh
$ wget -qO- 172.17.0.4:4444/version

# get into the node to hit API endpoints
$ minikube ssh 
$ curl -i -X PUT 172.17.0.4:4444/control/crash

# notice STATUS and RESTART count in watch pane
```

### create multi container pod
```s
$ kubectl apply -f multi-container.yaml
# notice READY column 2/2 - where as other pods are 1/1
$ kubectl describe pod multi-container

# get into node
$ curl -i 172.17.0.7   # see the timestamp

# get into one of the container
$ kubectl exec multi-container -it -- bash   
# default to 1st
$ cat /usr/share/nginx/html/index.html

# get into one specific container 2nd
$ kubectl exec multi-container -c 2nd -it -- bash
$ cat /html/index.html

```