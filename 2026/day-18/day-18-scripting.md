#Task 1: Basic Functions
Script-
#!/bin/bash
greet() {
        name=$1
        echo "my name is $name"
}
greet "yogesh"
add() {
        sum=$(($1 + $2))
        echo "$sum"
}
add 1 2
Output-
yogesh_jawlekar@Profound:~/script/day18$ ./functions.sh
my name is yogesh
3



#Task 2: Functions with Return Values
Script-
#!/bin/bash
check_disk() {
        echo "____DISK_USAGE_____"
        df -h|awk '/rootfs/ {print $3}'
}
check_memory() {
        echo "___FREE MEMORY___"
        free -h|awk '/Mem/ {print $4}'
}
echo "SYSTEM HEALTH CHECK"
echo "------------------"
check_disk
echo ""
check_memory
echo "------------------"
Output-
yogesh_jawlekar@Profound:~/script/day18$ ./disk_check.sh
SYSTEM HEALTH CHECK
------------------
____DISK_USAGE_____
2.7M

___FREE MEMORY___
332Mi
------------------



#Task 3: Strict Mode — set -euo pipefail
1)set -e 
If on top of the script below shebang we put set -e it works as a signal for script to stop executing the script whenever there is an error.
It means in chain of commands the script will stop running even if one command fails it will not execute the commands after that even they are proper.
  Script-
  #!/bin/bash
  set -e
  mkdir strict_demo.sh
  mkdir new directory
  
  Output-yogesh_jawlekar@Profound:~/script/day18$ ./strict_demo.sh
  mkdir: cannot create directory ‘strict_demo.sh’: File exists

Above there are two commands in the first command the file already exist but the second one is proper still in the output commands execution stopped at the error of first command only.

2)set -u
This basically informs us that if we use any variable like in the example for which we have not assigned any value that will give us an output which says unbound variables.

Script-
        #!/bin/bash
        set -u
        echo "My name is $name."
        Output-yogesh_jawlekar@Profound:~/script/day18$ ./strict_demo.sh
        ./strict_demo.sh: line 6: name: unbound variable

3)set -o pipefail- 
In set -o pipefail if there are two commands seperated by pipe like in the example usually if we ran commands which are divided by pipe where the first commands if fails the exit code is 1 which is an error but the other command returns exit 0 which is 
success even after the command fails due to this what happens the script keeps running but if we define set -o pipefail if command like this fails the script immediately stops.

Script-#!/bin/bash
        set -o pipefail
        df -h /n | awk '{print $1}'
        echo "Success"

Output-
yogesh_jawlekar@Profound:~/script/day18$ ./strict_demo.sh
df: /n: No such file or directory



#Task 4: Local Variables
Basically, all the varibales inside or outside of the function acts as a global function unless before the variable we assign the keyword as local as shown below example.

Script-
#!/bin/bash
loc () {
   local name=yogesh
echo "My name is $name."
}
loc
echo "My name is $name."

Output-
yogesh_jawlekar@Profound:~/script/day18$ ./local_demo.sh
My name is yogesh.
My name is .

#Task 5: Build a Script — System Info Reporter
Script-
#!/bin/bash
set -euo pipefail
host() {
        uname -a
        cat /etc/os-release
}
up() {
        uptime
}
disk() {
        df -h | head -5
}
mem() {
        free -h
}
cpu() {
         echo "PID    USER    %CPU   %MEM   COMMAND"
         ps -eo pid,user,%cpu,%mem,command --sort=-%cpu | awk 'NR>1 && NR<=6 {printf "%-6s %-8s %-6s %-6s %.50s\n", $1, $2, $3, $4, $5}'
}
main() {
        echo "--------------------"
        echo  "SYSTEM INFORMATION"
        echo "--------------------"
        echo ""
        echo "HOSTNAME"
        host
        echo "____________________"
        echo ""
        echo "UPTIME"
        up
        echo "___________________"
        echo ""
        echo "DISK USAGE(TOP 5)"
        disk
        echo "__________________"
        echo ""
        echo "MEMORY AVAILABLE"
        mem
        echo "_________________"
        echo ""
        echo "TOP CPU PROCESS"
        cpu
        echo "_________________"
}
main

Output-
yogesh_jawlekar@Profound:~/script/day18$ ./system_info.sh
--------------------
SYSTEM INFORMATION
--------------------

HOSTNAME
Linux Profound 6.6.87.2-microsoft-standard-WSL2 #1 SMP PREEMPT_DYNAMIC Thu Jun  5 18:30:46 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
PRETTY_NAME="Ubuntu 24.04.4 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.4 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
____________________

UPTIME
 05:43:38 up  2:24,  1 user,  load average: 0.59, 0.33, 0.17
___________________

DISK USAGE(TOP 5)
Filesystem      Size  Used Avail Use% Mounted on
none            1.9G     0  1.9G   0% /usr/lib/modules/6.6.87.2-microsoft-standard-WSL2
none            1.9G  4.0K  1.9G   1% /mnt/wsl
drivers         476G  462G   14G  98% /usr/lib/wsl/drivers
/dev/sdd       1007G   22G  935G   3% /
__________________

MEMORY AVAILABLE
               total        used        free      shared  buff/cache   available
Mem:           3.7Gi       1.8Gi       297Mi        38Mi       1.9Gi       2.0Gi
Swap:          1.0Gi          0B       1.0Gi
_________________

TOP CPU PROCESS
PID    USER    %CPU   %MEM   COMMAND
2170   root     4.5    7.0    kube-apiserver
2158   root     2.6    1.9    etcd
1730   root     2.4    2.3    /usr/bin/kubelet
2203   root     1.8    2.6    kube-controller-manager
1670   root     1.1    2.0    /usr/bin/kubelet
_________________

_____THE END_____
