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
  
### 2.Containers vs Virtual Machines — what's the real difference?
#### Containers
    There are reusable images which are made with the help of dockerfile containing all the requirments and dependencies which are pushed onto 
    registry then they are called docker images which are the blueprint of the application which now can be run on any system in the form of containers.

### Virtual machines
    Unlike containerization what virtual machines do is they put an hypervisor on top of our local systems which installs a new and seprate OS which then uses
    shared resources to run the application.

### 3.What is the Docker architecture? (daemon, client, images, containers, registry)
    In docker architecture there is docker client with the help of docker engine talks to docker deamon which is a background process and does
    the heavylifting of building,running and distibuting docker containers in the form of docker images which are stored on docker registry.
    - docker client- can be a shell like platform which talks to docker deamon
    - docker deamon- background process like kernel in linux which does the work
    - images - Blueprint of our application which has all the dependencies.
    - containers - which runs on any system with the help of docker images.
    - registry - storage space for docker images.
## Task 2: Install Docker
### 1.Install Docker on your machine (or use a cloud instance)
    sudo apt install docker.io
    [sudo] password for yogesh_jawlekar:
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    docker.io is already the newest version (29.1.3-0ubuntu3~24.04.2).
    0 upgraded, 0 newly installed, 0 to remove and 8 not upgraded.

    Using sudo apt install docker.io we can install docker in our system.
    as docker is already installed it notifies us that it is already there.
    
### 2.Verify the installation
    This we can check with docker --version.
    
### 3.Run the hello-world container
    To run the docker container of hello-world the official image is hello-world
    docker run hello-world
### 4.Read the output carefully — it explains what just happened
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
#### 1.Run an Nginx container and access it in your browser
    With the help of below command we first run our docker cpntainer with nginx:latest official image available on docker registry which docker hub.
    docker run -d -p 80:80 nginx:latest

    In this at first it created the containers but the up status was missing because the nginx was also running on local which was using 80 port already to use this as 
    container first stopped the nginx service and then ran the nginx container.
    To use it in local just visited the below link which showed nginx official homepage.

    http://localhost:80
    
### 2.Run an Ubuntu container in interactive mode — explore it like a mini Linux machine
    To run ubuntu container
    docker run -it ubuntu
    -it refers to interactive mode.
    so when we run this command once the container is made we are directly into that container as root so now on linux we are running an ubuntu container.

### 3.List all running containers
    - To list all the running container we can use
    docker ps
    
### 4.List all containers (including stopped ones)
    - To list all the containers running or exited
        docker ps -a
### 5.Stop and remove a container
    - First we will list the containers:
       docker ps -a
    CONTAINER ID   IMAGE                     COMMAND                  CREATED              STATUS                        PORTS                                 NAMES
    a9c9f334b451   ubuntu                    "/bin/bash"              About a minute ago   Exited (130) 19 seconds ago                                         stupefied_mclean
    27dc90abd377   nginx                     "/docker-entrypoint.…"   8 minutes ago        Up 8 minutes                  0.0.0.0:80->80/tcp, [::]:80->80/tcp   elated_kepler
    256411b30776   nginx                     "/docker-entrypoint.…"   14 minutes ago       Created                                                             xenodochial_jang
    fb20ac98a340   nginx                     "/docker-entrypoint.…"   16 minutes ago       Created                                                             loving_
    
    - Then with the help of container id first we will stop the container as per our requirment:
        docker stop 27dc90abd377
    
    - Then we will remove it by doing
        docker rm 27dc90abd377
## Task 4: Explore
### 1.Run a container in detached mode — what's different?
    To run container in detached mode means in background we use -d flag in docker run command as we did while running nginx container.

### 2.Give a container a custom name
    yogesh_jawlekar@Profound:~$ docker run --name yogesh -d -p 80:80 nginx:latest
    95c0c8972d1b90c35e3a0ac017aec9c6383ab42f6eb726d9122980a7fc4a25a5
    yogesh_jawlekar@Profound:~$ docker ps
    CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                                 NAMES
    95c0c8972d1b   nginx:latest           "/docker-entrypoint.…"   4 seconds ago   Up 3 seconds   0.0.0.0:80->80/tcp, [::]:80->80/tcp   yogesh
### 3.Map a port from the container to your host
    To map a port we can use -p as we have used in above example.
### 4.Check logs of a running container
    To check container specific logs we can run:
    docker logs containerid

### 5.Run a command inside a running container
    Once the containers are created if we want to use it we will first have to execute it as bash which can be done with the help
    of below command:
    docker exec -it containerid bash
    
## Task 4: Working with Running Containers
### 1.Run an Nginx container in detached mode
    doccker run -d -p 80:80 nginx:latest
### 2.View its logs
    docker logs 6fae129280e1(container ID)

### 3.View real-time logs (follow mode)
    docker logs 6fae129280e1 -f
    -f allows us to get live logs it basically follows the container and prints the live logs on terminal itself.
### 4.Exec into the container and look around the filesystem
    To enter into the container we can execute it by doing
    docker exec -it 6fae129280e1 bash
    The filesystem is similar to what we see in normal linux file structure there are several new folders in this dev  docker-entrypoint.d  docker-entrypoint.sh.
### 5.Run a single command inside the container without entering it
    To run commands without entering the container we can use:
    Did practice by creating new folder and listing it.
    docker exec container-ID mkdir new
    docker exec container-ID ls

### 6.Inspect the container — find its IP address, port mappings, and mounts
    So when we do 
    docker inspect container-ID
    The whole json config file of that container which has all the information of the container.
    We can check the ports,IP,state and network settings etc we can use docker inspect.

## Task 5: Cleanup

## 1.Stop all running containers in one command
    docker stop $(docker ps -q) && docker rm $(docker ps -aq)
    In the above command first by using docker ps -q we will find out all the running containers and stop them using docker stop.
    Then we will list containers which are running and stopped both with the help of docker ps -aq and remove them.

## 2.Remove all stopped containers in one command
    docker container prune
    Will delete all the stopped containers.
    
## 3.Remove unused images
    There are several ways to delete unused images.
    To remove dangling images which are created when we update an image and the older version takes place by using
    docker image prune
    
    To only remove docker unused images only
    docker image prune -a
    
    To remove all the images
    docker rmi $(docker images -q)

## 4.Check how much disk space Docker is using
    docker system df
    Will give us below details:
    TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
    Images          34        12        9.606GB   3.738GB (38%)
    Containers      21        4         28.74MB   24.62MB (85%)
    Local Volumes   5         3         3.271GB   204.9MB (6%)
    Build Cache     0         0         0B        0B
