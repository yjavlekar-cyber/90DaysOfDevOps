# Day 10 Challenge

## Files Created
1)devops.txt
2)notes.txt
3)script.sh

## Permission Changes
[before/after for each file]
1) script.sh changes to 764
  Before--rw-r--r-- 1 yogesh_jawlekar yogesh_jawlekar 35 Apr 30 16:21 script.sh
  After--rwxrw-r-- 1 yogesh_jawlekar yogesh_jawlekar 35 Apr 30 16:21 script.sh

2)devops.txt changed to 444
  Before--rw-r--r-- 1 yogesh_jawlekar yogesh_jawlekar  0 Apr 30 16:19 devops.txt
  After--r--r--r-- 1 yogesh_jawlekar yogesh_jawlekar  0 Apr 30 16:19 devops.txt

3)notes.txt changed to 640
  Before--rw-r--r-- 1 yogesh_jawlekar yogesh_jawlekar 33 Apr 30 16:20 notes.txt
  After--rw-r----- 1 yogesh_jawlekar yogesh_jawlekar 33 Apr 30 16:20 notes.txt

## Commands Used
1)touch-to create new file.
2)cat>filename-also to create new file but at the same time write in it.
3)cat>>filename-Same as cat>filename but using this can help us to append new data aswell.
4)vim script.sh-created shell script using vim editor.
5)cat-This can be used to read files.
6)cat /etc/passwd | tail -5 or head -5- cat with pipe can helps to read the file and extract the data as per our needs just like in the example head -5 will only show 5 lines and tail -5 will show last 5 lines.
7)./ - to run shell script
8)chomd +x filename-To make file executable.
9)chmod 777 filename - to change file or dirc permissions the number can be changed as per the truth table.


## What I Learned
As we all know everything in linux is either a file or a directory I can imagine why permission plays a vital role in linux.
It is very important to check the permissions of certain files or directories inorder to carry out operations related to them.
what I learned through this assignments i can explain using below task which i carried out:
  --File creation.
  --what are Read,write and execution permissions.
  --Checking file permissions.
  --Changing file permissions.
  --Difference between overwriting and appending a file.
  --Running shell script.
  
