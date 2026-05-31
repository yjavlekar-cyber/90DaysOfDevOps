# Docker Images & Container Lifecycle
## Task 1: Docker Images
### Pull the nginx, ubuntu, and alpine images from Docker Hub
    By using below command we can pull images:
    docker pull imagename

### List all images on your machine — note the sizes
    To list the images we can run
    docker images
    output-
    
    IMAGE                                      ID             DISK USAGE   CONTENT SIZE   EXTRA
    alpine:latest                              5b10f432ef3d       13.1MB         3.95MB
    ubuntu:latest                              f3d28607ddd7        160MB         45.3MB    U

### Compare ubuntu vs alpine — why is one much smaller?
    ubuntu is a debian based linux image which has wide range of packages and dependencies pre installed which makes it large in size.
    where as alpine images are linux based images which only has minimum required packages and dependencies which are required to run application.
    As their are less packages and dependencies the image size is less if compared to ubuntu which is standard image.

### Inspect an image — what information can you see?
    When we docker images we get list of all the images which are their in our system or which we have pulled.
    First we see the name of image then its ID then how much disk space that image is utilizing and its actual size besides that.
    Lastly there is an extra coloumn which indicates if the image is in use or not by showing u there.
### Remove an image you no longer need
    To remove an image we can run below command:
    docker rmi image-id

## Task 2: Image Layers
### Run docker image history nginx — what do you see?
    When we do docker image history nginx it gives us a table which shows layes of that particular image.
    It basically shows us image id when it was created, how it was created,its size and comment.
    
    Output-
       IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
    5aca99593157   7 days ago    CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
    <missing>      7 days ago    STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
    <missing>      7 days ago    EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
    <missing>      7 days ago    ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
    <missing>      7 days ago    COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
    <missing>      7 days ago    COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
    <missing>      7 days ago    COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
    <missing>      7 days ago    COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
    <missing>      7 days ago    COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
    <missing>      7 days ago    RUN /bin/sh -c set -x     && groupadd --syst…   87.1MB    buildkit.dockerfile.v0
    <missing>      7 days ago    ENV DYNPKG_RELEASE=1~trixie                     0B        buildkit.dockerfile.v0
    <missing>      7 days ago    ENV PKG_RELEASE=1~trixie                        0B        buildkit.dockerfile.v0
    <missing>      7 days ago    ENV ACME_VERSION=0.4.1                          0B        buildkit.dockerfile.v0
    <missing>      7 days ago    ENV NJS_RELEASE=1~trixie                        0B        buildkit.dockerfile.v0
    <missing>      7 days ago    ENV NJS_VERSION=0.9.9                           0B        buildkit.dockerfile.v0
    <missing>      7 days ago    ENV NGINX_VERSION=1.31.1                        0B        buildkit.dockerfile.v0
    <missing>      7 days ago    LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
    <missing>      12 days ago   # debian.sh --arch 'amd64' out/ 'trixie' '@1…   87.4MB    debuerreotype 0.17
    
### Each line is a layer. Note how some layers show sizes and some show 0B && Write in your notes: What are layers and why does Docker use them?
    The above table shows layers which are executed when image is in making.
    As we know docker image is build with the help of docker file and docker file has certain steps which gets executed step by step 
    those steps can be counted as layers those layers are listed here.
    This layers are listed in opposite order than this steps which are in docker file.

    0B shows that by that layer metadata was changed but no new files were added thats the reason the size is 0B.
## Task 3: Container Lifecycle
### Create a container (without starting it)
    To create a container without running it we can use:
    docker create nginx:latest
### Start the container
    To create and start at the sametime we can use:
    docker run -d -p 80:80 nginx:latest
### Pause it and check status
    To pause we can use:
    docker pause container-ID
    After this if we check the docker ps
    it will show that container but in status it will show as paused.

### Unpause it
    docker unpause container-ID
    It will as usual in docker ps -a.
    
### Stop it
    docker stop container-ID

### Restart it
    docker restart container-ID
### Kill it
    docker kill container-ID
### Remove it
    docker stop container-ID && docker rm container-ID


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
