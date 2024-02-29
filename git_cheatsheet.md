# Git cheatsheet


## GitHub Flow for Issues, Branches and Pull Requests

Create a GitHub issue  
On the issue right bottom: Development - Create a branch. Let's say the name is `branch_1`.  
GitHub will show the incantation to checkout locally. Great.  
So I don't have to play with VSCode UI.  

It is recommanded to set this `branch_1` as the default branch on GitHub in the Code tab.  
So to not have problems if we modify anything in GitHub, we want it to go to this "active default" branch.  

![github_default_branch](https://raw.githubusercontent.com/bestia-dev/cheatsheets/main/images/github_default_branch.png)

work locally on `branch_1`  
add many commits and pushes on `branch_1`  

When the last commit is done in Github there will be a big button to Compare and Pull Request.  

![github_compare_and_pull_request](https://raw.githubusercontent.com/bestia-dev/cheatsheets/main/images/github_compare_and_pull_request.png)

Do the Code review and write some comments.  
Merge Squash to main to have all the file changes in one single commit for simplicity.  

## Before you delete the GitHub remote branch

You have to pull locally what changed on the remote:
```bash 
# if we are not on branch_1, checkout the local branch  
git branch checkout branch_1  
# pull all the changes to this branch  
git pull  
```

Now you can delete the remote branch_1 on GitHub using the big button.

## After you delete the GitHub remote branch

```bash
# fetch all the changes from the remote  
git fetch --all --prune  
# go to the main branch
git checkout main
# pull all the changes to main branch
git pull
# list the branches with tracking remote names
# you will see the "gone" word to signal the remote branch is deleted
git branch -vv
$   branch_1 [origin/branch_1: gone] last commit_message
$ * main   9 [origin/main: behind 1] last_commit_mes
# Now we can finally delete the branch
git branch --delete branch_1
# all done. Just 7 commands. Why is that not more simple?
```

## Add a git tag to a commit with the commit's date

```bash
- find SHA with this
git log --pretty=format:"%h %aI %s"

git checkout 1eaa39c
GIT_COMMITTER_DATE="$(git show --format=%aD | head -1)" \
git tag -a 2022-07-19 1eaa39c -m "vscode-1.69.1  typescript-4.7.4"

git push origin --tags
git checkout main
```
