## Kubernetes Services
You have Deployments running multiple Pods, but how do you actually talk to them? Pods get random IP addresses that change every time they restart. 
Services solve this by giving your Pods a stable network endpoint. Today you will create different types of Services and understand when to use each one.

## Why Services?
- Pod IPs are not stable.
- When pods gets replaced the IPs also change with them.
- also there are several pods so on which pods IP you will connect.
- All these problems can be solved with service
- Service give us stable IP and DNS.
- Load balancing across all the pods that match its selector

## Task 1: Deploy the Application
- I first created a deployment in the namespace dev

      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: web-app
        labels:
          app: web-app
      spec:
        replicas: 3
        selector:
          matchLabels:
            app: web-app
        template:
          metadata:
            labels:
              app: web-app
          spec:
            containers:
            - name: nginx
              image: nginx:1.25
              ports:
              - containerPort: 80

- Then applied it with kubectl apply -f deployment.yaml -n dev
- To check the IP's of this pods created through our deployment we can check using command kubectl get pods -o wide -n dev
<img width="1457" height="383" alt="image" src="https://github.com/user-attachments/assets/71166ba5-4a98-4634-83d1-a3e916667a57" />

## Task 2: ClusterIP Service (Internal Access)
ClusterIP is the default Service type. It gives your Pods a stable internal IP that is only reachable from within the cluster.

- First created a service.yaml which includes kind as service then its name in metadata.
- And in spec we have matched our labels from deployment as selector in service to connect both
- then type as clusterIP which gives us stable IP which accesable inside our cluster
- and port from which our traffic will connect to a target port.
- so we were able to do this inside a port on our terminal we cannot do this because this operates on pod level.
  
      apiVersion: v1
      kind: Service
      metadata:
        name: web-app-clusterip
      spec:
        type: ClusterIP
        selector:
          app: nginx
        ports:
        - port: 80
          targetPort: 80


- To check this we will first run one pod in our cluster with kubectl run test-client --image=busybox:latest --rm -it --restart=Never -- sh
- Then inside the pod  wget -qO- http://clus-service.dev .dev is basically our namespace.
- the result of which is nginx page
- this tells us that in same cluster through service we can connect different pods.

## Task 3: Discover Services with DNS
- kubernetes has built in DNS server.
- Every service created in kubernetes gets it own DNS entry automatically.
        <service-name>.<namespace>.svc.cluster.local
- To check this first we run kubectl run dns-test --image=busybox:latest --rm -it --restart=Never -n dev -- sh in our namespace.
- Then inside this pod if we do nslookup clus-service(which is our servce name) which shows our service's cluster IP and its Domain name.
- It will show us
  
         Name:   clus-service.dev.svc.cluster.local
         Address: 10.96.132.74

<img width="1772" height="624" alt="image" src="https://github.com/user-attachments/assets/cefa1613-102a-499d-8eca-0d0e7013635b" />

## Task 4: NodePort Service (External Access via Node)

- Through Nodeport we can expose our application on a port on every node due to this we can excess our service outside the cluster as well.
- First we created a service.yaml which uses type-NodePort and seprate nodePort which routes traffic from port to targetport to nodeport which is accesiable on our terminal and outside.
  
      apiVersion: v1
      kind: Service
      
      metadata:
        name: node-service
      
      spec:
        selector:
          app: nginx
      
        type: NodePort
      
        ports:
          - port: 80
            targetPort: 80
            nodePort: 30020
- If we curl our nodes IP with our nodeport it will bring back our nginx page because obiviously our pods are of nginx.
<img width="553" height="475" alt="image" src="https://github.com/user-attachments/assets/bfe7c1cb-8cb6-4367-b5e7-36fe502152ca" />


## Task 5: LoadBalancer Service (Cloud External Access)
- LoadBalancer service type routes or balances the external traffic routes traffic to our nodes.
- For this we created serviec.yaml with type: LoadBalancer
- Once we apply this and when we do get services external IP will be pending
- because loadbalancer service is only helpful if we have provisioned loadbalancer on cloud
  <img width="1066" height="391" alt="image" src="https://github.com/user-attachments/assets/dd68f27c-fff5-4d82-b8ae-ecda7784e3d2" />
  <img width="647" height="479" alt="image" src="https://github.com/user-attachments/assets/90bfd9c4-fa7d-4b8c-8789-4cd2d3cf0fdb" />


|  Type | Accessible  | From	| Use Case |
|ClusterIP | Inside the cluster only | Internal communication between services |
| NodePort | Outside via <NodeIP>:<NodePort> | Development, testing, direct node access |
| LoadBalancer |	Outside via cloud load balancer | Production traffic in cloud environments |

