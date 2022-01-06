o# Git commands
#concept
**Related:**
-  

---

## Some basics
- `git reset --hard ORIG_HEAD`: Revert your repo to last committed state just before the merge.  
- `git reset --hard HEAD  `: Revert your repo to last committed state.  
- `git checkout [commit] -- [file]`: Restore a file, or if omitted the whole repo, to its state at commit. Can be used to recover files that were previously deleted using git rm.  
- `git revert commit`: Reverts the changes introduced by commit. If that commit was the result of a merge, effectively undoes the merge, and leaves the current branch in the state it was in before the merge. Git tries to back out just the changes introduced by that commit without disturbing other changes since that commit, but if the commit happened a long time ago, manual conflict resolution may be required.
- `git push [upstream] [branch]`: Push branch to upstream


## Push to Remote
- git pull
- git merge
- git push 
- Create pull request

## To see who changes which files when
- `git blame [file]`: Annotate each line of a file to show who changed it last and when.
- `git diff [file]`: Show differences between current working version of file and last committed  
version.  
- `git diff [branch] [file]`: Show differences between current version of file and the way it appears in the most recent commit on branch (see Section 10.2).  
- `git log [ref ..ref] [files]`: Show log entries affecting all files between the two commits specified by the refs (which must be separated by exactly two dots), or if omitted, entire log history affecting those files.  
- `git log --since="[date]" [files]`: Show the log entries apffecting all files since the given date (examples: "25-Dec-2019", "2 weeks ago"

## Ways to refer to commits
- `HEAD`: The most recently committed version on the current branch. 
- `HEAD∼`: The prior commit on the current branch (HEAD∼$n$ refers to the $n$th previous commit).  
- `ORIG_HEAD`: When a merge is performed, HEAD is updated to the newly-merged version, and ORIG_HEAD refers to the commit state before the merge. Useful if you want to use git diff to see how each file changed as a result of the merge.  
- `1dfb2c∼2`: 2 commits prior to the commit whose ID has 1dfb2c as a unique prefix.  
- `"[branch]@{[date]}"`: The last commit prior to date (see Figure 10.7 for date format) on branch, where HEAD refers to the current branch

## Branches
Feature branches: make changes until changes are complete and tested
Release branches: each branch is substantially different, often used with non-SaaS

## Changing History
### Rebasing
Rebasing: going through and changing git history
- Can be used to help resolve merge conflicts. Git should say if there will be a conflict caused by merging, you can fix it by rebasing the branch you're merging on onto current. This applies each change from that branch to yours and then tries to apply your change, if there is a conflict you change them one-by-one
- You can only do this in 3 cases:
	1. You haven't ever pushed the branch
	2. You've pushed the branch but no one has made changes based on your branch so changing the history won't be problematic
	3. Otherwise anyone else who has made changes based off of the branch will be out of sync

Instead of rebasing, you can also just merge to resolve conflicts but this will create a lot of merge commits

### Reflog
Use `git reflog` to see a history of git commands that have been executed. To undo one, I think do `checkout [that reflog identifier]` 