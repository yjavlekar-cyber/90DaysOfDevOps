# Metrics Server and Horizontal Pod Autoscaler (HPA)
## Task 1: Install the Metrics Server and explored kubectl top

- first we did wget https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
- Then edited componenets.yaml and applied it.
<img width="942" height="416" alt="image" src="https://github.com/user-attachments/assets/646c8bf0-6b19-4eec-888f-17588b7d6e44" />

- In here we can see our metrics server is installed.
- then if we use top with kubectl we can check cpu usage and memory usage details.
- like in above if we see we did kubectl top nodes it gaves us our two nodes cpu usage and memory usage.

## Task 2: Create a Deployment with CPU Requests
- wrote deployment which uses hpa image which is cpu intensive
- used resources cpu 200m
- and expose it as a service with port 80
- when we check kubectl top pods it gave us error: Metrics not available for pod default/hpa-deploy-b7f79c7bb-7g4k6, age: 16m10.554398652s
- because the hpa is cpu intensive and we only have 200m cpu which resulted the container being in creation stage

<img width="825" height="466" alt="image" src="https://github.com/user-attachments/assets/b168769a-4db5-4133-960d-54aa40872169" />

  
## Task 3: Create an HPA (Imperative)

<img width="1684" height="634" alt="image" src="https://github.com/user-attachments/assets/7a961596-82fd-4f1a-b36a-0bdff427b909" />

- In this we have our deployment which we have autosacled as per the cpu percent
- we ran command kubectl autoscale deployment deployment-name --cpu50% --min=1 --max=5
- This basically tells that avaerage cpu usage should be 50% only so whenever suppose the usg will go above 50 it will create pods to bring it down to 50.
- If we run kubectl get hpa (horizontal pod autoscaler) it will shows use our cpu usage and target min and max pods then replicas etc.


## Task 4: Generate Load and Watch Autoscaling

<img width="1852" height="767" alt="image" src="https://github.com/user-attachments/assets/6ae2f6d9-6827-45f1-9f1f-9237d32fbc5b" />

- In this task first we run a container which will generate load
- then when we watch our pods live we can see the load has been generated and once we check pods autoscaler has created max 5 pods for that matter
- and when we stopped the load-generaor and then if we watch the load slowly came down to 0%
- but the scaled down from 5 pods to desired 3 pods took 5 minutes.

  
## Task 5: Create an HPA from YAML (Declarative)
<img width="1363" height="803" alt="image" src="https://github.com/user-attachments/assets/6db682aa-37be-414c-baa8-6eff0376b823" />

- Earlier we used imperative way with commands now we will use declarative way where we will create yaml file
- like earlier first we have declaraed min and max replicas
- then cpu utilization
- we have one additional block of behavior which declares:
  - how much time it should take to scaleup or scaledown
  - where in scaleup policy max decides which ever policy gives us higher number of pods.
  - and in scaleup there are two policies:
     - first is where it calculates how many pods are currently running and add that much of pods
     - or 4 pods every 15 sec
  - where in scale down min means lowest number where we have define policy which calculates 10percent of running pods and delete them every 60seconds

