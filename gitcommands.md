# Git Commands

## My Custom Commands

### Deleting local and remote branches

```bash
git push <remotename> --delete <branchname> | git branch <branchname> -d
```

> See [how to delete remote branch](#deleting-remote-branch) and [how to delete local branch](#deleting-local-branch)

## Basic Snapshotting

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

#### Checkout

##### Simple checkout

```bash
git checkout <branchname>
```

##### Checkout to last branch

```bash
git checkout -
```

##### Checkout creating a new branch

```bash
git checkout -b <branchname>
```

##### Creating branch from a tag
```bash
git checkout tags/<tagname>
git checkout -b <branchname>
```

##### Checkout a remote branch

```bash
git checkout --track <remotename>/<branchname>
```

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

## Sharing and Updating Projects

### Push 

#### Deleting remote branch

```bash
git push <remotename> --delete <branchname>
```

#### Pushing tags

```
git push --tags
```