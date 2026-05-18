###Task 1: Understanding Branches
1.What is a branch in Git?
-In git we create branches in order to carry out different kind of work for the same project for eg there is master/main branch which is often the first and foremost branch then there might be other branches for that same project for testing,quality assurance or for any other 
changes.
   * Isolation: It allows you to work on a new feature, bug fix, or experiment in a separate environment without
     affecting the stable main or production code.
   * Parallel Development: Multiple developers can work on different branches simultaneously without interfering with
     each other's progress.
   * Workflow Management: Common patterns include using branches for feature/, bugfix/, hotfix/, or environment-specific
     stages like development and qa.

2.Why do we use branches instead of committing everything to main?
-Comitting everything to main branch will lead to mess instead of that we can use branching strategies which will allow us to work on new features,bug fixes etc without affecting the stable or production envoirmnet.
3.What is HEAD in Git?
-HEAD is basically a pointer which appears in commit history to tell us what was the last commit done.

4.What happens to your files when you switch branches?
-As I mentioned earlier branches allows us to work in isolation the files are also isolated in branches until we merge them.

###Task 2: Branching Commands — Hands-On
1.List all branches in your repo
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch
* master
2.Create a new branch called feature-1
-yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch feature-1
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch
  feature-1
* master
  
2.Switch to feature-1
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git switch feature-1
Switched to branch 'feature-1'

3.Create a new branch and switch to it in a single command — call it feature-2
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git checkout -b feature-2
Switched to a new branch 'feature-2'
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch
  feature-1
* feature-2
  master

4.Try using git switch to move between branches — how is it different from git checkout?
Both options can be used to switch between branches but git checkout can also be used to restore working tree files.

5.Make a commit on feature-1 that does not exist on main
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git add .
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git commit -m "Only for feature-1"
[feature-1 b9e55f9] Only for feature-1
 1 file changed, 2 insertions(+)

6.Switch back to main — verify that the commit from feature-1 is not there-
    yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch
      feature-1
      feature-2
    * master
    yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git log
    commit fe568b320edf7d96125e173070d1153aa3fbbc7c (HEAD -> master, feature-2)
    Author: Yogesh Jawlekar <yjawlekar@gmel.com>
    Date:   Sun May 17 17:46:19 2026 +0000
    
        Summary added
    
    commit 7da71761d74c716a0234ca9b406e4c79e6019561
    Author: Yogesh Jawlekar <yjawlekar@gmel.com>
    Date:   Sun May 17 17:44:45 2026 +0000
    
        New commands added
    
    commit 2ede56118dccd0f3f81cd306ec8d87eaa64a5c4b
    Author: Yogesh Jawlekar <yjawlekar@gmel.com>
    Date:   Sun May 17 17:34:44 2026 +0000
    
        Basic git commands
7.Delete a branch you no longer need
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch -d feature-2
Deleted branch feature-2 (was fe568b3).

8.Add all branching commands to your git-commands.md
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git add .
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git commit -m "branching commands added"
[master 77f0dcb] branching commands added
 1 file changed, 8 insertions(+)


###Task 3: Push to GitHub
1.Create a new repository on GitHub (do NOT initialize it with a README)
DONE

2.Connect your local devops-git-practice repo to the GitHub remote
-yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git remote set-url origin git@github.com:yjavlekar-cyber/gitpractice.git
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git remote -v
origin  git@github.com:yjavlekar-cyber/gitpractice.git (fetch)
origin  git@github.com:yjavlekar-cyber/gitpractice.git (push)

3.Push your main branch to GitHub
-yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git push origin main
Enumerating objects: 18, done.
Counting objects: 100% (18/18), done.
Delta compression using up to 8 threads
Compressing objects: 100% (12/12), done.
Writing objects: 100% (18/18), 2.25 KiB | 1.13 MiB/s, done.
Total 18 (delta 5), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (5/5), done.
To github.com:yjavlekar-cyber/gitpractice.git
 * [new branch]      main -> main
3.Push feature-1 branch to GitHub
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git push origin feature-1
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 334 bytes | 334.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'feature-1' on GitHub by visiting:
remote:      https://github.com/yjavlekar-cyber/gitpractice/pull/new/feature-1
remote:
To github.com:yjavlekar-cyber/gitpractice.git
 * [new branch]      feature-1 -> feature-1

4.Verify both branches are visible on GitHub
-Yes both branches are visible on github.

5.Answer in your notes: What is the difference between origin and upstream?
-with and example if i have to explain there is a companies repo which has code and if we are working with that project we cannot directly push and pull from their repo but we can fork it into our github and then we can pull that from github that we can call cloning or pulling
from origin repo and if their are any updates in that repo through upstream we can directly pull those from that company repo.

to upstream we need to add the url for that 
 git remote add upstream https://github.com/microsoft/vscode.git
 then
  git pull upstream main

###Task 4: Pull from GitHub
1.Make a change to a file directly on GitHub (use the GitHub editor)
Pull that change to your local repo
yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git pull origin main
From github.com:yjavlekar-cyber/gitpractice
 * branch            main       -> FETCH_HEAD
Updating 8f7b1f7..066665c
Fast-forward
 git-commands.md | 4 ++++
 1 file changed, 4 insertions(+)


Answer in your notes: What is the difference between git fetch and git pull?
-git pull we do when we want to pull our changes made in github remote into our local.
-git fetch basically shows us the changes and does not make any actuall changes in our local repo.

###Task 5: Clone vs Fork
What is the difference between clone and fork?
-clone is pulling first time from github repo.
-forking is basically cloning but from github repo into our github.
Forking happens Cloud-to-Cloud. Cloning happens Cloud-to-Local.

When would you clone vs fork?
-I will use clone when i want to pull a repo for the first time.
-I will fork when i want to get some other repo into my github.

After forking, how do you keep your fork in sync with the original repo?
-by doing sync fork i will keep the fork in sync.
