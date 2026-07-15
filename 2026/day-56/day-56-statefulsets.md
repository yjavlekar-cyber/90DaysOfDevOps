# Kubernetes StatefulSets
Deployments work great for stateless apps, but what about databases? You need stable pod names, ordered startup, and persistent storage per replica.
Today I will learn StatefulSets — the workload designed for stateful applications like MySQL, PostgreSQL, and Kafka.

## Task 1: Understand the Problem
- First created and aplied nginx deployment in namespace dev
- then listed all the pods and tried deleting one of the pod.
- but as i checked the new generated pod has a different name.
- that is the main issue with stateless deployments it starts every time new it does not pick up from where it was left.
- Why would random pod names be a problem for a database cluster?
   - we might face in checking logs,checking metrics and monitoring etc.

<img width="1496" height="655" alt="image" src="https://github.com/user-attachments/assets/2d1c945b-a2f7-43d6-b00a-53fe2f13fdeb" />

## Task 2: Create a Headless Service
- basiclly when we use clusterIP it gives a seprate ip to our service through which traffice is routed to pods.
- but in headless service we set clusterip as none so there is no mediator the traffic is directly routed to pod IPs
- created a service yaml where declaraed clusterip as none.
- as checked the clusterip coloumn is none as well.

<img width="536" height="352" alt="image" src="https://github.com/user-attachments/assets/3001326a-488f-483f-a97d-682b4321850d" />

## Task 3: Create a StatefulSet
- now that we have headless service we will create a stateful set
- statefulset is just like deployment creates pods but with predictable and ordered names.
- and attaching them with the headless service maps their IP to a DNS so that they are reacheable inside the cluster using that
- first we have already created a headless service yaml and apllied it
- Then we created a stateful set refer below yaml
  
<img width="1127" height="706" alt="image" src="https://github.com/user-attachments/assets/9d35f2b3-06d6-434f-bbae-55230d414c1d" />

- In this we have used our normal templayte to create containers.
- but the kind is statefulset
- a seprate volumeclaimtemplate we have used
- and when we apply this we can see both the pods and the pvc created have orederd names
<img width="1447" height="484" alt="image" src="https://github.com/user-attachments/assets/f1555ec7-4d2a-4d7d-87f5-ebe10eed4c76" />

## Task 4: Stable Network Identity
Each StatefulSet pod gets a DNS name: <pod-name>.<service-name>.<namespace>.svc.cluster.local
- In here we first created a busybox pod and exec into it
- then we did nslookup for our stateful pod names with the dns name it returened back our IP
- which proves that services with clusterIP none directly gives DNS for IPs of our pods.
  
<img width="1280" height="676" alt="image" src="https://github.com/user-attachments/assets/1d4150ce-710b-4ce0-a16f-be93987acc66" />


## Task 5: Stable Storage — Data Survives Pod Deletion
- as we have our pvc attached to our pods
- we did exec into our pod and created a file
- and then deleted the same pod the stateful set regenerated the pod
- and now when I checked the files are still their

## Task 6: Ordered Scaling
- To scale up and down we did it just like deployment
- used commands kubectl scale statefulset staful --replicas=5
- This scales up and down in order when doing scaling up it does like 0,1,2 if down 2,1,0

<img width="1548" height="736" alt="image" src="https://github.com/user-attachments/assets/3119dc1f-dd78-45a1-a761-b723cb2573d1" />


