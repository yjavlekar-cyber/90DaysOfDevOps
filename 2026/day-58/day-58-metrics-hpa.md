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
  
