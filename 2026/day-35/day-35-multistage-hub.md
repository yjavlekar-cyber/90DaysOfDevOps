# Multi-Stage Builds & Docker Hub
## Task 1: The Problem with Large Images
### 1.Write a simple Go, Java, or Node.js app (even a "Hello World" is fine)
    Created a simple node.js app which if we run prints hello world.
    We have index.js and package.json now in our folder.

### 2.Create a Dockerfile that builds and runs it in a single stage
    Created below docker file for above application.
    FROM node:latest
    WORKDIR /app
    
    COPY package.json ./
    RUN npm install
    copy . .
    CMD [ "node","index.js"]

### 3.Build the image and check its size
    By running docker build -t hello .
    build the image and if we do docker run hello:latest
    It prints : Hello, World! This is a simple Node.js application.
    
    But if we do docker images we get below details:
    IMAGE                       ID             DISK USAGE   CONTENT SIZE   EXTRA
    hello:latest                ff92f3901565       1.77GB          443MB    U
    
    For a simple application to print hello world this much size of image is too much and not required actually.

## Task 2: Multi-Stage Build
### 1.Rewrite the Dockerfile using multi-stage build:
#### Stage 1: Build the app (install dependencies, compile)
    FROM node:latest AS builder
    WORKDIR /app
    
    COPY package.json ./
    RUN npm install
    COPY . .
#### Stage 2: Copy only the built artifact into a minimal base image (alpine, distroless, or scratch)
    FROM gcr.io/distroless/nodejs22-debian13
    WORKDIR /app
    
    COPY --from=builder /app /app
    CMD ["index.js"]
### Build the image and check its size again
    EARLIER
    IMAGE                       ID             DISK USAGE   CONTENT SIZE   EXTRA
    hello:latest                ff92f3901565       1.77GB          443MB    U
    
    NOW
    IMAGE                                        ID             DISK USAGE   CONTENT SIZE   EXTRA
    gcr.io/distroless/nodejs22-debian13:latest   ed827daacb44        212MB         54.6MB    U

    The earlier size was around 1.gb whereas now when we have used distroless image the size has reduced to close to 200mb.
    Basically multi stage build has two steps first is builder stage and second is deployer stage.
    In builder stage we took our actual base image created workdir copied the json package installed it and copied other source code.
    In deployer stage we have used link of a distroless image and created a workdir called /app.
    then we have copie from builder the builders app folder into deployers app folder then ran CMD index.js.

    By this we not only reduce the size of our image but also make it secure like in normal images there are extra tools which are potential vulnerabilites.
    but in distroless we only have the copied files there is no shell, package managers which makes it secure cause no one can access it as it has no shell.

## Task 3: Push to Docker Hub
### 1.Log in from your terminal
    To login from cli into dockerhub
    docker login -u
    then it will ask for password, once password is entered we are logged in.

### 2.Tag your image properly: yourusername/image-name:tag
    Before pushing the image we first need to tag it:
    docker tag hello_world:latest yjawlekar/hello_world:latest
### 3.Push it to Docker Hub
    docker push yjawlekar/hello_world:latest

### 4.Pull it on a different machine (or after removing locally) to verify
    After removing the locally available images related to this project we have the same image on dockerhub
    we will pull it from there using below command:
    docker pull username/hello_world:latest

## Task 5: Image Best Practices
### 1.Use a minimal base image (alpine vs ubuntu — compare sizes)

  │ Image Tag      │ OS Base          │ Approx. Size │ Why use it?                                           │
  ├────────────────┼──────────────────┼──────────────┼───────────────────────────────────────────────────────┤
  │ node:22        │ Debian (Full)    │ ~1.1 GB      │ Testing, heavy builds, complex dependencies.          │
  │ node:22-slim   │ Debian (Minimal) │ ~200 MB      │ Best for production if you need Debian compatibility. │
  │ node:22-alpine │ Alpine Linux     │ ~130 MB      │ The Winner. Ultra-minimal, secure, and tiny.          |

### 2.Don't run as root — add a non-root USER in your Dockerfile
      To run as nonroot user in copy will chang ownership
      and after that we will mention the user as nonroot.
  
     COPY --from=builder --chown=nonroot:nonroot /app /app
    # Switch to the non-root user provided by Distroless
    USER nonroot
