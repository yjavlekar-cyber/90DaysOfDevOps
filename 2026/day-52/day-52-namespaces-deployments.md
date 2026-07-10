# Kubernetes Namespaces and Deployments
## Task 1: Explore Default Namespaces
- To list down all the namespaces in our system we can ran kubectl get namespaces which is currently giving us below list:
  
          NAME                 STATUS   AGE
          default              Active   46h
          kube-node-lease      Active   46h
          kube-public          Active   46h
          kube-system          Active   46h
          local-path-storage   Active   46h
  
     - default — where your resources go if you do not specify a namespace
     - kube-system — Kubernetes internal components (API server, scheduler, etc.)
     - kube-public — publicly readable resources
     - kube-node-lease — node heartbeat tracking
  - Then if we check inside kube-system there are around 10 pods running currentl which are control plane related we do not touch them.
  - to check pods inside a particular namespaces we will just use kubectl get pods -n/--namespace kube-system.

  <img width="1238" height="792" alt="image" src="https://github.com/user-attachments/assets/52fc269e-60b0-4b50-9bcd-962ab7b4a39e" />


## Task 2: Create and Use Custom Namespaces
- In this we will create namespaces of our own in two ways
   - imperative way : By running command kubectl create namespace dev.
   - declarative way: By creating a manifest file and applying it.
- To validate both namespaces are created we used kubectl get namespaces
- Then we run a pod with same image but in two different name spaces using -n
   - kubectl run nginx-dev --image=nginx:latest -n dev
   - kubectl run nginx-prod --image=nginx:latest -n production
- General way to list down the pods inside namespaces we saw in task 1 where we used kubectl get pods -n dev
- but we can also directly list down all the pods across all the namespaces by using below command
   - kubectl get pods -A

<img width="1890" height="974" alt="image" src="https://github.com/user-attachments/assets/c8bbde7d-4d90-4221-8a9d-28119cc4db63" />
