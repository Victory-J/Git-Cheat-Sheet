# git cheatsheet

## What's git?
git is a version control manager made by [the guy](https://en.wikipedia.org/wiki/Linus_Torvalds) who made linux. It consists of a (often remote) repository that keeps track of all the changes you've made to your source code, and the local client(s) that push changes to this repo.

GitHub is an online service that lets you host your git repos at free/minimal cost. It also lets you host informative gists like this one.

## Setup
~~~bash
$ git clone <repo.git>               # clones the repo from a url
$ git remote -v                      # shows the url of the repo
$ git branch                         # view all local branches (including current)
$ git status                         # gives you current status on the working directory & branch

# starting from scratch
$ git init                           # adds a new git to the current folder
$ git remote add origin <link.git>   # registers a new remote repository at the url
~~~

## Making Changes
In git, the changes you make to any files first need to be added (staged) to a commit before you can push them to the repo.

~~~bash
$ git add <file>              # stages changes to a file to the next commit
$ git add .                   # stages all changed files in the working directory
                              # to the next commit (use with care)
                              
$ git commit -m "description" # adds a commit with changes to the code, waiting to be pushed
$ git push                    # pushes all pending local commits in the current branch to the repo
~~~

## Working with Branches

~~~bash
$ git branch -r                  # view all remote branches
# Example output:
# origin/HEAD -> origin/master
# origin/master
# origin/signup

$ git branch <new-branch>        # create a new local branch
$ git checkout <branch>          # switch to a different local branch
$ git checkout -b <new-branch>   # shorthand for doing the previous two steps at the same time

$ git checkout -b <repo-branch>  # creates and switches to a local copy of a
                                 # remote branch (only if name matches repo branch)
# e.g. git checkout -b signup (matches origin/signup)

$ git branch -d <branch>         # delete a local branch

$ git merge <other-branch>       # applies all committed changes from <other-branch> to the current branch, 
                                 # reconciling the current branch's commits
$ git rebase <other-branch>      # applies all commits from <other-branch> one by one to the current branch,
                                 # rewriting all the current branch's commits when it is done
                                 
# Note: only use rebase if you have local commits pending. do NOT rebase if you have commits in your
# current branch that have been pushed to the repo already!
~~~

For more details, check out [this link on branches & basic merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) and [this link on rebasing.](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)

## Grabbing Changes

~~~bash
$ git fetch origin           # downloads information on remote branches, without applying any changes
$ git merge origin/<branch>  # applies all commited changes from downloaded remote <branch> to current branch
$ git pull origin <branch>   # shorthand for doing the previous two steps at the same time
# Note: the slashes matter here
~~~

For more details, check out [this link.](https://longair.net/blog/2009/04/16/git-fetch-and-merge/)

## In Case of Emergency, Break Glass

~~~bash
# these will make you lose changes
$ git reset --hard HEAD          # resets all uncommitted changes
$ git reset --hard origin/master # resets branch back to origin/master

# these are useful if you try to pull from another branch and there is a conflict
$ git stash                      # saves all local uncommitted changes, staged or unstaged
$ git stash apply                # brings all the stashed changes back

# you can always check the status of your current staged/unstaged commits with:
$ git status
~~~