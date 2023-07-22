# git笔记

## 基本命令

### git add filename

将文件修改提交到暂存区。

### git commit -m "comment"

上就是把暂存区的所有内容提交到当前分支。

### git diff filename

查看修改内容,

```git
git diff HEAD -- filename   # 查看版本库和工作区的区别
```

### git log [--pretty=oneline]

查看提交记录，--prett=oneline表示简化输出。

### git reset [--hard] HEAD^

回退当前版本，HEAD表示当前版本，HEAD^表示上一个提交的版本，回退n个版本可以使用 HEAD~n来表示。也可以使用commit id来回退到指定提交版本。

### git reflog

查看执行过的git命令。

### git restore [--staged] filename

丢弃filename对应文件的工作区的修改，如果已经通过git add 添加到暂存区，那么撤销修改就回到添加到暂存区后的状态。（回到最近commit或add的状态）。 ** --staged ** 表示撤销暂存区修改，回到上次commit的状态。

