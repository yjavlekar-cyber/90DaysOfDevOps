# Resource Requests, Limits, and Probes
Your Pods are running, but Kubernetes has no idea how much CPU or memory they need — and no way to tell if they are actually healthy. 
Today we will set resource requests and limits for smart scheduling, then add probes so Kubernetes can detect and recover from failures automatically.

## Resource Requests and Limits
- First we created a pod yaml with resources set inside it.
<img width="971" height="445" alt="image" src="https://github.com/user-attachments/assets/e34ccc3a-fb6c-4f1f-9fd5-15cb80093e2d" />

- When we apply this manifest and describe the pod we can se there under volume section we have QOS category

<img width="1769" height="941" alt="image" src="https://github.com/user-attachments/assets/776ec2d5-3ccc-413b-8ac8-435707503c34" />

### QOS classes
- This classes are of three types which are not explicitily defined by us but it is decided keeping in mind how the resources distribution is done.
  1. Guranteed: where requests and limits for cpu and memory are exactly same
  2. Burstable: When limits and requests are not equal then this class is thier.
  3. Besteffort: when the resources are empty nothing is defined inside it.
 
- This matters because in kubernetes this classes determine in scenarios where any certain node is low on resources which pods would be evicted.
- besteffort------>burstable------>Guranteed
