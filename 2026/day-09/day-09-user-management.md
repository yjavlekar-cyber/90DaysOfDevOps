# Day 09 Challenge _User-managment

## Users & Groups Created
    - Users: tokyo, berlin, professor, nairobi
    - Groups: developers, admins, project-team

## Group Assignments
    List who is in which groups
    tokyo-developers,tokyo,
    berlin-berlin,developers,admin2
    professor-admin2,professor
    nairobi-nairobi,project-team

## Directories Created
    [List directories with permissions]
    1)/opt/dev-project-775
    2)/opt/team-workspace

## Commands Used
    1) sudo useradd -m username-to add the user with home directory.   
    2)sudo passwd user- To set user password.
    3)sudo groupadd groupdname - to add new groups
    4)sudo gpasswd -a user group- to add the user into a group
    5)sudo mkdir -p path - to create a directory inside a directory e.g /opt/dev-project
    6)sudo chmod 755 file or direcotry name - to change permissions of file or directory.
    7)sudo su user- To switch between users
    8)touch file - to create file inside directory.
    9) sudo chrgp newgroup file/directory- To set or change group of partiular file and directory.
    10) sudo chown owner:group file - to change ownershp or group or both of a file/directory.
      

##### What I Learned######
* Today i learned how the user managment happens inside the linux system.
* I learned how to create groups and change ownerships.
* Majorly I learned that how without changing ownership we can give access to other users of specific directories/files by adding them in certain groups.
* Learned the differnce between changing ownership and changing groups of particular file/directories or users.


