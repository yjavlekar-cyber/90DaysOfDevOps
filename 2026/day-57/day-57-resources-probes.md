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


## OOMKilled — Exceeding Memory Limits

<img width="1901" height="977" alt="image" src="https://github.com/user-attachments/assets/1c9b27d5-e1b3-46d6-b372-24a9509363af" />

- In this what we have done is created an another pod which has limit set for memory of 100M
- but in command we have asked it to use around 200M
- because of this whenever container tries to start it is killed with exit code 137 which is basically due to OOM (out of memory).
- and as it gets killed the pod again tries to start and again it goes into OOM this loop continues hence our pod is going into crashloopbackoof state.

## Pending Pod — Requesting Too Much
- In this we have assigned resources which are way out of expectiations where our cpu is 100 as we have not mentioned M it assumes that we want whole 100 cores.
- then in memory we normally go for Mi but here we have used Gi which is way above normal we can refer below table as well.

| Unit | Resource Type | Meaning | Example | Actual Value |
|------|---------------|---------|---------|---------------|
| (no suffix) | CPU | Whole core(s) | `cpu: "1"` | 1 full CPU core |
| `m` | CPU | Millicore (1/1000 of a core) | `cpu: "100m"` | 0.1 core (10% of one core) |
| `m` | CPU | Millicore | `cpu: "500m"` | 0.5 core (half a core) |
| `Ki` | Memory | Kibibyte (1024 bytes) | `memory: "128Ki"` | 128 × 1024 bytes |
| `Mi` | Memory | Mebibyte (1024 Ki) | `memory: "128Mi"` | ~134 million bytes |
| `Gi` | Memory | Gibibyte (1024 Mi) | `memory: "1Gi"` | ~1.07 billion bytes |
| `Ti` | Memory | Tebibyte (1024 Gi) | `memory: "1Ti"` | rarely used at pod level |
| `K`, `M`, `G`, `T` | Memory | Decimal versions (1000-based, not 1024) | `memory: "128M"` | 128,000,000 bytes |

- because of our unxpected or abnormal resource allocation the pod status got into pending and it threw an error of insufficient cpu and memory which was obvious.

<img width="1910" height="772" alt="image" src="https://github.com/user-attachments/assets/0f78f94f-077a-4507-9c5f-af2e1809e128" />

