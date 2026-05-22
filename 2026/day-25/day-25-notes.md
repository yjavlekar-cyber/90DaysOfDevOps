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


## Task 4: Branching Strategies
### 1.GitFlow
#### How it works
    Under this branching flow devlopers create a feature branch from main branch and delay merging back to the main branch until feature is finally finished.
    
    In this with main branch there is another branch called devlop. main is basically the official release branch and devlop branch is the branch which will act
    as intermidiatery between feature branch and main branch.
    Once the features are done we can push those onto a devlop branch and from their we can push it to a new branch called "Release".
    Using a dedicated branch to prepare releases makes it possible for one team to polish the current release while another team continues working on features for the next release.

    Also there is an other branch called "Hotfix" which directly communicates with the main branch for bugfixes.

| Workflow Component | Gitflow Strategy |
| :--- | :--- |
| **Main Branch** | Production releases only. |
| **Develop Branch** | Main "hub" for integration. |
| **Feature Branch** | Private workspace for new code. |
| **Release Branch** | Final QA / Buffer before Production. |
| **Hotfix Branch** | Fast-track for production bugs. |


#### When/where it's used
     * Scheduled Release Cycles: Best for projects that release on a fixed schedule (e.g., every 2 weeks or monthly) rather than continuously.
     * Mobile App Development: Ideal for iOS/Android apps where releases must be "frozen" for App Store review while new development continues.
     * Large-Scale Enterprise Projects: Used when multiple teams are working on different features simultaneously and need a stable develop branch to integrate their work.
     * Strict QA Requirements: Perfect when a dedicated "Release" phase is needed for final bug hunting and polishing without stopping new feature development.
     * Legacy Software: When maintaining older versions is necessary, as Gitflow makes tracking versions (tags) very clear.

#### Pros and cons
- PROS
      - devlopment continues parallaly.
      - Highly structured.
      - Great for scheduled releases
      - Stability as the main branch is secluded only used to merge releases and hotfixes.
- CONS
      - Structure can be complex sometimes.
      - Can slow down small projects as this does not support continous delivery.
      - Merge conflicts
  
