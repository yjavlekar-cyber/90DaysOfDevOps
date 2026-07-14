## Persistent Volumes (PV) and Persistent Volume Claims (PVC)
Containers are ephemeral — when a Pod dies, everything inside it disappears. 
That is a serious problem for databases and anything that needs to survive a restart. Today you fix this with Persistent Volumes and Persistent Volume Claims.

# Task 1: See the Problem — Data Lost on Pod Deletion
- In this task i first created a container in a pod with alpine image.
- In this first we have set an emptyDir in volumes
- Then in volumeMounts we hae mentioned the path /data which is inside the emptyDir from volumes.
- Then we inserted one command which is basically a while loop
- so bacially when we insert command in a pod when the command is executed pod dies hence we have used while loop.
- This loop says while true pod is running echo the date in /data/message.txt
- after the pod is live if we exec a cat command to read the txt file we can the timestamps are wriiten over there.
- but as soon as we delete the pod and recreate it it writes new data to it but old one is gone forever.

<img width="1211" height="469" alt="image" src="https://github.com/user-attachments/assets/1aaa704c-cef1-44af-a371-2108c6440ded" />

## Task 2: Create a PersistentVolume (Static Provisioning)
- In this task we created a persistent volume which uses stroageClassName as manual.
- has access mode for readwriteonce
- storage capacity of 1Gi
- and hosted in path /mnt/data

<img width="1039" height="482" alt="image" src="https://github.com/user-attachments/assets/4538c884-9f67-4a82-b2c2-5b48d6ebd312" />

## Task 3: Create a PersistentVolumeClaim
- Persistent volume claim is basically we are claiming storage from our earlier created pv.
- pvc identifies pv with the help of storageclassname
- in this we are getting resources through requests 500mb storage
  
<img width="615" height="389" alt="image" src="https://github.com/user-attachments/assets/ebdf4b57-3802-4099-8778-96304d0ecc1d" />

## Task 4: Use the PVC in a Pod — Data That Survives
- so now that we have pvc where we have claimed a certain amount of storage.
- we can now use it inside our pod where on spec level we have claimed our pvc
- and in container level we have mounted the same to where our data gets stored.

<img width="1173" height="452" alt="image" src="https://github.com/user-attachments/assets/20de1cf4-c01c-4e51-a158-c50e9c04dee4" />

## Task 5: StorageClasses and Dynamic Provisioning
- first i ran kubectl get storageclass and then kubectl describe storageclass
<img width="1894" height="367" alt="image" src="https://github.com/user-attachments/assets/9d748434-5005-40ce-846c-56f6c74b4f95" />

- In our default storage class
   - first we have a local provisioner instead of creating persistent volume and them claiming it we can just direct claim the storageclass as standard we dont need to create pv provisioner creates a folder in
     local path whenever pod requires storage.

  - Then we have reclaimpolicy which is for now delete that means if we delete our pvc our data is also gone.
  - then third is voluimebinding mode which is mapped to waitforfirstconsumer which means when we create pyc it will be in pending status until we claim it.
 

## Task 6: Dynamic Provisioning
- Dynamic provisining is basically using standard staorageclass which will wait for our pod to generate only then it will automatically create a pv.
- in our pvc yaml we directly use storageclassname standard
- Im pod yaml our claimName will change to current pvcs metadata name.
- <img width="1726" height="626" alt="image" src="https://github.com/user-attachments/assets/09b4e24f-0fdd-4513-a0f8-e347d55285bf" />


## What I learned
- I learned how to keep our data safe if pod gets replaced or deleted by using pv and pvc
- difference between static provisioning and dynamic provisioning
