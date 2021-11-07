## Namespaces & Contexts


## What is NameSpace ?
Namespaces are a way to organize clusters into virtual sub-clusters — they can be helpful when different teams or projects share a Kubernetes cluster. Any number of namespaces are supported within a cluster, each logically separated from others but with the ability to communicate with each other.

## Creating Namespace
You can create your namespcae using below commands.
```
# checking your namespaces
kubectl get ns
kubectl get namespaces

# Creating namespace
kubectl create ns name_space_name
```

<p align="center">
  <img width="1000" height="550" src="https://github.com/amit17133129/Kubernetes-Series/blob/main/Namespaces&Contexts/Images/namespace.gif?raw=true">
</p>
