#Task 1: Log Rotation Script
#!/bin/bash
set -euo pipefail

source=$1

display_usage() {

        echo "usage:./newlog.sh <source>"

}

if [ $# -eq 0 ];then
        display_usage
fi

echo "Initiating Compression and deletion"
echo ""
echo "*********************************************************************************************************************"
echo ""

comp_list=$(find "$source" -name "*.log" -type f -mtime +7 -print)
if [ -n "$comp_list" ];then
        echo "$comp_list" | xargs gzip
        comp_count=$(echo "$comp_list"| wc -l)
        echo "Compression Successful. Compressed:$comp_count"
else
        echo "No files more than 7 days"

fi


del_list=$(find "$source" -name "*.gz" -type f -mtime +30 -print)
if [ -n "$del_list" ];then
        echo "$del_list" | xargs rm -f
        del_count=$(echo "$del_list" | wc -l)

        echo "compression Successful. Deleted:$del_count"

else
        echo "No files more than 30 days"

fi
Output-
Initiating Compression and deletion

*********************************************************************************************************************

No files more than 7 days
No files more than 30 days

summary-
In this script we had task to first compress the files which we have using gzip which are older than 7days and delete the compressed files which are older than 30days.
so first we checked our arguments should be used proper for the we used display usage function where if all the arguments are 0 then it will print the actuall arguments one should use to run the script.
Then for the first process of compression we used find to search for our source (path) like which files should be compressed then with "-name" we searched for file type "*.log" then with "-type f" which represnts all regular files.
then we used -mtime +7 to search on the basis of the files which are older than 7 days followed by -print.
Then we put if condition under which we used -n which if the first variable is not empty will compress the files through pipe where we echoed the output from the first process into xargs gzip which compressed the files.
After that we need to count how many files were compressed we followed the same pipe like process but instead of gzip te transfered the output from the first variable of our compressed process into wc -l.
then we printe the the account and used else if the first varible is empty it will print no files.
same process I have followed to delete and list down the count deleted files but instead of gzip i have used xargs rm -f.


#Task 2: Server Backup Script

Script-
#!/bin/bash
set -euo pipefail

source=$1
backup=$2
timestamp=$(date '+%y-%m-%d-%H-%M-%S')


Display() {
        echo "Usage:./backup.sh <source><backup>"
}

if [ $# -eq 0 ];then
        Display
fi

backup() {
        archive_name="${backup}/new_${timestamp}.tar.gz"
        if tar -czvf "$archive_name" "$source";then
                echo "file created successfully $timestamp"
        else
                echo "file creation unsucessful."
                exit 1
        fi
        size=$(du -sh "$archive_name")
        echo "$archive_name Created Succesfully having size: $size"
        echo "Deleting archives more than 14 days."
        find "$backup" -name "new_*.tar.gz" -type f -mtime +14 -delete

}

backup

Output-
yogesh_jawlekar@Profound:~/script/day19$ ./backup.sh source backup
source/
source/file1.txt
source/file2.txt
source/large_file.log
file created successfully 26-05-13-17-55-45
backup/new_26-05-13-17-55-45.tar.gz Created Succesfully having size: 4.0K       backup/new_26-05-13-17-55-45.tar.gz
Deleting archives more than 14 days.

Summary-
In this script we first set our variables which we will use as our arguments.
then we created a function to check our arguments.
then we created a function called backup where we first set our variable which will define the path files where we have to save the .tar.gz files and then by using if condition and -tar czvf we compressed and gzip those files into our abckup folder from the source
if that becomes sucessful it will echo the output sucessful or unsuccessful.
then we set our size variable using du -sh with our first variable.
then we printed our file name using first variable and size variable to check the file size created.
Then to deleted we used find to search and we used -name to search the path and "new_*.tar.gz" -type f to search the files with exact names and -mtime to delete those files.


#Task 3: Crontab
1.Read: crontab -l — what's currently scheduled?
--yogesh_jawlekar@Profound:~/script/day19$ crontab -l
no crontab for yogesh_jawlekar

2.Did crontab -e and set a cronjob as per below entries?

 43 18 * * 3 /bin/bash /home/yogesh_jawlekar/script/day19/backup.sh /home/yogesh_jawlekar/script/day19/source /home/yogesh_jawlekar/script/day19/backup

 Output-
 2026-05-13T18:43:01.368838+00:00 Profound CRON[16134]: (yogesh_jawlekar) CMD (/bin/bash /home/yogesh_jawlekar/script/day19/backup.sh /home/yogesh_jawlekar/script/day19/source /home/yogesh_jawlekar/script/day19/backup)

 Summary-To set a cronjob we need to first set the date and time as per the cron criteria the command in the above case was ./backup.sh source backup.
 hence as per that we have entered the data in crontab -e the crons time with the paths of the commands and their arguments.
 To cross verify wether the cron ran or not checked the folder itself also the cron logs by doing-grep CRON /var/log/syslog | tail -n 20.



 #ask 4: Combine — Scheduled Maintenance Script
 Script-
 #!/bin/bash
set -eo pipefail


timestamp=$(date '+%Y-%m-%d %H:%M:%S')
source ./backup.sh

echo "Maintenace started at $timestamp">> /var/log/maintenance.log

backup >> /var/log/maintenance.log

echo "Maintenace finished at $timestamp">> /var/log/maintenance.log

Output-Maintenace started at 26-05-14-02-01-24
Maintenace started at 26-05-14-02-03-54
Maintenace started at 26-05-14-02-05-14
source/
source/file1.txt
source/file2.txt
source/large_file.log
file created successfully 26-05-14-02-05-14
backup/new_26-05-14-02-05-14.tar.gz Created Succesfully having size: 4.0K       backup/new_26-05-14-02-05-14.tar.gz
Deleting archives more than 14 days.
Maintenace finished at 26-05-14-02-05-14

Summary-
In this I learned that earlier we took the actual backup of the files but it is also important to keep logs of the same process in seprate log file.


 
