# Docker Project: Dockerize a Full Application
## Task 1: Pick Your App
     * Frontend: React (Vite) — Used for building a responsive, reactive user interface. Served via Nginx for
       high-performance static delivery.
     * Backend: Node.js (Express) — A RESTful API built with JavaScript to handle business logic and database
       orchestration.
     * Database: PostgreSQL — A relational database for persistent task storage.
     * Initialization: SQL Seeding — Leveraged Docker’s entrypoint patterns to automate database schema creation and
       initial data population.

## Task 2: Write the Dockerfile
Created dockerfiles for backend and frontend with multi-stage build with non-root user with .dockerignore file.
### Backend
    FROM node:18-alpine AS builder
    WORKDIR /app
    COPY package*.json ./
    RUN npm install
    COPY . .
    
    FROM node:18-alpine
    RUN apk add --no-cache curl
    WORKDIR /app
    # Correct syntax: --chown comes before paths, and use trailing slash for folder content
    COPY --from=builder --chown=node:node /app/ ./
    
    USER node
    EXPOSE 5000
    CMD ["node", "index.js"]
    
    Here in backend we have in first stage took node-18 alpine as our base image created work directory called /app copied json package and install the dependencies from json and then copied other files through copy . .
    in deployer stage we have used same image thenwe have installed curl because that we have used in healthchek for backend then copied files from /app into current directory . with non-user node
    and run CMD to run index.js with help of node.
### Frontend
  FROM node:20-alpine AS builder
  WORKDIR /app
  COPY package*.json .
  RUN npm install
  COPY . .
  RUN npm run build
  
  FROM nginx:latest
  COPY --from=builder /app/dist /usr/share/nginx/html
  COPY ./nginx.conf /etc/nginx/conf.d/default.conf
  EXPOSE 80
  CMD ["nginx", "-g", "daemon off;"]

  In frontend we have base image of node in our builder stage where we have copied our packages,json which we installed then copied all the source and then run npm run build to build the installed packages.
  the in deployer we have used nginx base image  where first we have copied our files into nginx file sysetm.
  then copied the nginx.config into nginx file system and then put CMD.

  ### .dockerignore (backend)
    node_modules
    .env
    .git
    Dockerfile
    docker-compose.yml
### .dockerignore (frontend)
    node_modules
    dist
    .env
    .git
    Dockerfile
    docker-compose.yml

.dockerignore excludes unnecessary or sensitive files (like node_modules or .env) from the build context to make your images
smaller, faster, and more secure.

### nginx.conf
    server {
        listen 80;
    
        location / {
           root /usr/share/nginx/html;
           index index.html;
           try_files $uri $uri/ /index.html;
        }
    
        location /api/ {
            proxy_pass http://backend-nw:5000;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

## Task 3: Add Docker Compose
    services:
      db:
        image: postgres:alpine
        container_name: postgres_db
        restart: always
        environment:
          POSTGRES_USER: ${DB_USER}
          POSTGRES_PASSWORD: ${DB_PASSWORD}
          POSTGRES_DB: ${DB_NAME}
    
        healthcheck:
          test: ["CMD", "pg_isready", "-U", "${DB_USER}", "-d", "${DB_NAME}"]
          interval: 10s
          timeout: 5s
          retries: 5
        volumes:
          - ./db/schema.sql:/docker-entrypoint-initdb.d/schema.sql
        networks:
          - new
      
    
      backend:
        image: yjawlekar/day36_docker_project-backend:latest
        container_name: backend-nw
        restart: always
        environment:
          DB_HOST: db 
          DB_PORT: 5432
          DB_USER: ${DB_USER}
          DB_PASSWORD: ${DB_PASSWORD}
          DB_NAME: ${DB_NAME}
    
        healthcheck:
          test: ["CMD", "curl", "-f", "http://localhost:5000/health"]
          interval: 10s
          timeout: 5s
          retries: 5
    
        depends_on:
          db:
            condition: service_healthy
        ports:
          - "5000:5000"
        networks:
          - new
    
    
      frontend:
        image: yjawlekar/day36_docker_project-frontend:latest
        container_name: frontend
        ports:
          - "80:80"
        depends_on:
          backend:
            condition: service_healthy
        networks:
          - new
    
    networks:
      new:
        driver: bridge

  ## .env 
    DB_USER=me
    DB_PASSWORD=yog
    DB_NAME=newdb

  ## Docker-push
    Process to push local images into docker-hub
    First we will tag them
    - docker tag postgres:alpine yjawlekar/postgres:alpine
     Then we will push them 
    - docker push  yjawlekar/postgres:alpine
  
    Here once the images backend and frontend are available on dockerhub I deleted all the images available and changed the docker compose files backend and frontend from build from folder to image name directly.
    This will directly pull the images now and will build the containers and will run our application.
    

