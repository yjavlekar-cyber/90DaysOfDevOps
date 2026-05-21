# Git Reset vs Revert & Branching Strategies
## Task 1: Git Reset — Hands-On
    Make 3 commits in your practice repo (commit A, B, C)
    Use git reset --soft to go back one commit — what happens to the changes?
    Re-commit, then use git reset --mixed to go back one commit — what happens now?
    Re-commit, then use git reset --hard to go back one commit — what happens this time?
    Answer in your notes:
### What is the difference between --soft, --mixed, and --hard?
    -- soft = this deletes the commit.
    -- mixed = This deletes the commit takes the file back to unstaged cateogry but keeps the file as it is.
    -- hard = Hard deletes all three the commit,gets file to unstaged and modifys the file to the stage before that particular deleted commit.
    
    git reset --soft HEAD~1 - to delete the last one commit.

### Which one is destructive and why?
      In all three the destructive is -- hard because it wipes out the commits and changes the files.
      
### When would you use each one?
    -- soft = Only to delete the commit.
    -- mixed = to deleted commit and to get files back to unstaged.
    -- hard = To deleted,unstage and change the file.

### Should you ever use git reset on commits that are already pushed?
     No, because if someone has already started working on them commits they might face problem.
