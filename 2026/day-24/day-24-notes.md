# Day 24 – Advanced Git: Merge, Rebase, Stash & Cherry Pick
## Task 1: Git Merge — Hands-On
### 1.Create a new branch feature-login from main, add a couple of commits to it.
    - yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch feature-login
      yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git branch
        feature-1
        feature-login
      *main

  
### 2.Switch back to main and merge feature-login into main
    - yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git merge feature-login
      Updating 066665c..1c040da
      Fast-forward
       git-commands.md | 2 ++
       1 file changed, 2 insertions(+)
    - yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git log
        * commit 1c040dae00e76e513ea7d2a8047b74919c339fbd (HEAD -> main, feature-login)
        Author: Yogesh Jawlekar <yjawlekar@gmel.com>
        Date:   Mon May 18 16:01:00 2026 +0000
      
          merge 2
      
        * commit bd8fddbc8d4d3b894ab482f36cfbfc58eada461f
        Author: Yogesh Jawlekar <yjawlekar@gmel.com>
        Date:   Mon May 18 15:59:44 2026 +0000
      
          merge 1
### 2.Observe the merge — did Git do a fast-forward merge or a merge commit?
    - git did fastforward merge.
    - so basically if i have to explain this in one line fast forwards combines earlier commits from main and new commits from feature login in linear form but in commit merge we can visually see that main has
      this this commits and feature-login has this this commits.
       * Fast-Forward: History looks like a single lane road.
       * Merge Commit: History looks like a highway junction where two roads join together.

### 3.Now create another branch feature-signup, add commits to it — but also add a commit to main before merging
    - git branch feature-signup
    - git commit -m "In signup branch"
    - git switch main
    - git commit -m "In main branch"

  
### 4.Merge feature-signup into main — what happens this time?
    -   git merge feature-signup(in main branch)
    -   Now we can see our earlier commits of main branch then commits of our feature-login then commits of feature-signup and again commits done on main branch.

  
### Answer in your notes:
  * 1.What is a fast-forward merge?
    - Fast-forward is the kind of merge which create a linear commit history.
    
  * 2.When does Git create a merge commit instead?
    - when we use git merge main --no ff this manual way.
    - suppose we are in feature branch and we want to merge in the merge into main branch but our main branch has moved forward with its own commit history in that case fast forward is not possible.
    
  * 3.What is a merge conflict? (try creating one intentionally by editing the same line in both branches)
    - merge conflict is basically same change has been conducted by main branch and feature branch and when we try to merge them both same changes collide which creates merge conflict.


## Task 2: Git Rebase — Hands-On
### 1.Create a branch feature-dashboard from main, add 2-3 commits
    - git checkout -b feature-dashboard
    - added two commits
### 2.While on main, add a new commit (so main moves ahead)
    - git switch main (switched to main branch)
    - Did commit from main removed some of the earlier lines

### 3.Switch to feature-dashboard and rebase it onto main
    - git switch feature-dashboard( switched to another branch)
    - git rebase main (from feature branch)

### 4.Observe your git log --oneline --graph --all — how does the history look compared to a merge?
      yogesh_jawlekar@Profound:~/script/day22/devops-git-practice$ git log --oneline --graph --all
    - this basically tells that there is one main branch and adjascent to that on the right side there are other branches we created for change purpose or anyother purpose.

### 5.Answer in your notes:
    - What does rebase actually do to your commits?
      Rebase puts the commit history from current branch at the top.
    - How is the history different from a merge?
      When we do merge the history is basically as per the time but as i said rebase puts current branches history at the top and then other branches.
      
    - Why should you never rebase commits that have been pushed and shared with others?
      You should never rebase shared commits because it rewrites the commit IDs. If others have already started working on those commits, your rebase will force them to manually fix their entire history,
      causing major confusion and potential code loss.
      
When would you use rebase vs merge?
