# Day 34 – Docker Compose: Real-World Multi-Container Apps
## A Three tier tourism website including frontend, backend and database.

### what do we have as code:
#### 1.Backend (Flask)
    Processes application logic, handles page routing, and manages data flow for the contact form.
    Connects the user interface to the database and cache, ensuring content is delivered dynamically.

#### 2.Frontend (Nginx & CSS)
    Acts as a high-speed reverse proxy that secures the backend and serves static files like images.
    Uses a custom "Coastal Blue & Sand" CSS theme to provide a modern, responsive user experience.

#### 3.Database (MySQL)
    Provides persistent storage for tourist attraction details and saves all visitor-submitted messages.
    Automatically builds its own tables and seeds them with data the moment the container starts.

#### 4.Cache (Redis)
    Stores frequently requested information in-memory to eliminate the need for repeated database queries.
    Ensures the "Places" page loads instantly for visitors by serving cached data in milliseconds.


### What was the process:
    1.We made three folders frontend,backend and database
    2.Next step we made dockerfiles for frontend and backend inside them.
    3.along with this three folders we created docker-compose.yaml file.
    4.Then with the help of docker compose up run the compose file
    5.And now if we visit http://localhost:8081/ we will be able to view our website.

### Explaining Dockerfile:
#### Frontend
    FROM nginx:latest
    COPY ./static /usr/share/nginx/html/static
    COPY ./nginx.conf /etc/nginx/conf.d/default.conf
    EXPOSE 80
    
     -EXPLANATION-
    In frontend we have used nginx as reverse proxy which will show our website to the enduser.
    We have taken base image nginx:latest.
    Then we have copied our static website code into the nginx folder as html file.

    Then just for sake of it we have exposed port 80 to it.
#### nginx.conf

    server {
        listen 80;
    
        location /static/ {
            alias /usr/share/nginx/html/static/;
        }
    
        location / {
            proxy_pass http://backend:5000;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
    -EXPLANATION-
    This is a nginx configuration file.
    first we have created a server in that we have given nginx should listen on port 80.
    location is basically when end user load our website it gets routed to static location in nginx thats why we have assigned
    an alias location where our actual files are.
    After that we have another location in that only proxy pass we can change as per what is the name of backend container and its port.
    Rest headers can be contant.

    This config file is used in full stack applications where we need to tell nginx that the backend container exists.
  
#### Backend
    FROM python:3
    WORKDIR /app
    COPY requirements.txt .
    RUN pip install -r  requirements.txt
    COPY . .
    CMD [ "python","app.py" ]
    
     -EXPLANATION- 
    In the dockerfile of backend we have used
    python:3 as base image.
    the created a workdir named app.
    then copied our requirments.txt files in the current folder which is denoted by .(dot)
    then first installed all the requirments.
    Once the requirments are installed we will copy other files from . to .
    Then we have to install the .py file which we ran using python keyword.


#### Docker-compose.yml

    # services:
      Services is the main header which comes first under which we will code our containers.
    
      database:
        image: mysql:latest
        container_name: db
        restart: always
        environment:
          MYSQL_ROOT_PASSWORD: yog
          MYSQL_DATABASE: shriwardhan_tourism
        ports:
          - "3306:3306"
        healthcheck:
          test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-u", "root", "-pyog"]
          interval: 10s
          timeout: 5s
          retries: 3
          start_period: 30s
        volumes:
          - ./database/init_db.sql:/docker-entrypoint-initdb.d/init_db.sql
          - yogesh_db_data:/var/lib/mysql
        networks:
          - my-app-net
    
      redis:
        image: redis:alpine
        container_name: redis-cache
        networks:
          - my-app-net
    
      backend:
        build: ./backend
        container_name: back
        environment:
          DB_HOST: database
          DB_USER: root
          DB_PASS: yog
          DB_NAME: shriwardhan_tourism
          REDIS_HOST: redis
          SECRET_KEY: shriwardhan_secret_123
        depends_on:
          database:
            condition: service_healthy
          redis:
            condition: service_started
        networks:
          - my-app-net
    
      frontend:
        build: ./frontend
        container_name: front
        ports:
          - "8081:80"
        depends_on:
          - backend
        networks:
          - my-app-net
    
    volumes:
      yogesh_db_data:
    
    networks:
      my-app-net:
                               
