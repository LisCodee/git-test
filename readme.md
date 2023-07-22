# git笔记

> Tip: []中的内容为可选参数，{}中的内容为自己的参数内容。

## 基本命令

### git add {filename}

将文件修改提交到暂存区。

### git commit -m "comment"

上就是把暂存区的所有内容提交到当前分支。

### git diff {filename}

查看修改内容,

```git
git diff HEAD -- filename   # 查看版本库和工作区的区别
```

### git log [--pretty=oneline]

查看提交记录，--prett=oneline表示简化输出。

### git reset [--hard] {HEAD^}

回退当前版本，HEAD表示当前版本，HEAD^表示上一个提交的版本，回退n个版本可以使用 HEAD~n来表示。也可以使用commit id来回退到指定提交版本。

### git reflog

查看执行过的git命令。

### git restore [--staged] {filename}

丢弃filename对应文件的工作区的修改，如果已经通过git add 添加到暂存区，那么撤销修改就回到添加到暂存区后的状态。（回到最近commit或add的状态）。 **--staged** 表示撤销暂存区修改，回到上次commit的状态。

### git rm {filename}

在工作区删除文件后，如果想要在版本库也要删除该文件，可以使用git rm命令,然后commit，如果是误删文件，则可以使用**git restore {filename}**恢复文件。
如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

### git remote命令

git remote -v:查看远程仓库信息
git remote add {origin} {giturl}：将远程仓库和本地仓库关联。
git remote rm {origin}:删除远程仓库。

### git push [-u] origin {main}

加上了-u参数，Git不但会把本地的{main}分支内容推送的远程新的{main}分支，还会把本地的{main}分支和远程的{main}分支关联起来，在以后的推送或者拉取时就可以简化命令。

## 分支管理

### git checkout/switch [-b]/[-c] {branch_name}

创建新分支{breanch_name}，并切换到此分支。相当于**git branch {breanch_name}** + **git checkout {branch_name}** 组合。

### git branch

git branch {branch_name}: 新建分支
git branch:查看所有分支信息。
git branch -d {branch_name}:删除分支。

### git merge {branch_name}

将{branch_name}分支的修改合并到当前分支上。