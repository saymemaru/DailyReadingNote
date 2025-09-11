# Git 常用指令

- [Git 常用指令](#git-常用指令)
  - [建立仓库基本操作](#建立仓库基本操作)
  - [查看信息](#查看信息)
  - [使用``.gitignore``忽略不想上传的文件](#使用gitignore忽略不想上传的文件)
  - [Config](#config)
  - [多人协作](#多人协作)
  - [待完成](#待完成)


## 建立仓库基本操作

首先在cmd中使用命令``cd /d``到达想要建立仓库的路径  

``git init``，初始化仓库  

``git add .``，缓存当前路径所有文件

``git commit -m "<评论>"``，为文件添加注释

``git remote add origin <仓库URL>``，指定目标远程仓库

``git push origin <分支>`` //推送到特定分支

## 查看信息

``git status -s`` 查看当前文件夹文件状态
> 不同的字母表示不同的文件状态  
> 
> ``M``修改未暂存
>
> ``MM``修改已暂存
>
> ``A``新添加到暂存

## 使用``.gitignore``忽略不想上传的文件

在``.git``所在路径建立一个没有后缀的``.gitignore``文件，用记事本打开在其中输入不想上传的文件

[GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表](https://github.com/github/gitignore)

``*.<后缀名>`` 忽略以<后缀名>为后缀的文件

## Config

``git config --list`` 查看所有设置

``git config <key>``  查看特定设置

``git config --global user.name "John Doe"``  设置用户名

``git config --global user.email johndoe@example.com`` 设置邮箱

## 多人协作

## 待完成

``git fetch xx`` //拉取xx仓库
``git remote show xx`` //查看xx仓库
``git pull`` //推送
``git remote -v`` //查看所有仓库