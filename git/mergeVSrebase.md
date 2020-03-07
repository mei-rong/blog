# Merge vs Rebase
[Reference URL](https://medium.com/datadriveninvestor/git-rebase-vs-merge-cc5199edd77c)

Git has 2 ways to integrate changes in diffferent branches: merge/rebase

Merge will result as a **combination** of commits

Rebase will add all the changes in feature branch starting **from the last commit** of the master branch

![](https://mei-rong.github.io/notes/images/mergeVSrebaseGraph.png)


Merging adds **one more commit** to your history
![](https://mei-rong.github.io/notes/images/mergeVSrebaseLog.png)

## When to rebase? When to Merge?

For a **shared** feature branch where you are getting changes from, the rebasing process will create inconsistent repositories.

For **individuals**, rebasing can simplify you commit history.

## How to use

merge **from other branch to the current**
> git merge {some branch}

rebase from other branch to the current
> git rebase {some branch}

## Change commit history
### To edit the lastest 5 commit history
> git rebase -i HEAD~5
### To edit the commit after some one
> git log(find the commit id)  
> git rebase -i {commit id}  
> **Change "pick" to "f" (drop the commit meaasge) if you don't want them in the log**  
> **change "pick" to "r" if you want to change the message**  
Save and push
