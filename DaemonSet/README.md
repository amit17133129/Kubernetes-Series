<p align="center">
  <img width="1000" height="550" src="https://cdn.journaldev.com/wp-content/uploads/2021/04/Kubernetes-Daemonset.png">
</p>

# What is DaemonSets ?

A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.

Some typical uses of a DaemonSet are:

    running a cluster storage daemon on every node
    running a logs collection daemon on every node
    running a node monitoring daemon on every node

In a simple case, one DaemonSet, covering all nodes, would be used for each type of daemon. A more complex setup might use multiple DaemonSets for a single type of daemon, but with different flags and/or different memory and cpu requests for different hardware types.

# Creating your first DaemonSet
The yaml structure of daemonset is same as deployment. Just edit the deployment file while creating a dry-run of your deployment resource you will get yaml file of your deploymen. you can use below commands to create your deployment file.
```
kubectl create deployment mydaemonset --image=centos:7 --dry-run -o yaml > daemonset.yaml
```
After running the above command you will get a daemonset.yaml file and the you can edit the following things to launch a daemonset in your cluster.
## Need to do changes in deployment file to get a daemonset
1. Change the name of kind from Deployment --> DaemonSet
2. Remove relicas 
3. Remove   strategy: {}
4. Remove status: {}

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/creating%20daemonset.gif?raw=true">
</p>


After that run the file using `kubectl create -f daemonset.yaml` and then you can check the daemonset resources using `kubectl get ds`. *Here ds means daemonset*. 
Check the below gif to go through the hands part. 

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/creating%20daemonset.gif?raw=true">
</p>

## Restricting the DaemonSet to launch the pod in one node using Node Selector.
As you know daemonset is meant to launch the resources in all the respective nodes, but we can also retrict the resources to be launched in one of the node or your respective give nodes. This will help us to launch the application in a required node. Imaginge your application needs more ram,cpu,gpu to start. So in that case we can able to launch the application in the required nodes.

Fisrt we have to label the nodes using the below command `kubectl label node k8sslave1 gpu=true` and the another node will be labeled as `kubectl label node k8sslave2 gpu=false`. The node k8sslave1 has a label of `gpu=true` whereas node2 'k8sslave2' has a label of 'gpu=false'.

So we can launch the pods through daemonset within the required node. If the application running inside the pod requires more gpu so we can launhced in node1 i.e., k8sslave1 and vise versa.


<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/DaemonSet_nodeSelector.gif?raw=true">
</p>

