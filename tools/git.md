# Git

## Command snippets

### Common commands

```bash
git checkout <branch>  # change branch

git branch      # see all local branches
git branch -r   # see all remote branches
git branch -a   # see all branches

git status      # list all changes

git add <file>  # add file to commit
git checkout .  # revert changes for files not added
git clean -fdx  # remove untracked files
                #   -f force
                #   -d remove whole directories
                #   -x remove ignored files too

git log origin/<branch>..<local-branch>  # list all unpushed commits
```

### Push up through a given commit

```bash
git push origin <commit-sha>:<remote-branch-name>
```

### Reordering commits

```bash
# Will open an editable file 3 commits back, oldest commit first
git rebase -i HEAD~3
```