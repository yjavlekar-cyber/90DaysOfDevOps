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

## Task 4: Expose WordPress (Day 53)
- Then we created a nodeport service so that we can access it through our browser.
- as we were using kind we have to do port forwarding.

## Task 5: Test Self-Healing and Persistence
- Then if we delete the pods we can see as we the self healing and also data persistance because of the pvcs

## Task 6: Set Up HPA (Day 58)
- Then we set up an horizontol pod scaler which will keep mini 2 and max 10 pods if the usage crosses 50 percent utilization.

## Project flow
- first we created a statefulset for our mysql pods which gets secrest from the secrest yaml and a for that we have also created a headless service.
- then we created a wordpress deployment which uses secrets from the db and a configMap variables where we have defined the host which is the services linked to our db pods.
- and then again we created a nodeport service to access word press from browser.
- So how all this is connected:
   - the traffic travels through nodeport into wordpress pod which then usues db host which is our service through that service we are entering db for the data.
