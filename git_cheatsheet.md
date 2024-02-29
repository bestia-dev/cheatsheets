# Git cheatsheet


## GitHub Flow for Issues, Branches and Pull Requests

Create a GitHub issue  
On the issue right bottom: Development - Create a branch. Let's say the name is `branch_1`.  
GitHub will show the incantation to checkout locally. Great.  
So I don't have to play with VSCode UI.  

It is recommanded to set this `branch_1` as the default branch on GitHub in the Code tab.  
So to not have problems if we modify anything in GitHub, we want it to go to this "active default" branch.  

![image](https://github.com/bestia-dev/cheatsheets/assets/31509965/c6e261cf-31fd-40e3-bf7b-9886ceccb74e)

work locally on `branch_1`  
add many commits and pushes on `branch_1`  

When the last commit is done in Github there will be a big button to Compare and Pull Request.  

![image](https://github.com/bestia-dev/cheatsheets/assets/31509965/6847999c-3c4d-43da-8b54-ecbee7b537ec)

Do the Code review and write some comments.  
Merge Squash to main to have all the file changes in one single commit for simplicity.  
In GitHub (on the remote), Delete the branch.  

## How to delete the branch locally after GitHub delete branch?  

```bash
# fetch all the changes from the remote  
git fetch --all --prune  
# if we are not on branch_1, checkout the local branch  
git branch checkout branch_1  
# pull all the changes to this branch  
git pull  
# go to the main branch
git branch checkout main
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
