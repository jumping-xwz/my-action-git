# my-action-git

此处列出我关于 Git 的学习实践。

- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
- [深入理解学习Git工作流（git-workflow-tutorial）](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)

# HandBook

## 初始化本地仓库
```
git init
```

## 配置

#### 配置用户名,邮件
```
git config --global user.name "xxx"
git config --global user.email "xxx@xxx.com"
```

#### git status等命令自动着色
```
git config --global color.ui true
git config --global color.status auto
git config --global color.diff auto
git config --global color.branch auto
git config --global color.interactive auto
```

## 远程仓库

#### 检出仓库
```
git clone
```

#### 查看远程仓库
```
git remote -v
```

#### 添加远程仓库
```
git remote add [name] [url]
```

#### 删除远程仓库
```
git remote rm [name]
```

#### 修改远程仓库
```
git remote set-url --push[name][newUrl]
```

#### 拉取远程仓库
```
git pull [remoteName] [localBranchName]
```

#### 推送远程仓库
```
git push [remoteName] [localBranchName]
```

## 添加

#### 添加xyz文件
```
git add xyz
```

#### 增加当前子目录下所有更改过的文件
```
git add .
```

## 提交
```
git commit -m 'xxx'
```

#### 合并上一次提交（用于反复修改）
```
git commit --amend -m 'xxx'
```

#### 将add和commit合为一步
```
git commit -am 'xxx'
```

## 删除
```
git rm xxx
```

#### 递归删除
```
git rm -r *
```

## 日志

#### 显示提交日志
```
git log
```

#### 显示1行日志 -n为n行
```
git log -1 
```

#### 显示提交日志及相关变动文件
```
git log --stat
git log -p -m
```

#### 显示某个提交的详细内容
```
git show dfb02e6e4f2f7b573337763e5c0013802e392818
git show dfb02
```

#### 显示HEAD提交日志
```
git show HEAD
```

#### 显示HEAD的父（上一个版本）的提交日志 ^^为上两个版本 ^5为上5个版本
```
git show HEAD^
```

#### 显示v2.0的日志及详细内容
```
git show v2.0
```

#### 显示v2.0的日志
```
git log v2.0
```

#### 列出git index包含的文件
```
git ls-files
```

#### 显示提交历史对应的文件修改
```
git whatchanged
```

#### 图示提交日志
```
git log --pretty=format:'%h %s' --graph
git show HEAD~3
git show -s --pretty=raw 2be7fcb476
```

## 分支操作

#### PUSH本地分支到远程分支
```
git push --progress "origin" wjp-dev:wjp-dev
```

#### 查看本地分支
```
git branch
```
- 显示包含提交50089的分支 `git branch --contains 50089`
- 显示所有分支 `git branch -a`
- 显示所有已合并到当前分支的分支 `git branch --merged`
- 显示所有未合并到当前分支的分支 `git branch --no-merged`

#### 查看远程分支
```
git branch -r
```

#### 创建本地分支
```
git branch [name]
```

#### 切换分支
```
git checkout [name]
```

#### 创建新分支并立即切换到新分支
```
git checkout -b [name]
```

#### 本地分支改名
```
git branch -m master master_copy
```

#### 从当前分支创建新分支master_copy并检出
```
git checkout -b master_copy
git checkout -b master master_copy
```

#### 检出已存在的features/performance分支
```
git checkout features/performance
```

#### 检出远程分支hotfixes/BJVEP933并创建本地跟踪分支
```
git checkout --track hotfixes/BJVEP933
```

#### 删除分支
```
git branch -d [name]
git branch -D [name] 强制删除
```

#### 合并远程master分支至当前分支
``` 
git merge origin/master
```

#### 创建远程分支(本地分支push到远程)
```
 git push origin [name]
```
- 将当前分支push到远程master分支 `git push origin master`

#### 从远程分支develop创建新本地分支devel并检出
```
git checkout -b devel origin/develop
```

#### 检出head版本的README文件
```
git checkout -- README
```

#### 删除远程分支
```
 git push origin :heads/[name]
```
- 删除远程仓库的hotfixes/BJVEP933分支 `git push origin :hotfixes/BJVEP933`

#### 图示当前分支历史
```
git show-branch
```

#### 图示所有分支历史
```
git show-branch --all
```

#### 合并提交ff44785404a8e的修改
```
git cherry-pick ff44785404a8e
```

#### 获取所有远程分支（不更新本地分支，另需merge）
```
git fetch
```

#### 获取所有原创分支并清除服务器上已删掉的分支
```
git fetch --prune
```

#### 获取远程分支master并merge到当前分支
```
git pull origin master
```

## 版本操作

#### 查看版本状态
```
git status
```

#### 查看版本
```
git tag
```

#### 创建版本
```
git tag [name]
git tag -a v2.0 -m 'xxx'
```

#### 删除版本
```
git tag -d [name]
```

#### 查看远程版本
```
git tag -r
```

#### 创建远程版本(本地版本push到远程)
```
git push origin [name]
```

#### 检出版本v2.0
```
git checkout v2.0
```

#### 删除远程版本
```
git push origin :refs/tags/[name]
```

#### 把所有tag推送到远程仓库
```
git push --tags 
```

## 变更

#### 显示所有未添加至index的变更
```
git diff
```

#### 显示所有已添加index但还未commit的变更
```
git diff --cached
```

#### 比较与上一个版本的差异
```
git diff HEAD^
```

#### 比较与HEAD版本lib目录的差异
```
git diff HEAD -- ./lib
```

#### 比较远程分支master上有本地分支master上没有的
```
git diff origin/master..master
```

#### 只显示差异的文件，不显示具体内容
```
git diff origin/master..master --stat
```

#### 重命名文件README为README2
```
git mv README README2
```

## 暂存

#### 暂存当前修改，将所有至为HEAD状态
```
git stash
```

#### 查看所有暂存
```
git stash list
```

#### 参考第一次暂存
```
git stash show -p stash@{0}
```

#### 应用第一次暂存
```
git stash apply stash@{0}
```

## 忽略

- 根目录创建 .gitignore 文件
- 写入不需要的文件夹名或文件，每个元素占一行

## 重置

#### 将当前版本重置为HEAD
```
git reset --hard HEAD
git rebase
```

#### 撤销提交dfb02e
```
git revert dfb02e
```

## 内部命令

#### 显示某个git对象
```
git ls-tree HEAD
```

#### 显示某个ref对于的SHA1 HASH
```
git rev-parse v2.0
```

#### 显示所有提交，包括孤立节点
```
git reflog
git show HEAD@{5}
```

#### 显示master分支昨天的状态
```
git show master@{yesterday}
```

#### 文件中搜索文本
```
git grep "delete from"
git grep -e '#define' --and -e SORT_DIRENT
```

#### 维护及数据恢复
```
git gc
git fsck
```

