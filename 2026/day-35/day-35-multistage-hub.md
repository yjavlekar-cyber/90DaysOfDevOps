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

    
