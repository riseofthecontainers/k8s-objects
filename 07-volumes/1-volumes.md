# Volumnes


## emptyDir

```s
$ kubectl create -f empty-dir.yaml

# create 2 verticle split pane for showcase 2 container commands side by side

$ kubectl exec empty-dir -c c1 -it -- bash
$ mount | grep html
$ tail -f /usr/share/nginx/html/index.html

$ kubectl exec empty-dir -c c2 -it -- bash
$ mount | grep html
$ tail -f /html/index.html

$ kubectl delete pod empty-dir

# apply again to showcase all data gone after restart
$ kubectl create -f empty-dir.yaml
$ kubectl exec empty-dir -c c1 -it -- bash
$ tail -f /usr/share/nginx/html/index.html
```


## hostPath

# check if directly exists on host machine or not

```s
$ kubectl create -f host-path.yaml
$ kubectl describe pod host-path
# notice failture as the directory on host machine does not exists

$ kubectl delete pod host-path

# create directly on node

$ kubectl create -f host-path.yaml
$ kubectl describe pod host-path

# on host machine
$ cd /home/vagrant/nginx/html
$ tail -f index.html


# delete and recreate pod to be lucky on same machine
$ kubectl delete pod host-path
$ kubectl apply -f host-path.yaml

```

# PV & PVC

```s
$ kubectl get pv
$ kubectl get pvc

# /home/vagrant/k8svolumes/mypv
# goto each node and create folder and file
$ echo "Node 1" > index.html
$ echo "Node 2" > index.html
$ echo "Node 3" > index.html

$ kubectl apply -f pvc.yaml
$ kubectl apply -f pv.yaml
$ kubectl get pv

$ kubectl apply -f pod.yaml
$ kubectl port-forward pod/mywebserver 8080:80
# browser http://localhost:8080/
$ kubectl get pv
$ kubectl get pvc


$ kubectl delete pod mywebserver
$ kubectl get pv
$ kubectl get pvc

# delete all to go in reverse order
$ kubectl delete pod mywebserver
$ kubectl delete pvc mypvc
$ kubectl delete pv mypv

# try and create PVC first
$ kubectl apply -f pvc.yaml
# Notice Pending status as there is no PV available
$ kubectl apply -f pv.yaml
# request fullfilled

```

# Storage Class

# minikube
```s
$ kubectl get sc
$ kubectl describe sc standard
$ kubectl apply -f sc-pvc.yaml
$ kubectl describe pv pvc

$ minikube ssh
$ cd /tmp/hostpath-provisioner/
$ kubectl apply -f sc-pod.yaml
$ kubectl port-forward pod/pod-sc 8080:80

```

# digital ocean
```s


```


