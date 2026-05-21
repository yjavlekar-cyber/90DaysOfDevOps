# Day 12 revision
As of now I have learned the below topics in linux operating system and mentioned below with their respective commands and their major usage with example-

## 1)Navigation:
    Navigation is basically from what i have learned basically is how you travel in linux how you switch from one dirctory to another directory,
    and some of the major commands which i haved use that i can recall for navigation purpose in linux are as follow:
    
      1)cd(change directory)-with help of this i can switch into the directory by that i 
      mean suppose i do cd user i can enter in the directory "user",but if 
      i want to get out of that directory i can just do cd .. 
      and i will get back to the previous directory.
      
      2)ls(list files)-As the linux system is such a system which is either a file or a directory
      so in order to view or list the files situated in a directory we simply enter and run
      ls whatever files are there in directory will be listed there are certain varitions
                      also i have learned which are as follows:
                        *ls -a - this will give us all the hidden files as well with the existing viewable file.
                        *ls -l - This will show the list of files with all the details like files their permissions their owmner groups etc.
                        
      3)pwd(present working directory)-this command helps us to identify the directory in which we are now working.
      
      4)uname -a- to check the the user details.
      
      5)whoami- This gives us the current user.

  ## 2)File Related:
    Through below commands we can created file,directories deleted 
    them,read them append into them overwrite them and they are as follows:
    
      1)touch-to create file we can use this eg. touch files.txt
      
      2)mkdir-we can create directory by using mkdir eg. mkdir new-directory.
      
      3)rm- to remove files we can use this command eg sudo rm files.txt
      
      4)mv- we can use mv in two methods to mv files eg. mv dir1 dir2 this will transfer 
      dir1 into the dir2 and also in another way which is we can use it to tranfer the data 
      from file1 into the file2 basicall file2 is the new file mv file1 file2 new file will be created 
      named file2 with the data of file1 and file1 will be deleted.
      
      5)rm -rf-to delete the files.
      
      6)cat-The major use of cat is basically to read the 
      file but the two underrated uses are to append and overwrite the 
      files if we do cat>file file will open and we can write in it if their 
      is already data in it this new data will overwrite it and if we do cat>>file 
      it will also allow us to write us the data but if the data already 
      exist then it will append this data into the file.
      
      7)cp- to copy
      
      8)vim-this is an editor.

  ## 3)User related:
  
    Though everything in linux starts with root which is represented by backslash / we can also create users which 
    can acceses the system with their own passwords we can also created certain groups to assign specific duties.
    
    1)useradd -m - to create new user with the home directory.
    
    2)userdel -r - to delete the user with its home directory.
    
    3)passwd - to set password for the user
    
    4)groupadd newgroupname-this will create new group.
    
    5)gpasswd -a user group-this can be used to assign the user to a certain 
    group also we can use this wih gpasswd -d,to delete the user from group.
    
    6)chgrp group filename- This can be used to change the group of a specific file or directory.


  ## 4.)Permissions & Ownership:
  
    Permissions basically refer the read,write and executable permissions of the files 
    and ownership refers to the ownership give to a user to access a file or directory
    
    1)chmod-this can be used to modify the file permissions.
    2)chown user:group file- this will give the ownership of the file to the mentioned user and mentioned group.

  ## 5)Package installer commands:
        In ubuntu package installer command is basicall only one which is apt whic can be used with following instructions:
        
        1)sudo apt update-This will download the packages and update the system.
        
        2)sudo apt install- to install a particular unit or service such as nginx.
        
        3)sudo apt upgrade-to upgrade the downloaded services in to their latest version we can use this.

  ## 6)process related-
    1)top/htop-running processes
    
    2)ps-snapshot of the running process.
    
    3)free -h -to check the free memory or ram used.
    
    4)df -h - to check disk space
    
    5)du -sh - to check disk usage what is the highest disk space utilized.
    

  ## File system-
      The file system of root has below mentioned directories:
      /root-default directory of the root.
      /etc-directory which has mostly config files. cat /etc/group
      /var-This is directory which stores data which changes whil system is running mostly this is used to read logs cat /var/groups.
      /home-this is home directory of the user.
      /tmp-directory for temporary files.
      /bin- This binary stored the commands except system binaries.
      /sbin- This directory stores system commands.
  

  ## Shell scripting-
    Shell scripting is basically automating certain task with the help of the script 
    supposed for a particular task we require 10 commands we will create a .sh file 
    and by using vim will write those 10 commands into that file and 
    we can runt the same by using ./file.sh this will
    execute the commands from top down.

  ## Logs
    cat /var/log-can be used to check the system logs.
    
    journalctl -u nginx - this can be used to check the logs arisisng from service nginx.

  ## How to shell into aws instances:
    From local we can connect to remote servers using the shell which is an interactive way of talking to the system kernel.
    Through the private keys we can ssh into the instance through the terminal.
    Also learned concept of Jump/bastian hosting which basically means we create two instances and connect them by creating the private keys we create key and copy the pub keys into the other instance.
  

  ## Networking commands:

    1)ping- to check the basic connectivity between our machine and the host we use ping.
    2)ss -tuln-will give us info of the ports listening or not.
    3)ip addr -will give us our ip related details.
    4) ssh -i - to Securely log into remote machines.
    5)traceroute- to trace the routes of packets transmission.



# Summary

I learned why linux is called the basic part of learning devops.
Around 90% of the services run on linux operating system.
Linux is available as GPL so anyone can modify it he/she just needs to share those change publicly.
Linux is very much secure as we can access the remote server locally with pair of keys which makes it secure.
I feel linux is not just a operating system it is an whole playground.
