# [Pro Git](https://git-scm.com/book/en/v2) notes

## 1. Getting Started

Git checksums each file/directory (SHA-1 hash), based on the contents of a file or directory structure in Git. 

Files in git can reside in three main states: committed, modified, and staged. Committed means the data is safely stored in your local db. Modified means you have changes the file but not committed it yet to your database. Staged means you have marked a modified file to go into your next commit

Staging area is a file, generally in the Git directory, that stores info about what will go into your next commit (sometimes called an index).

Help:  

```
$ git help <verb>
$ git <verb> --help  
$ man git-<verb>  
```

## 2. Git Basics

Git stages a file exactly as it is when you run the `git add` command. If you modify a file after you run `git add`, you have to run `git add` again to stage the latest version of the file.

`git status -s` to get a far more simplified output from the command.

`git diff` compares what is in your working directory and with what is in your staging area. I.e. changes you've made that you haven't yet staged.

`git diff --staged` compares your staged changes to your last commit

`git rm` removes file from tracked files, stages file's remove and removes it from the working directory

`git rm --cached` keep file on disk but not have Git track it anymore

`git mv file_from file_to` renames a file in Git

`git log -p -2` prints log limited to the last 2 commits with diffs included

`git log --oneline --graph` shows branch and merge history

`git log -Sfunction_name` shows commits adding or removing code matching the string

### Undoing things

`git commit --amend` allows you to add files to the current commit or edit the message of your previous commit

### Working with Remotes

`git remote -v` shows the URLs that git has stored for the shortname used to read/write to that remote 

`git remote show [remote-name]` shows which remote branches on the server you don't have yet, which remote branches have been removed from the server

`git fetch [remote-name]` goes out and pulls down all data from that remote that you don't have yet, you should have references to all the branches from that remote, also

### Tagging

Two types of tags, lightweight and annotated. Lightweight is simply a pointer to a specific commit. Annotated tags are stored as full objects in the Git db - they're checksummed; contain tagger name, email, and date; have a tagging message; and can be signed with GPG.

`git tag -a v1.2 9fceb02` tags a commit after you've made it

Tags aren't pushed to remote servers by default, use `git push origin [tagname]` to do so.

##### Annotated Tags

`git tag -a v1.4 -m "my version 1.4"`  

```
$ git show v1.4
tag v1.4
Tagger: Ben Straub <ben@straub.cc>
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number
```

##### Lightweight Tags

To create a lightweight tag, simply don't supply the `-a`, `-s`, `-m` options

`git tag v1.4-lw`  


## 3. Git Branching

When you make a commit, Git stores a commit object that contains a pointer to the snapshot of the content you staged. This object also contains the author’s name and email, the message that you typed, and pointers to the commit or commits that directly came before this commit (its parent or parents): zero parents for the initial commit, one parent for a normal commit, and multiple parents for a commit that results from a merge of two or more branches.

Staging files checksums each one (SHA-1 hash) and stores that version of the file in the Git repository (referred to as blobs), and adds that checksum to the staging area. 

Git also checksums each subdirectory, and stores those tree objects in the Git repository. Then Git creats a commit object that has a pointer to the root project tree so it can re-create that snapshot when needed. 

