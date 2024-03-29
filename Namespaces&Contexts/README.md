
# Namespaces & Contexts In [![Kubernetes](https://img.shields.io/badge/-Kubernetes-326CE5?style=flat-square&logo=Kubernetes&logoColor=ffffff)](https://kubernetes.io/)
<!-- <p align="center">
     Namespaces & Contexts
</p> -->

## What is NameSpace ?
Namespaces are a way to organize clusters into virtual sub-clusters — they can be helpful when different teams or projects share a Kubernetes cluster. Any number of namespaces are supported within a cluster, each logically separated from others but with the ability to communicate with each other.

## Creating Namespace
You can create your namespcae using below commands.
```
# checking your namespaces
kubectl get ns
kubectl get namespaces

# Creating namespace
kubectl create ns __namespace_name__
```

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/Kubernetes-Series/blob/main/Namespaces&Contexts/Images/namespace.gif?raw=true">
</p>

## What is Context ?
A context is a group of access parameters. Each context contains a Kubernetes cluster, a user, and a namespace. The current context is the cluster that is currently the default for kubectl : all kubectl commands run against that cluster.

```
# checking in which context your are currently
kubectl config get-contexts

#checking config file of kubernetes
kubectl config view

# setting up a new context
kubectl config set-context __context__name__   --namespace=__namespace__name__  --user=__user__name__ --cluster=__cluster__name

eg. you can refer below command
kubectl config set-context k8s-series-context --namespace=k8s-series --user=kubernetes-admin --cluster=kubernetes

```

After creating your own context, you can view using `kubectl config view` and you have to update the current-context in the config file. So using commands we can also do so. Just type `kubectl config use-context __context__name__`. You can refer this command `kubectl config  use-context k8s-series-context`. 

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/Kubernetes-Series/blob/main/Namespaces&Contexts/Images/contexts.gif?raw=true">
</p>

Now after being in the context which you have selected if check in which context you are using this command 
`kubectl config get-contexts` then you will get the following output.

```
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
          kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   
*         my-k8s-context                kubernetes   kubernetes-admin   k8s-series
```
The asterik * denotes that ou are using that context i.e `my-k8s-context`. Now if you launched the pod it will take bt default your corren-context and will launch in that context.

```
# You can run the pod using below command
kubectl run mpod --image=centos:7  -- /bin/sleep 3650d

# now if you hit the below command same pod will deploy in the same context(k8s-series).
kubectl -n k8s-series run mpod --image=centos:7  -- /bin/sleep 3650d

```

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/Kubernetes-Series/blob/main/Namespaces&Contexts/Images/pod-in-k8s-series.gif?raw=true">
</p>

>> Hope You like the explaination of namespaces and context. If yes click on * (star) above and save this repo for learning kubernetes and follow for more interesting learning stuffs.
