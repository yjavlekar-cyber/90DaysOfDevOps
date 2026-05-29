# Introduction to Docker
## Task 1: What is Docker?
### 1.What is a container and why do we need them?
    Containers are isolated envoirnments containing all the dependencies pre installed which then can be run on any system.
    Basically when a devloper writes a code the code might work on his/her local system but it might not work on other
    systems due to dependency issues or other reasons.
    In this case contenrizing the code goes long way because unlike virtulization it does not require hypervisor to install new os to run the code
    what it does is on top of our system it puts docker engine which request our local system for requirments to run the container.
    The process of containrization is as give below:
    dockerfile------>docker image-------->container
    we first create a dockerfile which we push to docker registry as docker image which is reusable and which can be use to run in the form of containers.
  
### Containers vs Virtual Machines — what's the real difference?
#### Containers
    There are reusable images which are made with the help of dockerfile containing all the requirments and dependencies which are pushed onto 
    registry then they are called docker images which are the blueprint of the application which now can be run on any system in the form of containers.

### Virtual machines
    Unlike containerization what virtual machines do is they put an hypervisor on top of our local systems which installs a new and seprate OS which then uses
    shared resources to run the application.

### What is the Docker architecture? (daemon, client, images, containers, registry)
    In docker architecture there is docker client with the help of docker engine talks to docker deamon which is a background process and does
    the heavylifting of building,running and distibuting docker containers in the form of docker images which are stored on docker registry.
    - docker client- can be a shell like platform which talks to docker deamon
    - docker deamon- background process like kernel in linux which does the work
    - images - Blueprint of our application which has all the dependencies.
    - containers - which runs on any system with the help of docker images.
    - registry - storage space for docker images.
