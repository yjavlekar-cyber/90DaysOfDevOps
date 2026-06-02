# Task 1: The Problem
    Run a Postgres or MySQL container
    Create some data inside it (a table, a few rows — anything)
    Stop and remove the container
    Run a new one — is your data still there?

    Write what happened and why.
    
    So here we run mysql by using official image available on dockerhub by using below command.
    docker run -d --name yogesh -e MYSQL_ROOT_PASSWORD=passwd mysql:latest
    then executed the same using
    - docker exec -it containerID bash
    This will open shell to interact with mysql now we have to login using our password which we mentioned while running
    mysql -u root -p
    This will ask for password once we enter we are into mysql
    Now we have to create databases and data inside those databases refer following sequence:
     - SHOW DATABASE; - To view any exisiting db
     - CREATE DATABASE name; - To create db 
     -  USE NEW - To use this database to insert date or to operate.
     - CREATE TABLE learners (learner_ID INT,learnername VARCHAR (50)); - To create table inside the dataa
     - INSERT INTO learners (learner_ID,learnername) values(1,"Yogesh"); - To insert
     - SHOW TABLES; - To view tables inside our db
     - SELECT * FROM learners; - to view data inside the the table.
    Now after doing this whole process if we exit from the container and do stop and remove the data and tables which we 
    created got deleted.

  # Task 2: Named Volume
    Create a named volume
    Run the same database container, but this time attach the volume to it
    Add some data, stop and remove the container
    Run a brand new container with the same volume
    Is the data still there?

    Now we already have image in our local.
    And as pe our task 1 when we deleted the container with data and once again we created the data was not their.
    Solution to this is to create a volume inside docker and attache the volume when we run the container.
    To create volumes:
    - docker volume create name - this will create a new volume.
    - docker volume ls - This will list down all the volumes.
    Now that we have volumes will run or docker container with volumes which we created but first we will check the path of our volume inside
    docker by using:
    docker inspect volume volumename

    Then,
    docker run -d -v dockervolumepath:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=passwd mysql:latest

    we attached our created volume to mysql path.
    and now if we inserted any data inside this container and if we delete the container and again
    if we create a new container with this volumes again with earlier command we can see our earlier data 
    inside our new container.

  # ask 3: Bind Mounts
    Create a folder on your host machine with an index.html file
    Run an Nginx container and bind mount your folder to the Nginx web directory
    Access the page in your browser
    Edit the index.html on your host — refresh the browser
    Write in your notes: What is the difference between a named volume and a bind mount?

    Here i create a simple html file in a folder and while running the container i did mount it with the nginx container.
    docker run -d -p 80:80 --volume /home/yogesh_jawlekar/script/day32/new:/usr/share/nginx/html nginx:latest
    In above command we have used --volume to mount path of our index.html to mount it with nginx directory on /usr/share/nginx/html.
    So now as we have directly mount our html file in our folder directly to our nginx container,
    and if we visit our localhost on port 80 we will be to see the page.
    also if we change the data in our file it will directly change the webpage as well.

    
    
