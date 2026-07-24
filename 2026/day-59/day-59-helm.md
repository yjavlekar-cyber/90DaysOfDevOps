# Helm — Kubernetes Package Manager
## Helm installation
- first we installed snap then doing sudo snap install helm --classic
- to confirm we wo helm version
  
      version.BuildInfo{Version:"v4.2.3", GitCommit:"43e8b7feece8beb0fcba47059ec9b522fd929a64", GitTreeState:"clean", GoVersion:"go1.26.5", KubeClientVersion:"v1.36"}



    my-app/
    ├── Chart.yaml          # Metadata about the chart (name, version, API version)
    ├── values.yaml         # Default configuration values for variables
    ├── templates/          # Directory containing customizable Kubernetes manifest files
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   └── _helpers.tpl    # Helper snippets shared across templates
    └── charts/             # Optional directory containing dependent charts

1) Chart is helm is basically a folder where we keep our files and templates as mentioned in the above file structure.
2) Release so release is basically when we install helm chart locally the copy or the actuall installation happens is called an release.
    we list down release by using *helm list* and every time when we install a same chart helm tracks it by giving it a
    unique revision number which can help us rollback easily by doing *helm rollback name rev number*
3) Repository- This is where we keep our charts which can be pulled afterwards

## Task 2: Add a Repository and Search
- To add repo inside our kubernetes we ran

      helm repo add bitnami https://charts.bitnami.com/bitnami

- Once repo is added if we do helm search repo bitnami we will get the list of all the charts bitnami has as shown in below snapshot.
<img width="1325" height="953" alt="image" src="https://github.com/user-attachments/assets/9b0be62e-ab10-4206-a2fe-51acd136319a" />

## Task 3: Install a Chart
- First we installed nginx chart from bitnami by running helm install nginx bitnami/nginx
- Then as we know that charts are basically folders that we can verify using kubectl get all we can see deployment and all that is also created.
    
<img width="1899" height="850" alt="image" src="https://github.com/user-attachments/assets/d240240e-2489-499f-9d91-4a83ab621f84" />

<img width="1071" height="307" alt="image" src="https://github.com/user-attachments/assets/8158d90e-6fa6-48e8-b502-7092a14f3e42" />

- If we do helm list it will give us an list of charts installed on our machine with their revision number

      NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
      nginx   default         1               2026-07-23 03:04:46.21029059 +0000 UTC  deployed        nginx-25.0.14   1.31.3 
    

### How many Pods are running? What Service type was created?
- To answer the this i can say there is only one pod of nginx was created and service type was lead balancer as nginx himself acts as a load balancer.


## Task 4: Customize with Values
- First we check default values of our current bitnami/nginx chart which is huge file.
- Then we upgraded our bitnami/nginx with 3 replicas and service type as nodeport by running below command
  
       helm upgrade nginx bitnami/nginx --set replicaCount=3 --set service.type=NodePort
- now if we check our helm list our revision number is 2.
- then we created a custom values yaml and installed a seprate nginx chart and in release we can see two versions.
- if we do helm get values name of release we can see the values through which we installed our bitnami/nginx

  <img width="1881" height="978" alt="image" src="https://github.com/user-attachments/assets/7fc65978-0d2d-4213-9606-9cdbe54cd3dd" />

## Task 5: Upgrade and Rollback
- As explained earlier we can run helm list and list down all the releases.
- then we can check history of specific releases by running helm history release-name
- to roll-back we ran
  
      helm rollback nginx 1
- and again we check history helm history nginx we can check histroy of what has happened all the details.
  
      REVISION        UPDATED                         STATUS          CHART           APP VERSION     DESCRIPTION
        1               Thu Jul 23 03:04:46 2026        superseded      nginx-25.0.14   1.31.3          Install complete
        2               Thu Jul 23 03:20:21 2026        superseded      nginx-25.0.14   1.31.3          Upgrade complete
        3               Thu Jul 23 03:46:25 2026        deployed        nginx-25.0.14   1.31.3          Rollback to 1

- once we rollback another revision gets added of that rollback and same can be seen in history as well.

<img width="1612" height="877" alt="image" src="https://github.com/user-attachments/assets/2ab583b1-d0ad-48df-8188-6350e5d66f4b" />



## Task 6: Create Your Own Chart
- As we the structuring which we require to create a helm chart we can run helm create chart-name which will create a folder that will have Charts yaml,values and templates.
- we can validate or check if our folder is proper and we can run helm lint . or helm lint name (outside the folder)
- then we listed all of our files in one go with helm template my-release my-app which acts as a cat commands lists down templates folder as one file
- then once we have the chart we can install it or upgrade it as we want
