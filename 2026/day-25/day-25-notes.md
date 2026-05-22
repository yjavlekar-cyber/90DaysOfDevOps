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
## Task 2: Git Revert — Hands-On
    Make 3 commits (commit X, Y, Z)
    Revert commit Y (the middle one) — what happens?
    Check git log — is commit Y still in the history?
## Answer in your notes:
### How is git revert different from git reset?
    What git revert does is that it revertes the changes of that particular commit but in comit history/logs the original commit will still reflect but in addition
    as head there will be a new commit saying commit reverted.
    But in reset it deleted the commit also if we used mixed and hard it can change the file as well.
    
### Why is revert considered safer than reset for shared branches?
    If we use reset in shared branches if on one commit we did reset it can create problems to others with whom we are sharing those branches 
    the foundation of commits on which other people might be working might disapper because of reset.
    But in revert the original commit is still their though the file is changed.
    
### When would you use revert vs reset?
#### revert 
    - we can use revert if we are not sure wether to delete or to keep the commit in that case we can revert because as and when if we have to again undo the revert that option is also available.
    If the code is already pushed we can use revert because if someone has already pulled and started working and then we do revert it will not delete the commit it will just create a new commit to only hide that commit
    which we are reverting but if someone is making change on the same commit which we reverted then there will merge conflict which can be resolved by the other person.
    
#### reset
    - To delete any unwanted commits done or any unwanted changes we can use revert.
    reset we should only use until the code is on only our laptop not pushed yet.

## Reset vs Revert — Summary

|          | git reset | git revert |
| -------- | --------  | --------   |
| What it does? | Can delete the commit history and file changes as well | Creates new commit which will gide the commit we are reverting |
| Removes commit from history? | Yes | No, but hides it. |
| Safe for shared/pushed branches? | NO | Yes |
| When to use? | To delete any unwanted changes from our local. | If we are not sure about the changes we can revert when code is pushed. |
