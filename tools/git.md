---
layout: default
title: Git
parent: Tools
---

# Git

## Command snippets

### Common commands

```bash
git checkout <branch>  # change branch

git status      # list all changes

git add <file>  # add file to commit
git checkout .  # revert changes for files not added
git clean -f    # remove untracked files

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