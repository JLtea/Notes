# Git Utilities and Commands

```
git add -A // add local changes

git commit -m "<message here>" // commit local changes

git push origin <branch name> // push commit to git branch
```

`git fetch` is updating local branches with the most recent changes on git

`git pull` is overwriting the current local branch with the changes that were fetched

### Useful Tools

```
git checkout -b <new branch name> // creating a new local branch
git checkout <existing branch name> // checking out an existing git branch
```

**Rebase**: changing git commit history by _pick_ and _squash_

```
git rebase -i HEAD~<number of commits from head>

// Usually want to force push afterwards
git push --force origin <branch name> //WARNING: Will overwrite existing branch
```

```
git pull --rebase
```

**Cherry-Picking**: picking one commit from a branch

```
git cherry-pick <commit goes here>
```

Rewrite Commit History:

```
git filter-branch -f --env-filter \
"GIT_AUTHOR_NAME='Joseph Lee'; GIT_AUTHOR_EMAIL='tlee95@illinois.edu'; \
GIT_COMMITTER_NAME='Joseph Lee'; GIT_COMMITTER_EMAIL='tlee95@illinois.edu';" HEAD
```
