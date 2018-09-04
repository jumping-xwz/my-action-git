# my-action-git

此处列出我关于 Git 的学习实践。

- [git - 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
- [常用操作](common-operations.md)
- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
- [深入理解学习Git工作流（git-workflow-tutorial）](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)
- [git rest: soft, hard, mixed区别](soft-hard-mixed.md)
- [洁癖者用 Git：pull --rebase 和 merge --no-ff](http://hungyuhei.github.io/2012/08/07/better-git-commit-graph-using-pull---rebase-and-merge---no-ff.html)
- [Cherry-Pick](https://juejin.im/post/5925a2d9a22b9d0058b0fd9b)
- [关于Git分支中HEAD和Master的理解](https://zhuanlan.zhihu.com/p/40001702)
- [git stash提交PR的正确步骤&git squash技术](https://www.cnblogs.com/dsxniubility/p/4460834.html)

--- 

# 注意事项
1. #### The golden rule of rebase

> “No one shall rebase a shared branch” — Everyone about rebase

- 请不要在公共分支进行 rebase 操作， 这会坑死队友.

see more deatail on page: [Git rebase and the golden rule explained.](https://medium.freecodecamp.org/git-rebase-and-the-golden-rule-explained-70715eccc372)

# HandBook

## 初始化本地仓库
```git
git init
```

## 配置

#### 配置用户名,邮件
```git
git config --global user.name "xxx"
git config --global user.email "xxx@xxx.com"
```

#### git status等命令自动着色
```git
git config --global color.ui true
git config --global color.status auto
git config --global color.diff auto
git config --global color.branch auto
git config --global color.interactive auto
```

## 远程仓库

#### 检出仓库
```git
git clone
```

#### 查看远程仓库
```git
git remote -v
```

#### 添加远程仓库
```git
git remote add [name] [url]
```

#### 删除远程仓库
```git
git remote rm [name]
```

#### 修改远程仓库
```git
git remote set-url --push[name][newUrl]
```

#### 拉取远程仓库
```git
git pull [remoteName] [localBranchName]
```

#### 推送远程仓库
```git
git push [remoteName] [localBranchName]
```

## 添加

#### 添加xyz文件
```git
git add xyz
```

#### 增加当前子目录下所有更改过的文件
```git
git add .
```

## 提交
```git
git commit -m 'xxx'
```

#### 合并上一次提交（用于反复修改）
```git
git commit --amend -m 'xxx'
```

#### 将add和commit合为一步
```git
git commit -am 'xxx'
```

## 删除
```git
git rm xxx
```

#### 递归删除
```git
git rm -r *
```

## 日志

#### 显示提交日志
```git
git log
git log --oneline
git log —pretty=oneline
git log --graph
git log --all

git log --graph --decorate --oneline
```

#### 显示1行日志 -n为n行
```git
git log -1 
```

#### 显示提交日志及相关变动文件
```git
git log --stat
git log -p -m
```

#### 显示某个提交的详细内容
```git
git show dfb02e6e4f2f7b573337763e5c0013802e392818
git show dfb02
```

#### 显示HEAD提交日志
```git
git show HEAD
```

#### 显示HEAD的父（上一个版本）的提交日志 ^^为上两个版本 ^5为上5个版本
```git
git show HEAD^
```

#### 显示v2.0的日志及详细内容
```git
git show v2.0
```

#### 显示v2.0的日志
```git
git log v2.0
```

#### 列出git index包含的文件
```git
git ls-files
```

#### 显示提交历史对应的文件修改
```git
git whatchanged
```

#### 图示提交日志
```git
git log --pretty=format:'%h %s' --graph
git show HEAD~3
git show -s --pretty=raw 2be7fcb476
```

## 分支操作

#### PUSH本地分支到远程分支
```git
git push --progress "origin" wjp-dev:wjp-dev
```

#### 查看本地分支
```git
git branch
```
- 显示包含提交50089的分支 `git branch --contains 50089`
- 显示所有分支 `git branch -a`
- 显示所有已合并到当前分支的分支 `git branch --merged`
- 显示所有未合并到当前分支的分支 `git branch --no-merged`

#### 查看远程分支
```git
git branch -r
```

#### 创建本地分支
```git
git branch [name]
```

#### 切换分支
```git
git checkout [name]
```

#### 创建新分支并立即切换到新分支
```git
git checkout -b [name]
```

#### 本地分支改名
```git
git branch -m master master_copy
```

#### 从当前分支创建新分支master_copy并检出
```git
git checkout -b master_copy
git checkout -b master master_copy
```

#### 检出已存在的features/performance分支
```git
git checkout features/performance
```

#### 检出远程分支hotfixes/BJVEP933并创建本地跟踪分支
```git
git checkout --track hotfixes/BJVEP933
```

#### 删除分支
```git
git branch -d [name]
git branch -D [name] 强制删除
```

#### 合并远程master分支至当前分支
```git
git merge origin/master
```

#### 创建远程分支(本地分支push到远程)
```git
 git push origin [name]
```
- 将当前分支push到远程master分支 `git push origin master`

#### 从远程分支develop创建新本地分支devel并检出
```git
git checkout -b devel origin/develop
```

#### 检出head版本的README文件
```git
git checkout -- README
```

#### 删除远程分支
```git
 git push origin :heads/[name]
```
- 删除远程仓库的hotfixes/BJVEP933分支 `git push origin :hotfixes/BJVEP933`

#### 图示当前分支历史
```git
git show-branch
```

#### 图示所有分支历史
```git
git show-branch --all
```

#### 合并提交ff44785404a8e的修改
```
git cherry-pick <commit-id>
git cherry-pick ff44785404a8e

git cherry-pick -x <commit_id>  //增加 -x 参数，表示保留原提交的作者信息进行提交。
git cherry_pick <start-commit-id>…<end-commit-id> // (左开，右闭] 
git cherry-pick <start-commit-id>^...<end-commit-id> //[左闭，右闭] 
```

#### 获取所有远程分支（不更新本地分支，另需merge）
```git
git fetch
```

#### 获取所有原创分支并清除服务器上已删掉的分支
```git
git fetch --prune
```

#### 获取远程分支master并merge到当前分支
```git
git pull origin master
```

## 版本操作

#### 查看版本状态
```git
git status
```

#### 查看版本
```git
git tag
```

#### 创建版本
```git
git tag [name]
git tag -a v2.0 -m 'xxx'
```

#### 删除版本
```git
git tag -d [name]
```

#### 查看远程版本
```git
git tag -r
```

#### 创建远程版本(本地版本push到远程)
```git
git push origin [name]
```

#### 检出版本v2.0
```git
git checkout v2.0
```

#### 删除远程版本
```git
git push origin :refs/tags/[name]
```

#### 把所有tag推送到远程仓库
```git
git push --tags 
```

## 变更

#### 显示所有未添加至index的变更
```git
git diff
```

#### 显示所有已添加index但还未commit的变更
```git
git diff --cached
```

#### 比较与上一个版本的差异
```git
git diff HEAD^
```

#### 比较远程分支master上有本地分支master上没有的
```git
git diff origin/master..master
```

#### 只显示差异的文件，不显示具体内容
```git
git diff origin/master..master --stat
```

#### 重命名文件README为README2
```git
git mv README README2
```

## 暂存

#### 暂存当前修改，将所有至为HEAD状态
```git
git stash
```

#### 查看所有暂存
```git
git stash list
```

#### 参考第一次暂存
```git
git stash show -p stash@{0}
```

#### 应用第一次暂存
```git
git stash apply stash@{0}
```

## 忽略

- 根目录创建 .gitignore 文件
- 写入不需要的文件夹名或文件，每个元素占一行

## 重置

#### 将当前版本重置为HEAD
```git
git reset --hard HEAD
git rebase
```

#### 撤销提交dfb02e
```git
git revert dfb02e
```

## 内部命令

#### 显示某个git对象
```git
git ls-tree HEAD
```

#### 显示某个ref对于的SHA1 HASH
```git
git rev-parse v2.0
```

#### 显示所有提交，包括孤立节点
```git
git reflog
git show HEAD@{5}
```

#### 文件中搜索文本
```git
git grep "delete from"
git grep -e '#define' --and -e SORT_DIRENT
```

#### 维护及数据恢复
```git
git gc
git fsck
```

#### 显示设定清单
```console
$ git config --global --list
```

#### 把不需要用的文件归类到非管理对象
```console
$ echo <filename> >> .gitignore
```

#### 通过代理主机连接http
在.gitconfig文件的http项目添加以下的设定。
```
[http]
proxy = <代理主机的电子邮件地址>:<代理主机的端口号码
```
或者
```console
$ git config --global http.proxy <代理主机的电子邮件地址>:<代理主机的端口号码>
```

#### 通过需要用户认证的代理主机连接http
在.gitconfig文件的http项目添加以下的设定。
```
[http]
proxy = http://<用户名>:<密码>@<代理主机的电子邮件地址>:<代理主机的端口号码>
```
或者
```console
$ git config --global http.proxy http://<用户名>:<密码>@<代理主机的电子邮件地址>:<代理主机的端口号码>
```

#### 修改最近的提交记录 | 只修改最近的提交记录的注解
可以删除前一次提交，并创建一个新的提交记录以替代之前的提交。
```console
$ git commit --amend
```

#### 中途停止rebase
```console
$ git rebase --abort
```

#### 放弃最近的提交
```console
$ git reset --hard HEAD~
```

#### 我想了一下，决定不对 index.html 做更改了，想一下子把它返回到未更改状态
```console
$ git checkout -- index.html

# 如果想将多个文件撤销呢，文件名用一个“.”代替
$ git checkout -- .
```

#### 放弃rebase
```console
$ git reset --hard <commit>
```

#### 查找包含特定注解的提交
```console
$ git log --grep "<pattern>"
```

#### 修改已注册的远程数据库的电子邮件地址
```console
$ git remote set-url <name> <newurl>
```

#### 修改已注册的远程数据库
```console
$ git remote rename <old> <new>
```

#### 高效撤销Git管理的文件在各种状态下的更改
- 文件还未提交到暂存区，只是在工作目录中修改了，想要撤销
```
git checkout file-name (撤销单个文件修改)
git checkout . (撤销当前工作空间中所有文件的修改)
```
- 文件已经提交到本地仓库，但还没有push到远程仓库，想要撤销
```
git log (查看并记录下要回滚到的commitId)
git reset --hard commitId (回退版本)
```
- 文件已经提交到远程仓库，想要撤销
```
git log (查看并记录下要回滚到的commitId)
git reset --hard commitId (回退版本)
git push -f origin branch-name
```