---
sidebar_position: 2
sidebar_label: Github
sidebar_class_name: green
---
# Github

## Link to Github

### Use ssh

ssh is the way i mostly use.

#### Step1 : generation ssh

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

#### Step2 : add the ssh key to github 

In the setting -> ssh

#### Step3 : test the ssh connection

```sh
ssh -T git@github.com
```

if show the following words, it success.

```txt
Hi XXX! You've successfully authenticated, but GitHub does not provide shell access.
```

## Pull from Github

### Git fetch

fetch gets all the change history of a tracked branch/repo.

```sh
git fetch master
```

That looks as expected, but we can also verify by showing the differences between our local master and origin/master:

```sh
git diff origin/master
diff --git a/README.md b/README.md
index 23a0122..a980c39 100644
--- a/README.md
+++ b/README.md
@@ -2,6 +2,4 @@
 Hello World repository for Git tutorial
 This is an example repository for the Git tutoial on https://www.w3schools.com

-This repository is built step by step in the tutorial.

-It now includes steps for GitHub
+This repository is built step by step in the tutorial.
\ No newline at end of file
```

Then we can merge the head

### Git Pull

pull is a combination of fetch and merge. It is used to pull all changes from a remote repository into the branch you are working on.

## Push to Github

```sh
git push origin [remote]
```

if we have tracking branch , we don't need add remote

## Remote branch

remote branch is used to track the branch from the Github


we should use following command to checkout:

```sh
git branch -a
```

> `git branch -r` is for remote branch only

### Pull a branch from Github

```sh
git pull
```

pull all the branch of Github, then we observe the branches.

```sh
git branch -a
* master
  remotes/origin/html-skeleton
  remotes/origin/master
```

## Tracking branch

tracking branch :

- remote tracking branch -- 远程分支的副本
- local tracking branch -- 本地索引：索引的是 remote tracking branch --- 有了这个分支可以直接 pull 或 Push

![img](https://s2.loli.net/2022/12/20/Oq9mXNGIPEJKwaY.png)

```sh
#使用git branch -vv可以看看更多信息 -r查看远程分支
#git branch -vv
  feature        efdab37 f1
* feature-remote a9e2063 [origin/feature-remote] file3
  master         32a4a45 [origin/master] m2
```

> note : two tracking branch the same name

### Create local tracking branch

local tracking branch is useful, we can use following command to make a branch to track remote tracking branch

```sh
#git branch --track feature-remote-local origin/feature-remote
branch 'feature-remote-local' set up to track 'origin/feature-remote'.
#git branch --set-upstram-to=origin/feature-remote
#这个也可以
```
