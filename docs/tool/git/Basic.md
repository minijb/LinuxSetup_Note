---
sidebar_position: 1
sidebar_label: Basic
sidebar_class_name: green
---

# Git

<!--toc:start-->

- [Git](#git)
  - [Configure git](#configure-git)
  - [Check the status of current project](#check-the-status-of-current-project)
  - [Four environment](#four-environment)
  - [Stage file](#stage-file)
  - [Commit](#commit)
    - [Commit without stage](#commit-without-stage)
  - [Branch](#branch)
  - [Git branch merge](#git-branch-merge)
    - [Merge Conflict](#merge-conflict)
  - [Git stash](#git-stash)
    - [Pop the stash](#pop-the-stash)
    - [暂存未跟踪或忽略的文件](#暂存未跟踪或忽略的文件)
  - [Tag](#tag)
  - [.gitignore](#gitignore)
  <!--toc:end-->

## Configure git

This is important for version control systems, as each Git commit uses this information:

```sh
git config --global user.name xxxx
git config --global user.email xxx
```

> **Note**: use `global` to set username and email for every repository

## Check the status of current project

when we add new file or we want to know the changes of current project, we can use the following Commands

```sh
git status
```

outputs:

```sh
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        docs/
        mkdocs.yml

nothing added to commit but untracked files present (use "git add" to track)
```

it will show what we need to do.

## Four environment

**working environment** : where we code.

**staging environment** : whenever you hit a milestone or finish a part of the work, you should add the files to a Staging Environment.
Staged files are files that are ready to be committed to the repository you are working on.

**repository environment** : where store the different version of code

**stash** : stage the code templately

## Stage file

stage one file :

```sh
git add {filename}
```

stage more than one file :

```sh
git add .
```

now the status:

```sh
git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached ..." to unstage)
        new file:   README.md
        new file:   bluestyle.css
        new file:   index.html
```

## Commit

always include a message

```sh
git commit -m "First release of Hello World!"
```

### Commit without stage

```sh
git commit -a -m "Updated index.html with a new line"
```

## Branch

a branch is a new/separate version of the main repository.

**create a branch**:

```sh
git branch {branch_name}
```

**list branches**:

```sh
git branch
```

**change current branch**:

```sh
git switch {branch_name}
```

**delete branch**:

```sh
git branch -D {name}
```

## Git branch merge

merge: make another branch into current branch

```sh
# current is master
git merge {another branch}
```

### Merge Conflict

如果合并的分支有冲突，会自动生成一个commit，我们在处理完冲突之后继续进行commit就可以了。

```sh
git checkout master
git merge hello-world-images
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

冲突地区下所示

```html
<!doctype html>
<html>
  <head>
    <title>Hello World!</title>
    <link rel="stylesheet" href="bluestyle.css" />
  </head>
  <body>
    <h1>Hello world!</h1>
    <div>
      <img
        src="img_hello_world.jpg"
        alt="Hello World from Space"
        style="width:100%;max-width:960px"
      />
    </div>
    <p>This is the first file in my new Git Repo.</p>
    <<<<<<< HEAD
    <p>This line is here to show how merging works.</p>
    =======
    <p>A new line in our file!</p>
    <div>
      <img
        src="img_hello_git.jpg"
        alt="Hello Git"
        style="width:100%;max-width:640px"
      />
    </div>
    >>>>>>> hello-world-images
  </body>
</html>
```

After checking, we can stage and commit. Then delete the merged branch.

## Git stash

有时，当你在项目的一部分上已经工作一段时间后，所有东西都进入了混乱的状态， 而这时你想要切换到另一个分支做一点别的事情。 问题是，你不想仅仅因为过会儿回到这一点而为做了一半的工作创建一次提交。 针对这个问题的答案是 git stash 命令。

简单来说就是将项目的状态保存在一个栈上。

```sh
$ git status
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   index.html

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   lib/simplegit.rb

$ git stash
```

此时我们的目录就干净了，我们可以查看一下栈内的情况

```sh
$ git stash list
stash@{0}: WIP on master: 049d078 added the index file
stash@{1}: WIP on master: c264051 Revert "added file_size"
stash@{2}: WIP on master: 21d80a5 added number to log
```

**recomand add some message** :

```sh
$ git stash save "test-cmd-stash"
Saved working directory and index state On autoswitch: test-cmd-stash
HEAD 现在位于 296e8d4 remove unnecessary postion reset in onResume function
$ git stash list
stash@{0}: On autoswitch: test-cmd-stash
```

### Pop the stash

```sh
# not change the origin stash
git stash apply # get the newest work
git stash apply [name] # get work through name like stash@{1}

# remove the origin stash and use it
git stash pop

# only remove the orgin
git stash drop [stash@{0}]
```

文件的改动被重新应用了，但是之前暂存的文件却没有重新暂存。 想要那样的话，必须使用 --index 选项来运行 git stash apply 命令，来尝试重新应用暂存的修改。 如果已经那样做了，那么你将回到原来的位置：

```sh
$ git stash apply --index
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   index.html

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   lib/simplegit.rb
```

如果你储藏了一些工作，暂时不去理会，然后继续在你储藏工作的分支上工作，你在重新应用工作时可能会碰到一些问题。如果尝试应用的变更是针对一个你那之后修改过的文件，你会碰到一个归并冲突并且必须去化解它。如果你想用更方便的方法来重新检验你储藏的变更，你可以运行 git stash branch，这会创建一个新的分支，检出你储藏工作时的所处的提交，重新应用你的工作，如果成功，将会丢弃储藏。

```sh
$ git stash branch testchanges
Switched to a new branch "testchanges"
# On branch testchanges
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#      modified:   index.html
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#
#      modified:   lib/simplegit.rb
#
Dropped refs/stash@{0} (f0dfc4d5dc332d1cee34a634182e168c4efc3359)
```

### 暂存未跟踪或忽略的文件

**默认情况下，git stash会缓存下列文件：**
添加到暂存区的修改（staged changes）
Git跟踪的但并未添加到暂存区的修改（unstaged changes）

**但不会缓存一下文件**：
在工作目录中新的文件（untracked files）
被忽略的文件（ignored files）

git stash命令提供了参数用于缓存上面两种类型的文件。使用 `-u` 或者 `--include-untracked`可以stash untracked文件。使用-a或者--all命令可以stash当前目录下的所有修改。

至于git stash的其他命令建议参考Git manual。

## Tag

```sh
git tag#查看所有tag
git show [tag name]#查看tag对应的commit信息

git tag -d [tagname]
#light
git tag [name] [hash]#打标签

#有注释的
git tag -a [name] [hash] -m [messge]

#没有hash默认在当前commit上打标签
```

## .gitignore

写入不需要存储的东西
