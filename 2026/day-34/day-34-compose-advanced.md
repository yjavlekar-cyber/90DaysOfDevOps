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

    1.Services:
      Services is the main header which comes first under which we will code our containers.
    
      1.1 database:
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
    -EXPLANATION_
    In 1.1 database we have first made our database container.
    with its official image available on docker hub.
    - image - official image
    - conatiner_name - name which we decide
    - restart - tells us incase of any error or the container stops or crashes how shall it restart always or manually.
    - environment - This basically has the database root password and the database name which will connect to our backend.
    - ports
    - healthcheck - this is basically because if any other container is dependent on database this container should be healthy then only the other container should start in that case we will put this condition here.
    - volumes - to keep our data safe even if the container is deleted we have attached volumes and there is another database which has some data for our current website.
    -  networks - To keep all the networks on same page we will assign this to all containers.

    
     1.2 redis:
         image: redis:alpine
         container_name: redis-cache
         networks:
           - my-app-net
    -EXPLANATION_
    As I know caches is basically a temporary storage where the website keeps certain data stored in order to not request the required data to the main database which might be slow in processing the data.
    We normally have created redis with its image available on docker hub.
    container name and network to be on the same page.
    

    
    1.3 backend:
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


    -EXPLANATION_
    1.3 backend in this case is such container which contains the actual code which has logic of our website.
    In this we have not taken image we have built it from the folder of backend where we already have our dockerfile.
    - build - to build an image with already existing docker file.
    - container_name - name of our container
    - environment
        This basically has actuall details which will help connect backend to our database
        DB_HOST- this name of our database under which we have written all our database code.
        DB_USER - which will be root
        DB_PASS - the password which we have give to our database
        DB_NAME - this name is the name which we have assigned in our host environment by the MYSQL_DATABASE which is shriwardhan_tourism
        REDIS_HOST - this connecte redis to backend
        secret_key - it hides your internal server secrets from being guessed or manipulated by the user's browser. It keeps the "handshake" between the browser and your server
                      honest!
    As backend can and shall only operate if the database is healthy and redis is started we will create
    depends_on - first we will assign the container on which frontend is dependent in this case it is our database.
                second we have healthcheck going on database if condition of that is healthy then only backend should start.
                also redis where condition is if redis service is started then only start the backend.
                

    
    1.4 frontend:
        build: ./frontend
        container_name: front
        ports:
          - "8081:80"
        depends_on:
          - backend
        networks:
          - my-app-net

             -EXPLANATION-
             Then comes front end where jsut like backend we have used build, container_name and ports.
             with that depends on if backend starts then only frontend should start.
             and network to keep all the container on same page.

        
    volumes:
      yogesh_db_data:
    
    networks:
      my-app-net:
                 After all the containers are done we will also mention the volumes and networks sepreatly with services in the compose file.

    Summary-
    In this project we have three tiers:
    Where database and redis is connected to backend and backend is connected to frontend.
    we keep our database data secure by attaching volumes for data persistency.
    We assign same networks to each container so that every container should be on same page.
    
