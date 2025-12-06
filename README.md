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

If you run `kubectl get nodes`, it will show all nodes in the current Kubernetes cluster.  

Since we'll be using kubectl commands a lot, we should simplify things by adding a **shorthand** in our shell config file.  
In my case, I use fish (friendly interactive shell), so I need to add the following to ~/.config/fish/config.fish:
```fish
# Add kubectl k alias
abbr k kubectl
```
Then, save the file and reload the shell via `source ~/.config/fish/config.fish`  

>[!note]
>The `abbr` command in Fish creates an abbreviation that expands when you press space, which is more ergonomic than a plain alias.

...

<img width="700" height="320" alt="image" src="https://github.com/user-attachments/assets/5d1c280d-5656-47ac-9294-dd59a8ba3bb1" />


5/20
