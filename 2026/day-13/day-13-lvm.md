# Volume Managment

## commands used.
    1.sudo su- To switch from ubuntu into root user.
    
    2.lsblk - to list the blocks attached.
    
    3.pvcreate /dev/nvme1n1 /dev/nvme2n1-To create physical volume.
    
      Physical volume "/dev/nvme1n1" successfully created.
      Physical volume "/dev/nvme2n1" successfully created.
      
    4.vgcreate devopsvg /dev/nvme1n1 /dev/nvme2n1-To merge the physical volumes and create a volume group.
      Volume group "devopsvg" successfully created
      
    5.lvcreate -L 5g -n new-volume devopsvg-To create logical volume from the already created volume group.
      Logical volume "new-volume" created.
      
    6./home/ubuntu# pvs-To list doen all the physical volumes.
      PV           VG       Fmt  Attr PSize   PFree
      /dev/nvme1n1 devopsvg lvm2 a--  <10.00g <10.00g
      /dev/nvme2n1 devopsvg lvm2 a--  <12.00g <12.00g
      
    7./home/ubuntu# vgs-To list all the volume groups.
      VG       #PV #LV #SN Attr   VSize  VFree
      devopsvg   2   0   0 wz--n- 21.99g 21.99g
      
    8./home/ubuntu# lvs - to list down all the logical volumes.
      LV         VG       Attr       LSize Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
      new-volume devopsvg -wi-a----- 5.00g
      
    9.mkfs.ext4 /dev/devopsvg/new-volume-to format the logical volume path.
    
    10.mkdir -p /mnt/newblock-To create new directory in mnt location.
    
    11.mount /dev/devopsvg/new-volume /mnt/newblock- to mount the volume source volume into the mnt location.
    
    12. lvextend -L +5g /dev/devopsvg/new-volume-To extend the logical volume.
    
    13.resize2fs /dev/devopsvg/new-volume- to refresh the extended volume.
    
    14.df -h -to check the volumes are attached and can be seen or not.
## What I learned-
    In this particular assignment i got to do hands on practice of creating volumes on AWS console learnmed how to create them and attach them to the instance.
    After attaching this volumes the major part is to mount those to our storage.
    Today after attaching the volumes the first which i conducted was first converted those created volumes into physical volumes from out of those I created volume groups and then from them logical volume.
    Also did the process mounting this logical volumes to our mount location.
    Tried my hands on extending the already created logical volume as well. generate an image on basis of this to post on linked in



