# 常用操作

经常用的命令，其它命令主要还是使用IDEA自带的UI来进行可视化操作。

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
```git
git remote add origin https://github.com/wjpdeveloper/my-action-gradle.git
git push -u origin master
```

#### 单独设置项目的用户信息
```git
D:\CODEROOT\GitHub\my-action-git>git config user.name wjpdeveloper

D:\CODEROOT\GitHub\my-action-git>git config user.email wjpdev@gmail.com

D:\CODEROOT\GitHub\my-action-git>git config user.name
wjpdeveloper

D:\CODEROOT\GitHub\my-action-git>git config user.email
wjpdev@gmail.com
```

