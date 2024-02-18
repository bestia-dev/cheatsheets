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
