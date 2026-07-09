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
  
## Task 3: Imperative vs Declarative
- To create pods or any of the objects in kubernetes they are two ways
   - Declarative - Where we create yaml files and then run apply.
   - Imperative - In this approach we run commands to create the object using kubectl run as mentioned in below snap.
     also once the pod is create we can run command kubectl get pod redis-pod -o yaml which will give us the yaml file created by kubernetes itself after we run our imperative command.

<img width="1175" height="849" alt="image" src="https://github.com/user-attachments/assets/e5b6e03a-6339-4707-b000-00a64896bec5" />


## Task 4: Validate Before Applying
- Before applying our actual yaml we can also validate it by using --dry-run=client and --dry-run=server
- First i ran this command with proper yaml which validated the yaml and gave output that yaml is unchanged after it was applied.
- Then i deliberately messed up the syntax of the yaml and when i ran the command after that it gave error and informed me on the first two-three lines what might be the reason.

<img width="1636" height="899" alt="image" src="https://github.com/user-attachments/assets/d79efd41-1ec7-48ef-9077-748af0644651" />

## Task 5: Pod Labels and Filtering
While creating our pods we have give labels to them we now see some commands through which we can list down our pods with their labels and also see how we can delete certain given labels as well.

- kubectl get pods --show-labels : This command will help us to list down the pods with their labels.
- kubectl get pods -l app=nginx : This will only list the pods which have this as label.
- kubectl label pod busy-box environment- : This command will remove the environment label from pod named busy-box.
- kubectl label pod nginx-app environment=dev : Through this we can add a label to our existing pod.

<img width="1365" height="704" alt="image" src="https://github.com/user-attachments/assets/1f61d961-8e33-46aa-b65d-61ec08d5efd0" />

## Task 6: Clean Up
- To clean up or delete we can ran kubectl delete pod nginx-app or we can delete through yaml kubectl delete -f nginx-pod.yaml
 - kubectl delete pod pod-name
 - kubectl delete -f pod.yaml
<img width="696" height="397" alt="image" src="https://github.com/user-attachments/assets/196c97c5-20d6-418b-8a3b-044e859d4657" />

