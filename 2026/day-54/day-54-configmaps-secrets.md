# Kubernetes ConfigMaps and Secrets
Your application needs configuration — database URLs, feature flags, API keys. Hardcoding these into container images means rebuilding every time a value changes. 
Kubernetes solves this with ConfigMaps for non-sensitive config and Secrets for sensitive data.

## Task 1: Create a ConfigMap from Literals
- config map store are non-sensetive varibles which we can use in deployment instead of hardcoding them.
- First method of creating them is imperative method where through CLI we give command and the yaml for the configmap gets created.
- The command usess name of the file and --from-literal for every new variable to store just like below command.
    - kubectl create configmap app.config --from-literal=APP_ENV=production --from-literal=APP_DEBUG=false --from-literal=APP_PORT=8080
- once created we can also get its yaml by using
   - kubectl get configmaps app.config -o yaml
- and if we describe it we will also show us the data stored in config map
   - kubectl describe configmaps app.comfig
- I can also see that data stored in a configmap is not encoded it is stored in plain text and is visible.

<img width="1258" height="750" alt="image" src="https://github.com/user-attachments/assets/5ee5c7a7-4f73-46aa-b8b9-9ae2b9effbdd" />

## Task 2: Create a ConfigMap from a File
- Now we will create a .conf file which will create our configmap file.
- First we created a nginx.conf file where we mentioned http server should listen on port 80 and should return healthy if endpoint health returns 200.
- then we will use this file name in imperative way
   - kubectl create configmap nginx-config --from-file=default.conf=nginx.conf
- first we created our config file then gave it to default.conf is equal to that in command.
- and now if we do kubectl get configmap nginx-config -o yaml we can see the yaml of the same.
- we can also create a yaml file of the same but instited of spec we insert data in it.

<img width="1397" height="741" alt="image" src="https://github.com/user-attachments/assets/342ab398-069d-4a23-821c-945d63af29e8" />

## Task 3: Use ConfigMaps in a Pod
### Through CLI
- to use our congifurations created using imperative way we will use it under containers as envFrom:configMapRef and name of the configmap created.
- If we check the logs of busybox container we created as below yaml it prints the variables declared in app.config

<img width="1018" height="532" alt="image" src="https://github.com/user-attachments/assets/d3baa1f5-a234-4efd-b6d4-a02a6ff17269" />

### Through file
- we have created nginx.conf file in that if endpoint is health return healthy
- To use it in simple nginx pod.yaml
- first before containers under spec we have mapped volumes:name:configMap:name(name of the configmap created by file)
- and inside the container we have mentioned volumeMounts:name(sameasabovevolname):mountPath(which we set deafult at the time of creation of that config)

<img width="867" height="572" alt="image" src="https://github.com/user-attachments/assets/46baafc8-8788-439a-aa75-09dc50c91080" />


## Task 4: Create a Secret
- created a secret with imperative way using below command
  - kubectl create secret generic db-secrets --from-literal=DB_USER=admin --from-literal=DB_PASSWORD=s3cureP@ssw0rd
  - them to check the yaml i ran kubectl get secrets db-secrets -o yaml
  - we can see in secrets the values get encoded in base64 format
  - to decode we echo our value through pipe into base64 --decode
    -  echo 'value' | base64 --decode

<img width="1645" height="435" alt="image" src="https://github.com/user-attachments/assets/7f9ed20b-58f7-47e3-a3dc-12fb79cd773f" />

## Task 5: Use Secrets in a Pod
- In this task we created an nginx pod where we first assigned at the spec level our secrets.
- then we injected onky DB_USER from db-secrets and afterwards we attached the db-secrets as volume
- once the pod was created when i did exec commands inside the pod like ls the folder /etc/db-user it listed the files of the secrets it made also if we do cat inside that container the secrets are not encoded.
   - kubectl exec pod/nginx-app -- ls /etc/db-secrets

 <img width="1156" height="720" alt="image" src="https://github.com/user-attachments/assets/027ec748-5221-4278-88cf-bbf0f0a53540" />

