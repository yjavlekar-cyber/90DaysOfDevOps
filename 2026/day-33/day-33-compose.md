# Docker Compose: Multi-Container Basics
## Task 1: Install & Verify
    To check
    docker-compose --version

    output:
     docker-compose --version
      docker-compose version 1.29.2, build unknown

## Task 2: Your First Compose File
Create a folder compose-basics
Write a docker-compose.yml that runs a single Nginx container with port mapping
Start it with docker compose up
Access it in your browser
Stop it with docker compose down

    Followed below steps:
    1.vim docker-compose.yml
    2.wrote below compose script-
    services:
      nginx:
        image: nginx:latest
        container_name: new
    
        ports:
          - "80:80"

    3.Did run command docker compose up
    - output
     ✔ Container new  Created                                                                                                                                                              0.2s
        Attaching to new
        new  | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
        new  | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
    4.Also stopped it using
    docker compose down
    - output:
    [+] Running 2/2
     ✔ Container new                   Removed                                                                                                                                            10.5s
     ✔ Network compose-basics_default  Removed              
## Task 3: Two-Container Setup
Write a docker-compose.yml that runs:

A WordPress container
A MySQL container
They should:

Be on the same network (Compose does this automatically)
MySQL should have a named volume for data persistence
WordPress should connect to MySQL using the service name

    Wrote below yml:
    services:
      my-sql:
        image: mysql:latest
        container_name: db_container
    
        environment:
          MYSQL_ROOT_PASSWORD: yog
          MYSQL_DATABASE: wordpress
        ports:
          - "3306:3306"
    
        volumes:
          - yogesh:/var/lib/mysql
    
      wpress:
        image: wordpress:latest
        container_name: Wpress
        ports:
          - "8081:80"
    
        environment:
           WORDPRESS_DB_HOST: my-sql
           WORDPRESS_DB_PASSWORD: yog
           WORDPRESS_DB_USER: root
           WORDPRESS_DB_NAME: wordpress
    volumes:
      yogesh:

    So in this under services first we have created mysql container with its image and container name and we have assigned it the required ports
    Then in env we have give root its password and then the name of database of wordpress which will connect to mysql and volume.
    
    Then for wordpress containers same thins image,name and ports.
    In env we have used host as mysql, then the host password which is password for mysql db.
    then under same env we have created a user called root and the wordpress db called wordpress which will connect to mysql under env.
    
    Once we run docker compose up 
    we can visit on port localhost:8081 we can see wordpress setup.
    
    Major challenges i faced here were creating a connection between this two containers i was facing an error on wordpress website called error establishing connection.
    first the password which i gave was not in correct format docker was reading it as path yogesh@123 which i changed to simple yog
    then i gave wpdb name to mysql then it got connected.
    

## Task 4: Compose Commands

### 1.Start services in detached mode
    docker compose up -d
### 2.View running services
    docker compose ps
    docker compose ls (to list down projects)
    
### 3.View logs of all services
    docker compose logs
    docker compose logs -f (for live logs)

### 4.View logs of a specific service
    docker compose logs nameofservice
### 5.Stop services without removing
    docker compose stop
### 6.Remove everything (containers, networks)
    docker compose down
### 7.Rebuild images if you make a change
    docker compose up -d --build
