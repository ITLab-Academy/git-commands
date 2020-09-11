# Git Commands

## Table of Contents

1. [Tips And Tricks](#tips-and-tricks)
1. [Getting and Creating Projects](#getting-and-creating-projects)
    1. [Clone](#clone)
1. [Basic Snapshotting](#basic-snapshotting)
    1. [Diff](#diff)
    1. [Commit](#commit)
    1. [Restore](#restore)
    1. [Reset](#reset)
    1. [Mv](#mv)
1. [Branching and Merging](#branching-and-merging)
    1. [Branch](#branch)
    1. [Checkout](#checkout)
    1. [Tag](#tag)
1. [Sharing and Updating Projects](#sharing-and-updating-projects)
    1. [Push](#push)
    1. [Remote](#remote)
1. [Inspection and Comparison](#inspection-and-comparison)
    1. [Show](#show)
1. [Patching](#patching)
    1. [Cherry-Pick](#cherry-pick)
    1. [Revert](#revert)
1. [Plumbing Commands](#plumbing-commands)
    1. [Update-Index](#update-index)


## Tips and Tricks

### Deleting local and remote branches

```bash
git push <remotename> --delete <branchname> | git branch <branchname> -d
```

### Deleting local branches that have been merged

merged into HEAD
```bash
git branch --merged | grep -v '\\*\\|master\\|homolog' | xargs -n 1 git branch -d
```

merged into origin/master
```bash
git branch --merged origin/master | grep -v '\\*\\|master\\|homolog' | xargs -n 1 git branch -d
```

> See [how to delete remote branch](#deleting-remote-branch) and [how to delete local branch](#deleting-local-branch)

### Getting file from another branch

#### Using checkout command

```bash
# adding to staging
git checkout <branchname> --<file>
```

> See [more details about getting a file using resto command](#getting-file-from-another-branch-using-checkout)

#### Using restore command

```bash
# adding to staging
git restore -s <branchname> --<file>
```

> See [more details about getting a file using restore command](#getting-file-from-another-branch-using-restore)


#### Using show command

```bash
# creating a file
git show -<branchname>:<file> > <file>
```

### Rollback and fix a publication

In this example we just published the v.2 tag with a bug. First we need to revert our app to v.1 version

```bash
git revert v.1..v.2 --no-commit
```

Now we create a new commit with this revert

```bash
git commit -m "reverting v.2 publish"
```

> See [Reverting a group of commits using tags](#reverting-a-group-of-commits-using-tags) and [Reverting a group of with one commit](#reverting-a-group-of-with-one-commit)


Checkout the tag with the bug

``` bash
git checkout v.2
```

> See [Creating branch from a tag](#creating-branch-from-a-tag)

Create a branch to fix the bug

```bash
git checkout -b hotfix/v.2
```

> See [Checkout creating a new branch](#checkout-creating-a-new-branch)

Fix the bug, add, commit, push and merge to master. Create new tag (v.2.1), publish and be happy :)

### Show all aliases

```bash
git config --get-regexp alias
```

[Back to top](#table-of-contents)

### Change local user info

That is the way to change your local repo user info

```bash
git config user.email <youremail>
```

```bash
git config user.name <name>
```

[Back to top](#table-of-contents)

## Getting and Creating Projects

### Clone

#### Cloning a specific branch

```bash
git clone -b <branchname> --single-branch <repourl>
```

[Back to top](#table-of-contents)

## Basic Snapshotting

### Diff 

#### Compare file from two different branches

```bash
gid diff <branchname1> <branchname2> -- <filename>
```

[Back to top](#table-of-contents)

### Restore

#### Getting file from another branch using restore

```bash
git restore -s <branchname> --<file>
```

> This way the file will be added in the staging

[Back to top](#table-of-contents)

### Commit

#### Editing last commit

```bash
git commit --amend
```

#### Edit last commit without edit message

```bash
git commit --amend --no-edit
```

[Back to top](#table-of-contents)

### Reset

#### Undo last commit and bring changes back into Snapshotting

```bash
git reset --soft
```

#### Undo last commit and destroy all changes

```bash
git reset --hard
```

[Back to top](#table-of-contents)

### MV

#### Rename a file in a case-sensitive way

```bash
git mv <oldfilename> <Newfilename>
```

[Back to top](#table-of-contents)

## Branching and Merging

### Branch

#### Creating branches

> See [how create a branch using checkout command](#checkout-creating-a-new-branch)

#### Listing branches

##### Simple List branches
```bash
git branch
```
##### List remote branches
```bash
git branch --remote
```

#### Deleting Branches

##### Deleting local branch

```bash
git branch -d <branchname>
```

> See [how delete a remote branch](#deleting-remote-branch)

[Back to top](#table-of-contents)
### Checkout

#### Simple checkout

```bash
git checkout <branchname>
```

#### Checkout to last branch

```bash
git checkout -
```

#### Checkout creating a new branch

```bash
git checkout -b <branchname>
```

#### Creating branch from a tag
```bash
git checkout tags/<tagname>
git checkout -b <branchname>
```

#### Checkout a remote branch

```bash
git checkout --track <remotename>/<branchname>
```

#### Discarding files not staged

```bash
git checkout -- <filepath>
```

### Discarding all files not staged

```bash
git checkout -- .
```

> Be careful with this option, you will lose all changes!

#### Getting file from another branch using checkout

```bash
git checkout <branchname> --<file>
```

> This way the file will be added in the staging

[Back to top](#table-of-contents)

### Tag

#### Creating tags

##### New Tag

```bash
git tag <tagname>
```
##### New tag with annotated and comments

```bash
git tag -a v1.4 -m "my version 1.4"
```

> See [how to create a branch from a tag](#creating-branch-from-a-tag)

#### List tags

```bash
git tag
```

[Back to top](#table-of-contents)

## Sharing and Updating Projects

### Push 

#### Pushing remote branch

```bash
git push
```

#### Pushing remote forcing your local branch version

```bash
git push --force
```

> Prefer [--force-with-lease option](#pushing-remote-with-forcing-prevent-remote-throw-someone-elses-work) over --force

#### Pushing remote with forcing prevent remote throw someone else's work
```bash
git push --force-with-lease
```

#### Deleting remote branch

```bash
git push <remotename> --delete <branchname>
```

#### Pushing tags

```
git push --tags
```

[Back to top](#table-of-contents)

### Remote

#### Delete local branches that no longer exists in the remote repo

```bash
git remote prune origin
```
Use the --dry-run flag to only see what branches will be pruned, but not actually prune them:

``` bash
git remote prune origin --dry-run
```

[Back to top](#table-of-contents)
## Inspection and Comparison

### Show

#### Getting file from another branch using show

```bash
git show -<branchname>:<file> > <file>
```

> This way will be created a new file in your branch

[Back to top](#table-of-contents)

## Patching

### Revert

Revert commits without lost commits history

#### Reverting last commit

```bash
git revert HEAD
```

#### Reverting a group of commits

```bash
git revert <oldestcommittarget>..<lastcommit>
```

> All commits bettwen oldestcommittarget and lastcommit will be reverted

#### Reverting a group of commits using HEAD shortcut

```bash
git revert HEAD~2..HEAD
```

#### Reverting a group of commits using tags

```bash
git revert v.2..v.3
```

> All commits between v.2 and v.3 tags will be reverted

#### Reverting a group of commits with one commit

```bash
git revert v.2..v.3 --no-commit
```

> All commits between v.2 and v.3 tags will be reverted and added to staged so you can commit all changes as one commit.


[Back to top](#table-of-contents)

### Cherry-Pick

#### Copy a specific commit to your current branch

```bash
git cherry-pick <commithash>
```


[Back to top](#table-of-contents)


## Plumbing Commands

## Update-index

### Modify files managed by Git locally (or updated automatically) but you do not want Git to manage that change

```bash
git update-index --skip-worktree <file>
```

to restore file use:

```bash
git update-index --no-skip-worktree <file>

```

[Back to top](#table-of-contents)