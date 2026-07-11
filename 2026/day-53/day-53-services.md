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
