---
title: git
categories:
  - git
tags:
  - git
toc: true
---

# git

## local

### ? undo

* revert: remain in history, to target any one individual commit
* checkout: HEAD no longer points to a branch—it points directly to a commit

  git checkout a1e8fb5  
    Nothing you do in here will be saved in your repository

  git checkout master  
    get back to the “current” state of your project

* reset: only work backward from the current commit
* clean: for undoing changes to the working directory

Once changes have been committed they are generally permanent Use git checkout to move around and review the commit history git revert is the best tool for undoing shared public changes git reset is best used for undoing local private changes

### commit

* amend commit: update current commit, not create new
* sign-off commit: add by who

### delete commit

If it is the last commit this is very straight forward. Simply run: git reset HEAD

* rebase:  allow you to remove one or more consecutive commits

  `git rebase --onto` ~ ~ 

  ex\) git rebase --onto repair~3 repair~1 repair    

* cherry-pick:  allows you to remove non consecutive commits.

```text
init .
add
commit -am
log
```

#### ? remove commits in the middle

### tag -- log

branches=\* : in all branch

### branch

* `-a`: list all branch
* create: git branch branch-name
* switch: git checkout branch-name
* Merge your branch and delete\(from master\): git checkout master , git merge branch-name, git branch -d branch-name

  Created a branch and checked it out Made a change in the new branch Committed the change to the new branch Integrated that change back into the main branch Deleted the branch you are no longer using.

  master, origin/master merge from master delete

### ? merge branch

merge from master

conflict to see 'diff'

### ? patch

* create
* apply

### ? delete file from repository

## remote

