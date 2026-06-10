# Docker Revision & Cheat Sheet
## Self-Assessment Checklist
- [X] Run a container from Docker Hub (interactive + detached)
- [X] List, stop, remove containers and images
- [X] Explain image layers and how caching works
- [X] Write a Dockerfile from scratch with FROM, RUN, COPY, WORKDIR, CMD
- [X] Explain CMD vs ENTRYPOINT
- [X] Build and tag a custom image
- [X] Create and use named volumes
- [X] Use bind mounts
- [X] Create custom networks and connect containers
- [X] Write a docker-compose.yml for a multi-container app
- [X] Use environment variables and .env files in Compose
- [X] Write a multi-stage Dockerfile
- [X] Push an image to Docker Hub
- [X] Use healthchecks and depends_on

## Quick-Fire Questions
### 1.What is the difference between an image and a container?
    An image is a blueprint where we store all the neccesities reuired to run an app like base image,src code etc.
    A container is an isolated environment created using the image to run that particular application.

### 2.What happens to data inside a container when you remove it?
    If we remove container and if it has data inside it the data will also get deleted with that container.
    This we can prevent bu using volumes with the containers.
    There are two types of volumes we can use listed below:
    1) named volumes:
       This are the volumes which we create using docker volume create name.
    2) bind volumes:
       This volumes are already exsting folders available in our system which we use as volumes for container.
    With the help of volumes we can persist our data even if the data is deleted if we have used the volume while running the container we can also use the same volume to run if
    we delete the container this will keep the data as it is.
    
### 3.How do two containers on the same custom network communicate?
    If we are using user-defined networks or custom networks for this containers docker runs dns server every container is registered with DNS on custome network.
    hence we containers can communicate with other networks using DNS or names of the containers which is automatically provided by docker.
    
    but in default bridge there is no dns available hence containers can only communicate with each other using IP addresses.

### 4.What does docker compose down -v do differently from docker compose down
    docker compose down will only remove containers and networks attached to it.
    but docker compose down -v will remove container there networks with volumes which will result in loss of data.

### 5.Why are multi-stage builds useful?
    Multi-stage builds are useful because of following reasons:
    - Reduce image size.
    - for security reasons.
    - we can run as non-root user
    - we can use multisage where in builder stage we can only build our dependencies like packages needed and
      in deployer stage we can run them in CMD.

### 6.What is the difference between COPY and ADD?
    - COPY can be used to copy from local into a container.
    - ADD can do what COPY can do but also it can extraxt tar files and download through urls.

### 7.What does -p 8080:80 mean?
    This refers to mapping host port 8080 to container port 80.
### 8.How do you check how much disk space Docker is using?
    By running
    docker system df

## Docker Command Cheat Sheet
### Container commands — run, ps, stop, rm, exec, logs
- docker run -d -p 8080:80 nginx:latest
- docker ps
- docker ps -a
- docker stop containerID
- docker rm containerID
- docker exec -it containerID bash
- docker logs containerID

### image commands — build, pull, push, tag, ls, rm
- docker build -t name .
- docker pull username/imagename
- docker push username/imagename
- docker tag image username/imagename
- docker images(to list all the images)
- docker rmi imageID

### Network commands — create, ls, inspect, connect
- docker network create networkname
- docker network ls
- docker inspect network networkname
- docker netork connect containerID
- docker network prune (to remove all unused networks)
- docker network rm (to remove one or more networks)

### Compose commands — up, down, ps, logs, build
- docker compose up
- docker compose down
- docker compose ps
- docker compose logs
- docker compose up --build
- docker compose up -d

### Cleanup commands — prune, system df
- docker system df
-  docker system prune
       * All stopped containers.
       * All networks not used by at least one container.
       * All dangling images (images with no name/tag, usually leftovers from failed builds).
       * All dangling build cache.
       except volumes.
  
