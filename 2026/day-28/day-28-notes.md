# Day 28 – Revision Day: Everything from Day 1 to Day 27
## Task 1: Self-Assessment Checklist
### Linux
- [x] Navigate the file system, create/move/delete files and directories-Can do confidently
- [x] Manage processes — list, kill, background/foreground-Can do confidently
- [x] Work with systemd — start, stop, enable, check status of services-Can do confidently
- [x] Read and edit text files using vi/vim or nano-Can do confidently
- [x] Troubleshoot CPU, memory, and disk issues using top, free, df, du-Need to revisit
- [x] Explain the Linux file system hierarchy (/, /etc, /var, /home, /tmp, etc.) -Need to revisit
- [x] Create users and groups, manage passwords -Can do confidently
- [x] Set file permissions using chmod (numeric and symbolic)-Can do confidently
- [x] Change file ownership with chown and chgrp-Can do confidently
- [x] Create and manage LVM volumes -Can do confidently
- [x] Check network connectivity — ping, curl, netstat, ss, dig, nslookup -Need to revisit
- [ ] Explain DNS resolution, IP addressing, subnets, and common ports -Need to revisit

### Shell Scripting
- [x] Write a script with variables, arguments, and user input -Can do confidently
- [x] Use if/elif/else and case statements -Need to revisit
- [x] Write for, while, and until loops -Need to revisit
- [x] Define and call functions with arguments and return values -Need to revisit
- [x] Use grep, awk, sed, sort, uniq for text processing -Need to revisit
- [x] Handle errors with set -e, set -u, set -o pipefail, trap -Need to revisit
- [x] Schedule scripts with crontab -Need to revisit

### Git & GitHub
- [x] Initialize a repo, stage, commit, and view history -Can do confidently
- [x] Create and switch branches -Can do confidently
- [x] Push to and pull from GitHub -Can do confidently
- [x] Explain clone vs fork -Can do confidently
- [ ] Merge branches — understand fast-forward vs merge commit -Need to revisit
- [ ] Rebase a branch and explain when to use it vs merge -Need to revisit
- [x] Use git stash and git stash pop -Can do confidently
- [x] Cherry-pick a commit from another branch-Can do confidently
- [x] Explain squash merge vs regular merge -Can do confidently
- [ ] Use git reset (soft, mixed, hard) and git revert -Need to revisit
- [ ] Explain GitFlow, GitHub Flow, and Trunk-Based Development -Need to revisit
- [x] Use GitHub CLI to create repos, PRs, and issues -Can do confidently



## Task 3: Quick-Fire Questions
Answer these from memory (no Googling). Then verify your answers:
### 1.What does chmod 755 script.sh do?
    chmod 755 means giving read,write and execution permission to owner and only read and executing permissions to script.sh

### 2.What is the difference between a process and a service?
    Process is basically the background activity going and service for example can be nginx,docker which we use to do some operations which runs as a processs in the background.

### 3.How do you find which process is using port 8080?
    ss -tulpn can be used to check the process which are using 8080.

### 4.What does set -euo pipefail do in a shell script?
    The set -euo pipefail in a script basically if in a script in any command if their is any mistake or error it will stop the script,
    or if thier is any unbound variable then also it will stop the script and also if their is any pipeline command and in that if one command fails the whole pipeline will fail.


### 5.What is the difference between git reset --hard and git revert?
    git reset basicaly deletes the commit history also changes the file and unstages it while revert only creates a mask for that particular commit which is still thier in commit history.

### 6.What branching strategy would you recommend for a team of 5 developers shipping weekly?
    github flow is the correct strategy for this.

### 7.What does git stash do and when would you use it?
    If we want to switch immediaetly from one branch to another and we are changing any file we can just stash that file go the another branch return here and do git stash pop we will get the changes with out staging and commiting the file.

### 8.How do you schedule a script to run every day at 3 AM?
    Via cron job we can set script to run every day at 3am
    0 3 * * 7

### 9.What is the difference between git fetch and git pull?
    Git fetch only fetchs the file and shows us but git pull gets the file into our local.

### 10.What is LVM and why would you use it instead of regular partitions?
    LVM are logical volumes which are created from volume groups which are created from phyical volumes.
      we use lvm because we can resize them as per our wants without changing any thing in disk.

