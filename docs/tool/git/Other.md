---
sidebar_position: 4
sidebar_label: Other
sidebar_class_name: green
---
# Other tools

## submodule

简单来说就是在一个项目中我们需要使用**自己的或者其他人的项目**，通常是库。此时git允许我们将一个git仓库作为另一个git仓库的子目录

**添加模块**:

```sh
git submodule add https://github.com/chaconinc/DbConnector [path to you want]
```

此时使用`git status` 的时候会多出一个项目文件和 .gitmodules 文件

```sh
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   .gitmodules
    new file:   DbConnector
```

.gitmodules 文件内部保存另 submodule 中的关键信息。

```txt
[submodule "DbConnector"]
    path = DbConnector
    url = https://github.com/chaconinc/DbConnector
```

其中git不会跟踪 submodule 中的文件，而是是为一个子模块

### 克隆含有submodule的项目

克隆此类项目，submodule只是一个空文件，你必须运行两个命令：git submodule init 用来初始化本地配置文件，而 git submodule update 则从该项目中抓取所有数据并检出父项目中列出的合适的提交。

此时就恢复到原始项目状态

当然我们可以直接使用 `--recurse-submodules` 会自动初始化并更新子项目

### 删除子模块

删除子模块比较麻烦，需要手动删除相关的文件，否则在添加子模块时有可能出现错误
同样以删除assets文件夹为例

#### 删除子模块文件夹

```shell
$ git rm --cached assets
$ rm -rf assets
```

#### 删除.gitmodules文件中相关子模块信息

```txt
[submodule "assets"]
  path = assets
  url = https://github.com/maonx/vimwiki-assets.git
```

#### 删除.git/config中的相关子模块信息

```txt
[submodule "assets"]
  url = https://github.com/maonx/vimwiki-assets.git
```

#### 删除.git文件夹中的相关子模块文件

```shell
$ rm -rf .git/modules/assets
```

### submodule 开发

我们可以像正常模式一样开发submodule, 开发完成之后，主项目会记录更新后的 commit ID
使用 `git diff` 可以查看到更新状态

