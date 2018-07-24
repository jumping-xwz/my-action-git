# 常用操作

经常用的命令。

```console
$ git clone
$ git branch
$ git checkout 分支名
$ git checkout -b 分支名
$ git checkout origin/<远程分支> -b <本地分支>
$ git add
$ git checkout -- <file>
$ git reset
$ git commit
$ git push
$ git fetch  #并没更改本地仓库的代码，只是拉取了远程commit数据，将远程仓库的commit版本号 更新为最新。分支git log信息不会变
$ git pull  #fetch+merge，把远程代码拉到本地并merge，git log信息会更新
$ git merge
$ git rebase
$ git log
$ git rebase -i <提交版本号>
```

#### 项目初始化
create a new repository on the command line:
```git
echo "# my-action-gradle" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/wjpdeveloper/my-action-gradle.git
git push -u origin master
```

push an existing repository from the command line:
```console
git remote add origin https://github.com/wjpdeveloper/my-action-gradle.git
git push -u origin master
```

#### 单独设置项目的用户信息
```console
D:\CODEROOT\GitHub\my-action-git>git config user.name wjpdeveloper

D:\CODEROOT\GitHub\my-action-git>git config user.email wjpdev@gmail.com

D:\CODEROOT\GitHub\my-action-git>git config user.name
wjpdeveloper

D:\CODEROOT\GitHub\my-action-git>git config user.email
wjpdev@gmail.com
```

#### 撤消本地提交
```console
git reset HEAD~2        # undo last two commits, keep changes
git reset --hard HEAD~2 # undo last two commits, discard changes  
```

#### 从git中删除文件而不从文件系统中删除它
如果你在git add 时操作不慎，最终可能会添加你不想提交的文件。 
但是，git rm会将它从暂存区域以及文件系统中删除，这可能不是你想要的。在这种情况下，确保只删除暂存版本，并将文件添加到.gitingore以避免再次出现同样的错误：
```console
git reset filename          # or git remove --cached filename
echo filename >> .gitignore # add it to .gitingore to avoid re-adding it
```

#### 编辑提交消息
在提交的情况下修改拼写错误：
```console
git commit --amend                  # start $EDITOR to edit the message
git commit --amend -m "New message" # set the new message directly
```
但并非所有git-amend都能这样做。如果忘记添加文件，只需添加它并修改之前的提交：
```console
git add forgotten_file 
git commit --amend
```
`--amend`实际上会创建一个替换前一个提交的新提交，因此不要用它来修改已经到中央存储库的提交。

#### 恢复推送的提交
如果错误的提交进入中央存储库，git提供了一种简单的方法来恢复单个或多个提交：
```console
 git revert c761f5c              # reverts the commit with the specified id
 git revert HEAD^                # reverts the second to last commit
 git revert develop~4..develop~2 # reverts a whole range of commits
```
如果你只想对working tree进行必要的更改，则可以使用--no-commit/ -n ：
```console
# undo the last commit, but don't create a revert commit 
git revert -n HEAD
```

#### 谁打乱了我的代码？
```console
git blame [file_name]
```

