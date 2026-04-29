*Commands used:* 
1)chmod 400 "key.pem" 
2)ssh -i "key.pem" ubuntu@dns 
3)sudo apt update
4)sudo apt install nginx/docker.io 
5)journalctl -u nginx>nginx_logs.txt 

*challenges faced* 
I forgot to change and modify the file permissions before doing ssh because of the i faced an error after i realized did change my permissions of the file with chmod 400 before doing ssh. 


*What I Learned* 
First thing i learned that how to create and ec2 instance and how to connect it through ssh. then learned how to update and install services. how to check their status and also did learn how to directly extract the logs into the new log file.
