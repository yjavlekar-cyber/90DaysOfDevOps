##Task 1: Install and Configure Git
1.Verify Git is installed on your machine
yogesh_jawlekar@Profound:~/script/day22$ git --version
git version 2.43.0

2.Set up your Git identity — name and email
yogesh_jawlekar@Profound:~/script/day22$ git config --global user.name "Yogesh Jawlekar"
yogesh_jawlekar@Profound:~/script/day22$ git config --global user.email "yjawlekar@gmel.com"

3.Verify your configuration
yogesh_jawlekar@Profound:~/script/day22$ git config user.name
Yogesh Jawlekar
yogesh_jawlekar@Profound:~/script/day22$ git config user.email
yjawlekar@gmel.com

##Task 2: Create Your Git Project
1.Create a new folder called devops-git-practice
yogesh_jawlekar@Profound:~/script/day22$ mkdir devops-git-practice
yogesh_jawlekar@Profound:~/script/day22$ ls
devops-git-practice

2.Initialize it as a Git repository
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /home/yogesh_jawlekar/script/day22/devops-git-practice/.git/

3.Check the status — read and understand what Git is telling you
Once we intilized local git repo by using git init it informing us that majorly for branches main as  name is used and our by default name is master.
It is asking us to change that globaly by doing-
git config --global init.defaultBranch <name>
or only for current repo -
git branch -m <name>

4.Explore the hidden .git/ directory — look at what's inside
We can check once the directory is intilized into git repo it creates a hidden folder with name .git
It has various folders such as HEAD,branches,config etc

##Task 3: Create Your Git Commands Reference
1.Create a file called git-commands.md inside the repo-
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ touch git-commands.md
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ ls
git-commands.md

2.Add the Git commands you've used so far, organized by category:
Setup & Config
Basic Workflow
Viewing Changes

##3.Task 4: Stage and Commit
1.Stage your file
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git add git-commands.md

2.Check what's staged
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git status
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   git-commands.md

3.Commit with a meaningful message
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git commit -m "Basic git commands"
[master (root-commit) 2ede561] Basic git commands
 1 file changed, 16 insertions(+)
 create mode 100644 git-commands.md

4.View your commit history
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git log
commit 2ede56118dccd0f3f81cd306ec8d87eaa64a5c4b (HEAD -> master)
Author: Yogesh Jawlekar <yjawlekar@gmel.com>
Date:   Sun May 17 17:34:44 2026 +0000

    Basic git commands

##Task 5: Make More Changes and Build History
1.Edit git-commands.md — add more commands as you discover them
##SETUP AND CONFIG
---git --version- Tells what version of git is installed.
---git config --global user.name "Yogesh Jawlekar"-To set username for commit history.
---git config --global user.email "yjawlekar@gmel.com"-To set email of the username to list in commit history.
##BASIC WORKFLOW
---git init:Git init lets us intialize the local repo into a git repository to use it further to push or pull from remote repo.
---git add filename-lets us add the file into staging.
---git status-lets us check the status of the file if red then unstaged if green staged.
---git commit -m "commit message"-By this command we commit our changes into the git commit means basically keeping record of the changes.
Thats why git is called VCS (Version control system).
---git log/git log --oneline0- lets us check the commit history it shows the changes made earlier with details like who made those change which can be identified through username.

2.Check what changed since your last commit
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git-commands.md

no changes added to commit (use "git add" and/or "git commit -a")
3.Stage and commit again with a different, descriptive message
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git add .
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git commit -m "New commands added"
[master 7da7176] New commands added
 1 file changed, 8 insertions(+), 5 deletions(-)
4.Repeat this process at least 3 times so you have multiple commits in your history
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ vim git-commands.md
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git add .
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git commit -m "Summary added"
[master fe568b3] Summary added
 1 file changed, 1 insertion(+), 1 deletion(-)
5.View the full history in a compact format
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git log --oneline
fe568b3 (HEAD -> master) Summary added
7da7176 New commands added
2ede561 Basic git commands


Task 6: Understand the Git Workflow:
1.What is the difference between git add and git commit?
-Through git add we can add the file into staging but through git commit we add the same file in tracked.

2.What does the staging area do? Why doesn't Git just commit directly?
- suppose there are more than one change which should be kept seprate we do git commit directly those changes will get commited directly but if we do it one by one we will get diff comit history for different change due to this our history will not become messy.
  
3.What information does git log show you?
git log shows author section where username and its email is stored.
date and below date there is our commit message.

4.What is the .git/ folder and what happens if you delete it?
-.git folder is like brain of our project it has all the configs files and other things until and unless we want to restart we should not delete because deleting .git folder will reverse our git repo into normal file system and we will also lose the data or earlier history.

5.What is the difference between a working directory, staging area, and repository?
-working directory is the directory in which we do changes in our file in our shell.
-staging area is where we keep our changes before commiting them.
-repository-we can say repositry is our .git folder because it stores all the commits done by us in hash/encoded manner.
