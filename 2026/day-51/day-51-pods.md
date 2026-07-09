# Kubernetes Manifests and Your First Pods
## Task 1: Create First Pod (Nginx)
1. Created below yaml file for nginx-pod.
<img width="684" height="484" alt="image" src="https://github.com/user-attachments/assets/3d9511b5-d727-4554-9f37-155f0a710199" />

2. After creating this file ran the command kubectl apply -f nginx-pod.yaml which created our pod.
3. To check pods status i ran kubectl get pods and kubectl get pods -o wide

<img width="1200" height="705" alt="image" src="https://github.com/user-attachments/assets/917689d7-4c84-4cd2-95ad-74d092e9a4eb" />

4. To check all the info of pods like namespaces,container details,conditions and volumes etc we can ask kubectl to describe our pod by running kubectl describe pod nginx-app.
<img width="1719" height="853" alt="image" src="https://github.com/user-attachments/assets/639003c6-0e67-4bac-88a6-ef08209dae61" />
5. we can also check logs by running kubectl logs nginx-app
6. Just like we used to enter in a container in docker here also using kubectl exec -it nginx-app -- /bin/bash we can enter and run commands inside our nginx pod.
<img width="1501" height="916" alt="image" src="https://github.com/user-attachments/assets/77ae0296-1890-4350-a69d-0d2da8bfcb8d" />

## Task 2: Created a Custom Pod (BusyBox)
<img width="877" height="390" alt="image" src="https://github.com/user-attachments/assets/5a5f78fc-cb52-4bd6-b193-6231fbd5eaa4" />
- I created a new busybox pod remembering how i created nginx pod keeping in mind basic structure such as apiVersion,kind,metadata and specs.
  
<img width="1390" height="384" alt="image" src="https://github.com/user-attachments/assets/b1b99e7d-511c-43dc-b832-ceb130067fea" />
- When we checked logs by running kubectl logs busy-box it give us hello from busy box as mentioned in above screenshot.
  
