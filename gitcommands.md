# Git Commands

## Table of Contents

1. [Tips And Tricks](#tips-and-tricks)
1. [Basic Snapshotting](#basic-snapshotting)
    1. [Commit](#commit)
    1. [Reset](#reset)
1. [Branching and Merging](#branching-and-merging)
    1. [Branch](#branch)
    1. [Checkout](#checkout)
    1. [Tag](#tag)
1. [Sharing and Updating Projects](#sharing-and-updating-projects)
    1. [Push](#push)
    1. [Remote](#remote)

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

[Back to top](#table-of-contents)
## Basic Snapshotting

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