# Kubernetes Architecture and Cluster Setup
## Task 1: Kubernetes Story
### 1.Why was Kubernetes created? What problem does it solve that Docker alone cannot?
- To solve the problem of auto scaling and auto healing google launched a tool called "Borg".
- which was then donated by google to open source.
- The linux foundation and CNCF (cloud native computing foundation) started maintaining it and they afterwards
  changed its name from Borg to Kubernetes.
- So with docker we can create and run apps in contenarize form no problem but what if the traffic increases?
- what if we need to contenrize our application on a large scale for larger market?
- What if we want our app to run on O downtime? what if we want our containers to auto scale and auto heal?
- So in such cases we can use kubernetes to orchestered our application on larger scale and all the above problems whcih we were facing when using docker can be dealt with kubernetes.
### 2.What does the name "Kubernetes" mean?
- Kubernetes name is derived from ancient greek word κυβερνήτης (pronounced koo-burr-NET-eez), which translates to "helmsman," "pilot," or "governor).
- Which means a captain who leads and navigates our containers in this context of cloud computing.

## Kubernetes Architecture
<img width="2689" height="1746" alt="IMG_3431" src="https://github.com/user-attachments/assets/a7a7df48-27cc-44c2-9727-7d25ccbdfbdc" />

1) What happens when you run kubectl apply -f pod.yaml? Trace the request through each component.
   - When we run the above command kubectl commuincates with API server which writes down to ETCD and then checks with Scheduler for to check if space available on node.
   - Then scheduler on selected node talks to kubelet to apply the pods through container runtime.
 
2) What happens if the API server goes down?
   - If API server goes down on a control plane the already existing worker nodes or pods will keep running.
   - But when it comes to descion making part where we will need to schedule new pod that time we will not be able to operate.
  
3) What happens if a worker node goes down?
  - The node-controller from control manager checks for the worker nodes health.
  - Then scheduler which schedules pods finds healthy nodes where it can run pods.
  - In here our deployment.yml plays major role for auto healing where it keeps checking the actual state and desired state
  - If it finds any gap tried to fill it but if we only have pod.yml for our application once to worker nodes are down those pods will also cease to exist.
## Kubectl installation
- So in order to communicte with our clusters we will first need a client/kubectl which will comuunicate with our clusters.
- Kubectl is CLI tool which helps us communicate with our clusters.
- To install we can we visit official documentation provided by kubernetes.
- As checked we already have kubectl installed.
- 
  x<img width="643" height="115" alt="image" src="https://github.com/user-attachments/assets/4d6d5f25-d28b-42c9-95d4-1a0b05cf5c7b" />


## Cluster Set-up
- To create cluster there several methods listed below:
   - Kubeadm: which allows us to create bare metal K8s clusters.
   - Kind: Kind allows us to install and run kubernetes inside docker the full form of kind is kubernetes inside docker.
   - minikube: this is same as kind
   - EKS: Elasctic kubernetes service is orchestration service provided by amazon web services.
   - AKS from azure
   - GKE from GCP (goggle kubernetes engine)

- We will be using Kind method for practice
  - prerequisites for which are
    - docker
    - kubectl
   
- we first created a kind-config.yaml
<img width="1090" height="399" alt="image" src="https://github.com/user-attachments/assets/c644fdb7-6b43-404a-ada9-f5b195d78342" />
  
- Then we run kind create cluster --config=kind-config.yaml which creates our cluser as per the config in the file.
<img width="1069" height="301" alt="image" src="https://github.com/user-attachments/assets/5f402a52-d1e8-4bef-9f5f-43dd5ae386f5" />

- Commands used:
  1) kind create cluster --config=filename.yaml - To create cluster
  2) kind get clusters - to get lists of clusters live.
  3) kubectl get nodes - This commands list downs total nodes created.
  4) kubectl cluster-info - This gives us info on where control-plane and core dns is running.
  5) kubectl describe node <node-name> - To get detailed info of one particular node.
  6) kubectl get pods -A - See ALL pods running in the cluster (across all namespaces)
  7) kubectl get namespaces - To list all namespaces
  8) kind delete cluster --name=nameofcluster
  9) kubectl config current-context - To check which cluster kubectl is currently connected
  10) kubectl config get-contexts - list all available contexts (clusters)
  11) kubectl config view - To see whole kubeconfig kube config tells us all the clusters,users and contexts.




