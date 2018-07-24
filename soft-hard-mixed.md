# git rest: soft, hard, mixed区别

## 术语
- HEAD 

当前分支版本顶端的别名，也就是在当前分支你最近的一个提交
- Index

也被称为staging area，是指一整套即将被下一个提交的文件集合。他也是将成为HEAD的父亲的那个commit

- Working Copy

working copy代表你正在工作的那个文件集

- Reset
它本身做的事情就是重置HEAD(当前分支的版本顶端）到另外一个commit。

## Parameters

#### 1. soft

--soft参数告诉Git重置HEAD到另外一个commit，但也到此为止。如果你指定--soft参数，Git将停止在那里而什么也不会根本变化。这意味着index,working copy都不会做任何变化，所有的在original HEAD和你重置到的那个commit之间的所有变更集都放在stage(index)区域中。
![pic-1.png](pics/pic-1.png)

#### 2. hard

--hard参数将会blow out everything.它将重置HEAD返回到另外一个commit(取决于~12的参数），重置index以便反映HEAD的变化，并且重置working copy也使得其完全匹配起来。这是一个比较危险的动作，具有破坏性，数据因此可能会丢失！如果真是发生了数据丢失又希望找回来，那么只有使用：git reflog命令了。makes everything match the commit you have reset to.你的所有本地修改将丢失。如果我们希望彻底丢掉本地修改但是又不希望更改branch所指向的commit，则执行git reset --hard = git reset --hard HEAD. i.e. don't change the branch but get rid of all local changes.另外一个场景是简单地移动branch从一个到另一个commit而保持index/work区域同步。这将确实令你丢失你的工作，因为它将修改你的work tree！
![pic-2.png](pics/pic-2.png)

#### 3. mixed(default)

--mixed是reset的默认参数，也就是当你不指定任何参数时的参数。它将重置HEAD到另外一个commit,并且重置index以便和HEAD相匹配，但是也到此为止。working copy不会被更改。所有该branch上从original HEAD（commit）到你重置到的那个commit之间的所有变更将作为local modifications保存在working area中，（被标示为local modification or untracked via git status)，但是并未staged的状态，你可以重新检视然后再做修改和commit。
![pic-3.png](pics/pic-3.png)

