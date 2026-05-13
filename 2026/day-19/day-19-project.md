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


 
