# Sources

- https://www.youtube.com/watch?v=9AKSLbfen6w
- https://docs.rancherdesktop.io/getting-started/installation/
  
# Why K8s?

The problem it's solving is "managing containers at scale".  
When having many containers across multiple VMs or servers, it becomes very difficult to manually handle things such as failovers, updates, or scaling.  
This is where Kubernetes comes in.  

Kubernetes is what we call a "container orchestrator", it orchestrates the deployment of containers over multiple machines, and its key benefits are:
- automation
- scalability
- high-availability (HA)

# Getting started with Kubernetes

The best way to learn Kubernetes is by installing and playing with **Rancher Desktop**.  
When you install Rancher Desktop, you'll also get **kubectl**, which is the CLI for Kubernetes.  

Since we'll be using kubectl commands a lot, we should simplify things by adding a **shorthand** in our shell config file.  
In my case, I use fish (friendly interactive shell), so I need to add the following to ~/.config/fish/config.fish:
```fish
# Add kubectl k alias
abbr k kubectl
```
Then, save the file and reload the shell via `source ~/.config/fish/config.fish`  

>[!note]
>The `abbr` command in Fish creates an abbreviation that expands when you press space, which is more ergonomic than a plain alias.

# Nodes & Clusters

A K8s node is basically a VM that is part of a K8s cluster.  
If you run `kubectl get nodes`, it will show all nodes in the current Kubernetes cluster.  

A K8s cluster can be one or multiple (virtual or physical) machines.  

# Core concepts

## Pods

A pod is the smallest unit of deployment on K8s.  
A pod is a collection of containers, and a few other things, in which we can run our application.  
```fish
kubectl run nginx --image=nginx
kubectl get pods
kubectl delete pod nginx
kubectl get pods
```

Pods are ephemeral, they can die and be replaced.  

## Deployments

A deployment is a collection of pods.  
It's a way to declare the "desired state" to K8s, for example:
```fish
kubectl create deployment my-nginx --image=nginx --replicas=3
kubectl get deployments.apps
kubectl get pods
kubectl delete deployments.apps my-nginx
```

And if we delete only one of the pods, we can see how fast K8s creates a new one to replace it:  
<img width="700" height="320" alt="image" src="https://github.com/user-attachments/assets/5d1c280d-5656-47ac-9294-dd59a8ba3bb1" />

That's because K8s' job is to make sure the current state of our cluster always matches the desired state.

# Networking

When K8s creates a new replacement pod, it doesn't get the same IP address as the replaced one.  
So, how can we make sure our pods are always able to talk to each other, and to talk with the outside world?  

## Introduction to K8s Services

A service is responsible for routing incoming traffic to the different pods in our cluster.  

This service is called **ClusterIP**, and its role is to provide internal service discovery and load balancing for pods, abstracting away ephemeral pod IPs so clients connect to a consistent endpoint.  

In other words, the ClusterIP service exposes an application running on Pods via a stable, internal virtual IP address accessible only within the cluster, enabling load-balanced communication to matching backend pods.  

To return to our Ningx example:  
<img width="678" height="224" alt="image" src="https://github.com/user-attachments/assets/2b3c30fd-bff7-449d-8543-a3588550d1c3" />

## Port forwarding

To access a K8s service from the host machine, we can use port forwarding: 
```fish
kubectl port-forward svc/my-nginx 8080:80
```
Port 80 is the port we've specified on service creation, and port 8080 is the one we'll use to access our service from the host machine.  
And now we can access our Nginx service from our web browser at http://localhost:8080/

15/20
