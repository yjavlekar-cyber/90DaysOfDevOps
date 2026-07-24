# Day 60 – Capstone: Deploy WordPress + MySQL on Kubernetes
Ten days of Kubernetes — clusters, Pods, Deployments, Services, ConfigMaps, Secrets, storage, StatefulSets, resource management, autoscaling, and Helm. 
Today I will put it all together. Deploy a real WordPress + MySQL application using every major concept I have learned.

## Task 1: Create the Namespace (Day 52)
- We first created a namespace.

      kubectl create namespace capestone
- After creating the namespace we set it as default in kube config.
  
      kubectl config set-context --set --namespace=capestone

## Task 2: Deploy MySQL (Days 54-56)
1) Created a secrets.yaml which will have our database secrets with type: opaque and stringData where we can insert data in string if we use only data we have to feed data in base64 encoding.
2) Then we created a headless service by declaraing the clusterIP as none headless service basically routes the traffice directly to the pods IP instead of creating and intermediator which is clusterIP.

<img width="1128" height="587" alt="image" src="https://github.com/user-attachments/assets/0824beed-6522-4a37-b7f6-16bfdaa1fe4e" />

   
3) Atlast we created a stateful set which deplopys our database:
   1) first we declaraed usuall apiversion,kind and metadata.
   2) then spec under whcih we defined replicas and our service name then template under which we have metadata and container info like image,ports,envFrom which ingests our secrets,resources and volumemounts.
   3) as we have also mentioned volumes inside temlates as template level we will declare volumeclaimtemplates as well.

<img width="1139" height="982" alt="image" src="https://github.com/user-attachments/assets/4a751e74-a07e-490e-acba-32edf8cc4069" />

5) we can exec into the pod and see our data is showing their
   
       kubectl exec -it pod-name -- mysql -u root -p

## Task 3: Deploy WordPress (Days 52, 54, 57)
- Here we first created a configmap which will have our host and db name.
- then we created a deployment where we ingested our configmap values and used already applied secrets which were already declaraed in database secrets
- we have also used liveness and readiness probe as well
