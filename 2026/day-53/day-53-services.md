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


