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

After that run the file using `kubectl create -f daemonset.yaml` and then you can check the daemonset resources using `kubectl get ds`. *Here ds means daemonset*. 
Check the below gif to go through the hands part. 

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/images/blob/main/images/creating%20daemonset.gif?raw=true">
</p>