![commit and its tree](https://git-scm.com/book/en/v2/book/03-git-branching/images/commit-and-tree.png)

Commits store pointers to the commit that came immediately before it.

A branch in Git is simply a lightweight movable pointer to one of these commits. Creating a new branch simply creates a new pointer for you to move around. 

A special pointer called `HEAD` keeps track of what branch you're currently on. 

`git checkout [branch-name]` moves `HEAD` to the specified branch name. 

The `HEAD` branch moves forward as commits are made

`git log --oneline --decorate --graph --all` will print out the history of your commits, showing where your branch pointers are and how your history has diverged

A branch in Git is in actuality a simple file that contains the 40 character SHA-1 checksum of the commit it points to

### Basic Branching and Merging

Three way merge, uses the two snapshots pointed to by the branch tips and the common ancestor of the two. Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that points to it (merge commit). Special in that it has more than one parent. 

![Three-way merge](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-merging-1.png)

When merge conflicts occur, git pauses the process while you resolve the conflict. Git add conflict resolution markers to files that have commits.

### Branch Management

`--merged` and `--no-merged` options filter the `git branch` list to branches that you have or haven't already merged into the branch you're on

### Remote Branches

Remote references are references (pointers) in your remote repositories, including branches, tags, and so on. You can get a full list of remote references explicitly with `git ls-remote [remote]`

Remote-tracking branches are references to the state of remote branches.They’re local references that you can’t move; they’re moved automatically for you whenever you do any network communication. Essentially bookmakrs to remind you where the branches in your remote repositories were the last time you connected to them. 

They take the form `(remote)/(branch)`

`git fetch origin` fetches any data from the server you don't yet have, updates your local database, and moves your `origin/master` pointer to its new, up-to-date position.

##### Pushing

`$ git push origin serverfix` is actually expanded to: `refs/heads/serverfix:refs/heads/serverfix` or `git push origin serverfix:serverfix`, which means 'take my serverfix and make it the remote's serverfix. 

It’s important to note that when you do a fetch that brings down new remote-tracking branches, you don’t automatically have local, editable copies of them. If you want your own serverfix branch that you can work on, you can base it off your remote-tracking branch:

`$ git checkout -b [branch] [remotename]/[branch]`

shortcut: `git checkout --track origin/serverfix`

##### Tracking Branches

Tracking branches are local branches that have a direct relationship to a remote branch. They're automatically created when checking out a local branch from a remote-tracking branch. 

If you're on a tracking branch and `git pull`, Git automatically knows which server to fetch from and branch to merge into.

If the branch you're trying to checkout doesn't exist locally, and is unique in your remotes, Git will create a tracking branch for you

`git checkout serverfix`

If you already have a local branch and want to set it to a remote branch, use `-u` or `--set-upstream-to` with `git branch`. 

To view tracking branches set up: `git branch -vv`

##### Deleting Remote Branches

`git push origin --delete serverfix`

This simply removes the pointer from the server. 

### Rebasing

In Git, there are two main ways to integrate changes from one branch into another: the merge and the rebase. With the `rebase` command, you can take all the changes you committed on one branch and replay them on another one.

It works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn.

![Divergent history](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-1.png)

```
$ git checkout experiment
$ git rebase master
```

![Rebasing experiment](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-3.png)

```
$ git checkout master
$ git merge experiment
```

![Fast-forwarding the master branch](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-4.png)

There is no difference in the end product of the integration, but rebasing makes for a cleaner history. If you examine the log of a rebased branch, it looks like a linear history: it appears that all the work happened in series, even when it originally happened in parallel. Rebasing replays changes from one line of work onto another in the order they were introduced, whereas merging takes the endpoints and merges them together.

##### More Interesting Rebases

`$ git rebase --onto master server client`

![](https://git-scm.com/book/en/v2/book/03-git-branching/images/interesting-rebase-2.png)

You can rebase the server branch onto the master branch without having to check it out first by running `git rebase [basebranch] [topicbranch]`

##### The Perils of Rebasing

_Do not rebase commits that exist outside your repository._

When you rebase stuff, you’re abandoning existing commits and creating new ones that are similar but different. If you push commits somewhere and others pull them down and base work on them, and then you rewrite those commits with git rebase and push them up again, your collaborators will have to re-merge their work and things will get messy when you try to pull their work back into yours.

In general the way to get the best of both worlds is to rebase local changes you’ve made but haven’t shared yet before you push them in order to clean up your story, but never rebase anything you’ve pushed somewhere.

## 5. Distributed Git

`git diff --check` to check for whitespace issues

If some changes only modify the same file, try to use `git add --patch` to partially stage files