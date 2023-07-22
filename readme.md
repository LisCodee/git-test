# git笔记

> Tip: []中的内容为可选参数，{}中的内容为自己的参数内容。

## 基本命令

### git add [-f] {filename}

将文件修改提交到暂存区。

### git commit -m "comment"

上就是把暂存区的所有内容提交到当前分支。

### git diff {filename}

查看修改内容,

```git
git diff HEAD -- filename   # 查看版本库和工作区的区别
```

### git log [--pretty=oneline] [--graph] [--abbrev-commit]

查看提交记录，--prett=oneline表示简化输出，--graph表示显示分支合并图,--abbrev-commit仅显示commit id的前七个字符。

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
git branch -D {branch_name}:强行删除分支，不管分支是否合并
git branch --set-upstream-to=origin/{branch_name} {local_branch_name}:指定本地{local_branch_name}分支与远程origin/{branch_name}分支的链接

### git merge [--no-ff] {branch_name}

将{branch_name}分支的修改合并到当前分支上。[--no-ff]表示强制禁用Fast forward模式，Git会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
否则，使用fast forward模式合并后的分支看不出来合并历史。

### git stash

git stash:可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。
git stash list:查看存储的现场；
git stash apply:恢复现场，stash内容并不删除
git stash pop:恢复并删除stash内容
git stash drop:删除stash内容

### git cherry-pick {commit id}

复制一个特定的提交到当前分支。一般用于把bug提交的修改“复制”到当前分支，避免重复劳动。

### git pull 

抓取远程分支。先pull再push的方案会使得提交历史混乱。

### git rebase

把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。

## 标签管理

### git tag [{tag_name}] [{commit_id}] [-a | -m | -d]

默认为显示所有tag，加上{tag_name}就是为当前分支打上标签，默认打在最新的commit上，加上{commit_id}后就可以为特定的commit打上标签。
通过**git show {tag_name}** 来显示标签具体信息。
-d:删除标签

git tag -a {tag_name} -m {comment} [{commit_id}]:创建带有说明的标签

> 标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

### git push origin {tag_name}

推送某个标签到远程。
git push origin --tags:推送所有标签到远程
git push origin :refs/tags/{tag_name}：删除远程标签，需要先删除本地标签然后推送到远程

## 自定义git

### git config [--global] [ user.name | user.email | color.ui ｜ alias.{al_name}]
```git 
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

### git ignore

[官方ignore文件](https://github.com/github/gitignore)

git check-ignore -v {file_name}：查看文件被哪条规则忽略

## [搭建git服务器](https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664)

