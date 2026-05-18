# Task 1: Git Merge — Hands-On
## 1.Create a new branch feature-login from main, add a couple of commits to it.
- yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch feature-login
  yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch
    feature-1
    feature-login
  *main

  
## 2.Switch back to main and merge feature-login into main
- yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git merge feature-login
  Updating 066665c..1c040da
  Fast-forward
   git-commands.md | 2 ++
   1 file changed, 2 insertions(+)
- yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git log
  commit 1c040dae00e76e513ea7d2a8047b74919c339fbd (HEAD -> main, feature-login)
  Author: Yogesh Jawlekar <yjawlekar@gmel.com>
  Date:   Mon May 18 16:01:00 2026 +0000
  
      merge 2
  
  commit bd8fddbc8d4d3b894ab482f36cfbfc58eada461f
  Author: Yogesh Jawlekar <yjawlekar@gmel.com>
  Date:   Mon May 18 15:59:44 2026 +0000
  
      merge 1
## 2.Observe the merge — did Git do a fast-forward merge or a merge commit?
- git did fastforward merge.
- so basically if i have to explain this in one line fast forwards combines earlier commits from main and new commits from feature login in linear form but in commit merge we can visually see that main has
  this this commits and feature-login has this this commits.
   * Fast-Forward: History looks like a single lane road.
   * Merge Commit: History looks like a highway junction where two roads join together.

Now create another branch feature-signup, add commits to it — but also add a commit to main before merging
Merge feature-signup into main — what happens this time?
Answer in your notes:
What is a fast-forward merge?
When does Git create a merge commit instead?
What is a merge conflict? (try creating one intentionally by editing the same line in both branches)
