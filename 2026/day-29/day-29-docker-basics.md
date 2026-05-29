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
## Task 2: Install Docker
### Install Docker on your machine (or use a cloud instance)
    sudo apt install docker.io
    [sudo] password for yogesh_jawlekar:
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    docker.io is already the newest version (29.1.3-0ubuntu3~24.04.2).
    0 upgraded, 0 newly installed, 0 to remove and 8 not upgraded.

    Using sudo apt install docker.io we can install docker in our system.
    as docker is already installed it notifies us that it is already there.
    
### Verify the installation
    This we can check with docker --version.
    
### Run the hello-world container
    To run the docker container of hello-world the official image is hello-world
    docker run hello-world
### Read the output carefully — it explains what just happened
    Once we run the hello-world container as above
    It first check wether the image is available locally.
    then it pulls the image from registry and informs us that pulling and downloading and downloaded.
    The result of which is following output:
    To generate this message, Docker took the following steps:
     1. The Docker client contacted the Docker daemon.
     2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
        (amd64)
     3. The Docker daemon created a new container from that image which runs the
        executable that produces the output you are currently reading.
     4. The Docker daemon streamed that output to the Docker client, which sent it
        to your terminal.

### Task 3: Run Real Containers
#### Run an Nginx container and access it in your browser

Run an Ubuntu container in interactive mode — explore it like a mini Linux machine
List all running containers
List all containers (including stopped ones)
Stop and remove a container
