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
