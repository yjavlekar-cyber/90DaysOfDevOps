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
#### What does rebase actually do to your commits?
      Rebase puts the commit history from current branch at the top.
#### How is the history different from a merge?
      When we do merge the history is basically as per the time but as i said rebase puts current branches history at the top and then other branches.
      
#### Why should you never rebase commits that have been pushed and shared with others?
      You should never rebase shared commits because it rewrites the commit IDs. If others have already started working on those commits, your rebase will force them to manually fix their entire history,
      causing major confusion and potential code loss.
      And whenever we rebase and get the commits on top using rebase the old ids of those commits gets deleted and new ones are generated which are now at the top.
      
#### When would you use rebase vs merge?
        I will use merge to view the linear history of the commits with the specific timelines but in rebase basically what happens if there is a feature branch where we have done small small changes or any other changes which are not neccesary and all are commited 
        by doing rebase we will get them at the top and squash that into a single commit so that only finished commit we will be able to see.

## Task 3: Squash Commit vs Merge Commit
### 1.Create a branch feature-profile, add 4-5 small commits (typo fix, formatting, etc.)
    - created and switched to branch using git checkout -b feature-profile and then edited the git commands file and added two commits to it.
### 2.Merge it into main using --squash — what happens?
        merged it into main using git merge main --squash
### 3.Check git log — how many commits were added to main?
     as checked no commits were directly added to main after doing merge squash we had to do git add and commit to name the squashed commit.
     
### 4.Now create another branch feature-settings, add a few commits
        Done
        
### 5.Merge it into main without --squash (regular merge) — compare the history
    merged into main but unlike squash commits were directly added to the commit history of main.
    
### 6.Answer in your notes:
#### 1.What does squash merging do?
    when we squash merge one branches commit history into another it basically transforms all the commits into one single commit but it doesnt get directly added we have to first do git add and commit with a final message.
    
#### 2.When would you use squash merge vs regular merge?
    I will use squash merge when i want to merge a branch into main but in that branch there too many unwanted commits which can be transformed into one single commit.
    I would use reqular merge when the whole commit history with each and every commit is required to maintain i will opt for regular merge.
#### 3.What is the trade-off of squashing?
    git rebase -i     In normal squashing we squash all the commits but in trade off we only squash which are junk commits.

## Task 4: Git Stash — Hands-On
### 1.Start making changes to a file but do not commit
      Done
### 2.Now imagine you need to urgently switch to another branch — try switching. What happens?
    Before commiting if i am doing the branch switch it is informing that local files in that branch will be overwritten it asking ton either add and commit or stash the changes.
### 3.Use git stash to save your work-in-progress
    Done and It gave this: Saved working directory and index state WIP on profile: 8428c47 to confirm.
### 4.Switch to another branch, do some work, switch back
    Did few commits in another branch.
    
### 5.Apply your stashed changes using git stash pop
     So once switched back to branch where we had our stashed file if we do git status it will not show anything but we do git stash pop it will reflect the earlier file that we stashed i mean the changes that we stashed.
     
### 6.Try stashing multiple times and list all stashes
    Did tried stashing 4 times each time with minor changes it saved every stash but when i did git stash pop it only poped the latest one.
    
### 7.Try applying a specific stash from the list
    To get the list of all the stashed changes we need to do git stash list.
    and also remember that this list works in LIFO method that means if the lastes is 0 than if we add one more the earlier will go to 1 and next to that will become 0.
    to apply anyone we need to use below command
    git stash apply stash@{0}
    
### Answer in your notes:
#### 1.What is the difference between git stash pop and git stash apply?
    - git stash pop- only gives us our last stashed change.
    - git stash apply- On the other hand git stash apply allows us to choose from the list of our stashes to apply and the add and commit.
    
#### 2.When would you use stash in a real-world workflow?
    In a real-world workflow if suppose i am in a branch doing something in a file if in any urgency i have to switch to a branch without commiting those changes i will use git stash which will stash my changes into a stash list which will be hiddem until i do git stash pop.

## Task 5: Cherry Picking

