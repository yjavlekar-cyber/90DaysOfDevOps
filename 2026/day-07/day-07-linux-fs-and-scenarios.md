*Linux File System Hierarchy*
/ (root) -As root is the starting point in linux and under root there are various directories,files and folders root will be starting point for me will check by doing ls what are the directories are listed and according as per requirments we can cd into them.
/home- home directory is bascially user directory as a user my data will be stored there for major part of the operations i will work on this directory only.
/root-/ is the starting point of linux and /root is its own directory and as of now there are no files but if when you login into root .history file is created which saves commands ran while you were root and if we did ssh the keys and authorized keys folder might be thier in the root folder.
/etc-etc is such a directory which holds core config files of the whole system like networking,users,services and package sources i will use this if i want to acces system config files.
/var/log--var stands for variable, it stores the data which is variable or which changes while the system is running for example /var/log saves the logs suppose nginx is running its logs will get stored their.a system’s working memory + storage room, I will use this when i want to access the logs or any other variables.
/tmp -- tmp folder is basically temporary folder which stores such temporary data which gets deleted once rebooted some of the examples are-a text editor saving a temporary copy while you edit a program processing data before saving final output, When you install software files may be unpacked in /tmp before being installed.
/bin-contains user commands like ls cd cp mkdir.
/sbin- contains commands which are used for system administration.
/opt-this optional directory is used to stored third party softwares or softwares installed which are from outside the core system of linux which are installed manually not with system package installers like apt.


Hands-on task:

*Scenario 1: Service Not Starting*
A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?

Step 1: systemctl status myapp
Why: Will first check the status of the service is it active or stopped.

Step 2: journalctl -u myapp -n 50
Why: With the help of journalctl i will check the lastest 50 logs of the service myapp to dignose.

step 3:systemctl is-enabled myapp
Why: By using this command i will check whether this service is enabled to start automatically after reboot.


*Scenario 2: High CPU Usage*
Your manager reports that the application server is slow.
You SSH into the server. What commands would you run to identify
which process is using high CPU?

Step 1: top/htop
Why: Through top i will first see the live running processes or htop for better visualistic approach.

Step 2: ps aux --sort=-%cpu | head -10
Why: through ps aux will list snapshot of running process then it will sort the %cpu with the help of - and by sending its output through pipe into head -10n to get output of 10 highest cpu consumin proceses which are using cpu.

Step 3-Pid no-6 
why- This PID no is using highest percent of cpu amongst all the other services.

*Scenario 3: Finding Service Logs*
A developer asks: "Where are the logs for the 'docker' service?"
The service is managed by systemd.
What commands would you use?

Step 1:systemctl status docker
Why : to check status of the service.

Step 2: journalctl -u docker -n 5
Why: to check the logs of docker service and only latest 5 logs.

Step 3:journalctl -u docker -f
Why: to check realtime logs getting updated.


*Scenario 4: File Permissions Issue*
A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"
What commands would you use to fix this?
Hint:

Step 1: ls -l /home/user/backup.sh
Why: To check permissions given the reason behind permission denied is file must not have executaion permisions.

Step 2:chmod +x backup.sh
Why: To give execution permissions to the file backup.sh

Step 3:ls -l /home/user/backup.sh
Why : To check permission very successfully give or not.

Step 4: ./backup.sh
Why:after giving execute permission to run the shell script.
