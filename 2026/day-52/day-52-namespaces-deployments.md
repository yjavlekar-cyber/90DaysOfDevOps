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

## Task 3: Created my First Deploymennt
<img width="628" height="488" alt="image" src="https://github.com/user-attachments/assets/a79a2b52-d161-433f-95ad-314aa1e3d00c" />

- Created a deployment.yaml where below details we have mentioned:
  - apiVersion: which is apps/v1 which is current version
  - kind: which is our Deployment'
  - metadata: which includes name,namespace and label
  - spec: this will have replicas for our desired state then selector label to inform that as per this label replicas should be made
      - template: where we will give details of our container like its image and port and a label which we have give in replicaset.

- Then we ran kubectl apply -f deployment.yaml and the deployment was successfully created.
- To list downn our created deployment we can kubectl get deployments -n dev if we do not use the extension -n it will assume that we are asking deployments from default namespace.
- we can also list down pods directly using kubectl get pods -n dev
  
<img width="1893" height="521" alt="image" src="https://github.com/user-attachments/assets/885a7c9f-0c84-442d-b01b-5eedd934bbb5" />

## Task 4: Self-Healing — Delete a Pod and Watch It Come Back

- The major difference between a standalone pod and pods created using deployment is self healing
- When we create a pod using pod.yaml the created pod if we delete it is gone forever.
- but as deployment is a manifest file which defines a desired state it like in above example we define 3 replicas
- now this 3 replicas are desired state even if we delete one scheduler will create new pod to match the desired state mentioned in deployment.yaml

  
## Task 5: Scale the Deployment
