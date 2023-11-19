---
sidebar_position: 3
sidebar_label: Undo
sidebar_class_name: green
---
# Git

## Undo commit

### Git Revert

revert is the command we use when we want to take a previous commit and add it as a new commit, keeping the log intact.

```sh
git revert [ID]
```

### Git Reset

简单来说就是回退

```sh
git reset [options] [ID]
```

three options

- `--hard` : 重置 HEAD, 暂存区，工作区，Branch --- 简单来说就是整个重置。**会head回退，并同步到暂存区和工作区**
- `--soft` :  则会保留工作目录的内容，并把因为重置 HEAD 所带来的新的文件差异放进暂存区。**此方法会回退head，暂存区和工作区不变**
- `--mixed` : 保留工作目录，并清空暂存区。也就是说，工作目录的修改、暂存区的内容以及由 reset 所导致的新的文件差异，都会被放进工作目录。简而言之，就是「把所有差异都混合（mixed）放在工作目录中」  **会head回退，并将新的commit替换到暂存区**

> --soft
>Does not touch the index file or the working tree at all (but resets the head to `<commit>`, just like all modes do). This leaves all your changed files "Changes to be >committed", as git status would put it.
>
>--mixed
>Resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the default >action.
>
>If -N is specified, removed paths are marked as intent-to-add (see git-add[1]).
>
>--hard
>Resets the index and working tree. Any changes to tracked files in the working tree since `<commit>` are discarded. Any untracked files or directories in the way of writing any tracked files are simply deleted.

### Git amend

just change the message of commit

```sh
git commit -m "Adding plines to reddme"
```

## Undo working environment

### Delete a file

删除一个文件同步到暂存区

```sh
git add [file]
```

### undo staged changes

暂存区 --> 工作区

```sh
git checkout/restore [file]/.
```

> 如果暂存区没有修改的话，会同步commit中的文件


**删除工作区中   暂存区没有的文件**：

如果我们新创建了一个文件，暂存区没有此文件，那此时restore命令是没有用的。我们可以使用`git clean`命令

1. 使用`git clean -n`来确认会删除那些文件(指出将会删除哪些文件)
2. 使用`git clean -f`来删除不在暂存区的文件

> - 使用`git clean-i`会弹出一个菜单，帮助我们更好的删除不在暂存区的文件
>
> - 使用没有`-d`只删除当前目录下的文件，不删除文件夹，加上则会递归的删除

## Undo staged file3

commit --> staged

```sh
git reset [file/.]
git restore --staged [file/.]
```
