# Bash Scripting Challenge: Log Analyzer and Report Generator
In this assignment i have created two scripts one for all the code related to process the log file and another one to transfer the same into a txt file.
SCRIPT- log_analyzer.sh
=bin/bash

lofi=$1

logs() {
                if [ $# -eq 0 ];then
                        echo "Error No Arguments!"
                else

                        if [ ! -f "$1" ];then
                                echo "File doesn't exist"

                        else
                                echo "File exists"
                                Total_lines=$(wc -l "$lofi")
                                echo "$Total_lines."
                                echo "  Processing logs."
                                echo "*                 *"
                                echo " *               *"
                                echo "  *             *"
                                echo "   *           *"
                                echo "    * loading *"

                        fi
                fi

        }





count() {

        if [  -f "$1" ];then

                echo "Counting lines haveing Error and failed keywords."
                echo "_________________________________________________"



                echo ""
                error_count=$(grep -c "ERROR" $1)
                if [ $? -eq 0 ];then
                        echo "Total Errors:$error_count"

                fi

                echo ""


                fail_count=$(grep -c "Failed" $1)
                if [ $? -eq 0 ];then

SCRIPT-summary.sh
==#!/bin/bash
timestamp=$(date +%Y-%m-%d)
log_file="Summary_$timestamp.txt"
logfile=$1

if [ -z "$logfile" ]; then
     echo "Error: No log file provided."
     echo "Usage: $0 <path_to_log_file>"
     exit 1
fi



echo "Date of analysis: $timestamp">>"$log_file"

echo "Log file: $logfile" >> "$log_file"



source ./log_analyzer.sh



logs "$logfile" >> "$log_file"


count "$logfile" >> "$log_file"


OUTPUT-
Data redirected to the file with name Summary_2026-05-14.txt
Date of analysis: 2026-05-14
Log file: sample.log
File exists
101 sample.log.
  Processing logs.
*                 *
 *               *
  *             *
   *           *
    * loading *
Counting lines haveing Error and failed keywords.
_________________________________________________

Total Errors:72

Total Failures:4

Please find below lines containing keyword 'CRITICAL'
     1  2025-07-29 10:15:23 CRITICAL Disk space below threshold on /var/log
     2  2025-07-29 14:32:01 CRITICAL Database connection lost - primary node down

All lines containing 'ERROR'
     1  2025-07-29 10:05:12 ERROR Connection timed out while reaching upstream server
     2  2025-07-29 10:07:12 ERROR Connection timed out while reaching upstream server
     3  2025-07-29 10:20:45 ERROR File not found: /app/data/cache/tmp_0921.dat
     4  2025-07-29 10:26:15 ERROR Permission denied: Cannot write to /app/output/report.pdf
     5  2025-07-29 10:30:12 ERROR Connection timed out while reaching upstream server
     6  2025-07-29 10:40:10 ERROR Permission denied: Cannot write to /app/output/report.pdf
     7  2025-07-29 10:42:05 ERROR Connection timed out while reaching upstream server
     8  2025-07-29 10:45:30 ERROR File not found: /app/images/logo_v2.png
     9  2025-07-29 10:50:18 ERROR Disk I/O error on sector 0x4F22
    10  2025-07-29 11:00:12 ERROR Connection timed out while reaching upstream server
Top 5 most common error masaages
     24    ERROR Connection timed out while reaching upstream server
      2    ERROR Permission denied: Cannot write to /app/output/report.pdf
      1    ERROR Permission denied: UID 1001 attempted write to /etc/passwd
      1    ERROR Permission denied: SSH key has wrong permissions
      1    ERROR Permission denied: SELinux policy violation

commands used:
I have used commands like grep,awk,cat,wc -l,sort,head and uniq -c.

#What did I learn?
In this particular assignment I got idea how the log files are processed and how the reports are generated.
This assignement helped me to build logic around the processing of log files.
Did hands on the major commands like awk,grep which are very useful why processing log files.

