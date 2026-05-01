# Day 11 Challenge

## Files & Directories Created
devopsfile.txt
notes.txt
fileownership/i/want/you/notess.txt


## Ownership Changes
devopsfile.txt
  Before- -rw-r--r-- 1 yogesh_jawlekar yogesh_jawlekar 0 May  1 15:13 devopsfile.txt
  After-  -rw-r--r-- 1 tokyo berlin 0 May  1 15:13 devopsfile.txt

notes.txt
  Before-rw-r--r-- 1 yogesh_jawlekar yogesh_jawlekar 0 May  1 15:15 notes.txt
  After- -rw-r--r-- 1 yogesh_jawlekar ezee   0 May  1 15:15 notes.txt

## Commands Used
sudo chown tokyo:berlin devopsfile.txt-to change owner and group
sudo chgrp ezee notes.txt - To change group
sudo touch notess.txt /home/yogesh_jawlekar/fileownership/i/want/you/ - to create directories and file recursively
sudo chown professor:planners /home/yogesh_jawlekar/fileownership/i/want/you/notes.txt-to change ownership recursively
