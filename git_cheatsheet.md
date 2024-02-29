# Git cheatsheet

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

## Branch deleted on GitHub

Using GitHub Pull Request, I can delete the remote branch after merging.
But the local git knows nothing about it.

```bash
# First fetch prune, so the local git knows, that a remote branch is deleted
git fetch --prune

# The local branch still exists, but the "tracking branch" is "gone". Mark the word "gone".
git branch -vv
  branch_1 [origin/branch_1: gone] last commit_message
* main   9 [origin/main: behind 1] last_commit_message

# If you know what you are doing, delete the local branch
git branch --delete branch_1
```

