# Task 1: Your First Dockerfile
## 1.Create a folder called my-first-image
    mkdir my-first-image
## 2.Inside it, create a Dockerfile that:Uses ubuntu as the base image Installs curl and Sets a default command to print "Hello from my custom image!"
    FROM ubuntu:latest
    RUN apt-get update && apt-get install curl -y
    CMD ["echo","Hello from my custom image!"]

## 3.Build the image and tag it my-ubuntu:v1
    docker build -t my-ubuntu:v1 .
## 4.Run a container from your image
    docker run my-ubuntu:v1
## 5.Verify: The message prints on docker run
    Once we run the image using above command it prints our command.
    We made a dockerfile where we took base image as ubuntu.
    and to run our commands used RUN.
    and to print we used CMD.
# Task 2: Dockerfile Instructions
    FROM — base image
    RUN — execute commands during build
    COPY — copy files from host to image
    WORKDIR — set working directory
    EXPOSE — document the port
    CMD — default command
    
    Using above format a of dockerfile created one simple nginx dockerfile.
    FROM nginx:latest
    WORKDIR /app
    COPY index.html /usr/share/nginx/html
    EXPOSE 80
    
    In this we have simple html page which we will copy into the nginx containers html file.
    first we have taken base image as nginx
    then working directory
    then copied the file into containers path
    and exposed port 80.
    
    The problems i faced here were as follows:
    1)Common problem was that as nginx was alreadt installed it was using port 80 had unistall the services which were using those similar ports and then run the container.
    2)Earlier in this dockerfile i had used CMD to echo nginx installed but as nginx has its own commands which it runs when the image is build this was replacing it and
    thats the reason the container were exiting as soon as it was created.
    3)Even after i deleted the last command still the container were exiting the reason was when i deleted the CMD i forgot to rebuild the image so whenever i was running it was 
    running the version of dockerfile which had CMD in it.

# Task 3: CMD vs ENTRYPOINT
## 1.Create an image with CMD ["echo", "hello"] — run it, then run it with a custom command. What happens?
    So if we use CMD inside a dockerfile and normally run it will execute the command which is inside the dockerfile but,
    if we use any command with docker run it will override the dockerfile command and instead will execute the new command.4
## 2.Create an image with ENTRYPOINT ["echo"] — run it, then run it with additional arguments. What happens?
    In a dockerfile when we use ENTRYPOINT it basically appends the commands inside the dockerfile and outside dockerfile.
    For example in docker file we have ENTRYPOINT ["echo","hello"] when we build and run this it will print hello
    but if we run with any other text like docker run image new text.
    The ouput will be combined like: hello new text.
# Use of .dockerignore
    In an Nginx project, .dockerignore is mostly used to prevent sensitive files (like .env) or junk files (like .git or local documentation) from being copied into the public /usr/share/nginx/html folder where
    anyone on the internet could see them.
    In general .dockerignore file used is used to ignore certain files while building the image.

