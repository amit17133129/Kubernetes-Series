# NodeSelector

# What is NodeSelector ?

NodeSelector is one of the forms of node selection constraint. nodeSelector is a field of PodSpec. This is a simple Pod scheduling feature that allows scheduling a Pod onto a node whose labels match the nodeSelector labels specified by the user.

You can check tha lables of each node by using below commnad
```
# command to check label on each node
kubectl get nodes --show-labels

```

## Setting Label

Now we will set the label on each node. Here i am setting the label as `gpu=true` in frst node (**k8sslave1**) whereas `gpu=false` in second node (**k8sslave2**).
```
# setting label as gpu=true in k8sslave1 node.
kubectl labale node k8sslave1 gpu=true

# setting label as gpu=false in k8sslave2 node.
kubectl labale node k8sslave1 gpu=false

```

## Launching pod with same label of node.
Now we will launch the pod with the same label as of what we have given in two slave nodes. Here i will be launching one pod with name `mypod` and giving the label as `gpu=true` in the *node selector* section and `mypod1` with the label of another node as `gpu=false`.

### mypod code with nodeSelector as gpu=true
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: mypod3
  name: mypod3
spec:
  containers:
  - image: centos:7
    name: mypod3
    command: ["/bin/sleep", "3650d"]
    resources: {}
  nodeSelector:
          gpu: "true"
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

```


### mypod code with nodeSelector as gpu=false
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: mypod3
  name: mypod3
spec:
  containers:
  - image: centos:7
    name: mypod3
    command: ["/bin/sleep", "3650d"]
    resources: {}
  nodeSelector:
          gpu: "false"
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

```

By this you will see that `mypod` will launching in the `k8sslave1` (**first node**) where as `mypod1` will be launching in `k8sslave2` (**second node**).

Here its detailed implementation of the NodeSlector. you click on node slector image to watch the video of it.

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/Kubernetes-Series/blob/main/Namespaces&Contexts/Images/node_selector.gif?raw=true">
</p>



[![Watch the video](https://cdn.journaldev.com/wp-content/uploads/2021/04/Kubernetes-nodeSelector-label.png)](https://youtu.be/oJygtTXP5Mc)
