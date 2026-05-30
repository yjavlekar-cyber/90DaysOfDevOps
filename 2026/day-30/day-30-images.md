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

