*File System commands:
1.cd-to switch directories we can use this command called 'change directories'.
2.ls-to list the files or folders in directory we can use this command.
3.mkdir-this command can be used to create new directories.
4.touch-touch can be used to create files.
5.cp,mv,rm-this commands can be used to copy(cp),move(mv) or rm(remove) files or directories in linux.

*Process related commands:
1.ps-this commands basically will give us snapshot of the running processes.
2.top-top will give us active running processes.
3.htop-htop is a more visually appealing or easily understandable option where we can scroll down horizontally to the processes.
4.journal ctl-we can use journal ctl to view logs
5.systemctl-through this we can start,stop and check status of any unit e.g nginx or docker.
6.kill-this can be used to kill any running process with the help of pid number which can be identified with the help of top or htop.

*Networking related:
1.ping-ping is used to check wether the destination is reacheable or not.
2.ip addr-can be used to check current network configuration.
3.curl-it is used to send requests to servers and get responses, mainly for testing APIs and web services.
4.traceroute-It shows the route through which packets have travelled.



*user managment commands;
1.useradd-to add new user.
2.userdel-to delete existing user.
3.passwd-to set password to a user.
4.useradd -m-to add user with directory.
5.gpasswd -a,-d - to add and delete users into the group.

*Package installer:
1.sudo apt update-updated the whole system and download the packages.
2.apt install-to install the downloded packages.
3.apt upgrade-to update packeges to latest version.

*File managment:
1.chmod-this can be used to change read,write and execution permissions of directory or a file.
2.chown-this can be used to change the ownership of the file or folder.

*Volume managment:
1.free-free displays the total amount of free and used physical and swap memory in the system.
2.df-to check disk usage.
3.du-to check space occupied by files.
4.lsblk- lists information about all available or the specified block devices.
5.pvcreate paths of created volume-we can create the physical volumes.
6.vgcreate groupname pvpaths(paths of only those pv of which can be converted to lv)-earlier physical volumes can be converted tp volume group
7.lvcreate -L(how much gb or volume) 10G -n name of lv nameofvg - from vg we can create lv.
(note:created lv can be mounted by creating a dir in mnt then by doing mkfs.ext4 format the lv path folder/vg/lv and then mount source location to mount location)
8.lvextend-can be used to extend the existing size of logical volume.

