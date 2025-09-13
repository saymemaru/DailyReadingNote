# Git 常用指令

- [Git 常用指令](#git-常用指令)
  - [建立仓库基本操作](#建立仓库基本操作)
  - [出现错误了怎么办](#出现错误了怎么办)
    - [commit 提交错误](#commit-提交错误)
      - [缓存区上传文件过大/上传错误](#缓存区上传文件过大上传错误)
      - [commit 内容有误](#commit-内容有误)
  - [查看信息](#查看信息)
  - [有不想上传的文件](#有不想上传的文件)
  - [git 基本设置](#git-基本设置)
    - [设置作用范围](#设置作用范围)
  - [多人协作](#多人协作)
    - [创建分支](#创建分支)
    - [删除分支](#删除分支)
    - [合并分支](#合并分支)
    - [分支命名规范](#分支命名规范)
    - [想要下载其他仓库](#想要下载其他仓库)
    - [SSH 和 HTTPS](#ssh-和-https)
  - [回档](#回档)
    - [保险](#保险)
  - [.bat 快速push脚本](#bat-快速push脚本)
  - [额外资源](#额外资源)
  - [待完成](#待完成)

## 建立仓库基本操作

首先在cmd中使用命令``cd /d``到达想要建立仓库的路径  

``git init``，初始化仓库  

``git add .``，将当前路径所有文件添加到缓存区

``git commit -m "<评论>"``，为文件添加注释

``git remote add origin <仓库URL>``，为当前仓库指定远程仓库地址

``git push origin <分支>`` //将缓存区内容推送到特定分支

## 出现错误了怎么办

### commit 提交错误

#### 缓存区上传文件过大/上传错误

``git log``查询提交日志，查询提交`head`  
>`head`形如：``77e3f9eb02b96d7d2ea5def048fb4f1d07f19868``

``git reset --soft <head>`` 撤销 commit 到指定的 head 版本，本地修改的文件不会变动

#### commit 内容有误

``git log --oneline``查看最新提交历史

``git commit --amend -m "<修正内容>"`` 快速修改 commit message

``git commit --amend`` 启动编辑器修改 commit message

``git commit --amend --no-edit`` 不修改 commit message, 将暂存区里的新改动与上一个 commit 的内容合并，然后创建一个全新的 commit 来替换旧的

## 查看信息

``git status -s`` 查看当前文件夹文件状态
> 不同的字母表示不同的文件状态  
>
> ``M``修改未暂存
>
> ``MM``修改已暂存
>
> ``A``新添加到暂存

## 有不想上传的文件

使用``.gitignore``忽略不想上传的文件  

在``.git``所在路径建立一个没有后缀的``.gitignore``文件，用记事本打开在其中输入不想上传的文件

[GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表](https://github.com/github/gitignore)

``*.<后缀名>`` 忽略以<后缀名>为后缀的文件

## git 基本设置

### 设置作用范围

- system 整个电脑
- global 当前用户
- local 当前仓库

``git config --list --show-origin`` 查看所有设置，且附带设置文件路径

``git config <key>``  查看特定设置

``git config --global --edit`` 编辑器打开global配置文件

``git config --global user.name "John Doe"``  设置用户名

``git config --global user.email johndoe@example.com`` 设置邮箱

``git config --global core.editor "'E:\app\Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`` 设置编辑器，当前为notepad++

## 多人协作

### 创建分支

如果你不想影响主仓库的文件，但又想加点小料...

`git branch <branch name>` 创建名为`branch name`的分支。

``git checkout <branch name>`` ``HEAD``指针转向名为`branch name`的分支，以后的操作只会影响该分支，并且你当前**目录的文件**会更新为**该分支已储存的内容**。

``git checkout -b <branch name>``: 创建并立即切换，一步到位。

### 删除分支

``git branch -d <branch name>`` 当一个分支的工作不再需要时，可以用这个命令删除它。
>如果分支上有未合并的提交，Git 会阻止你，这时你可以用 -D (大写) 来强制删除。

### 合并分支

``git checkout <main>`` 首先切换到`<main>`主分支

``git merge <branchB>`` 然后与`<branchB>`副分支合并

快速合并 (Fast-forward)：如果`<main>`在你开发`<branchB>`的过程中没有产生任何新的提交，那么会直接合并。

合并冲突 (Merge Conflict)：这才是重头戏。如果在你开发`<branchB>`分支的同时，其他人也修改了`<main>`，并且你们俩改了同一个文件的同一行代码。  

当你尝试合并时 Git 会在冲突文件中插入类似 <<<<<<< HEAD、=======、>>>>>>> dev 的标记，把决定权交还给你。它告诉你`<main>`（也就是 master 分支）的版本是怎样的，`<branchB>`分支的版本又是怎样的。  

你需要做的，就是手动编辑这个文件，保留你想要的代码，删除这些特殊标记，然后再次提交完成合并

```cmd
git add .
git commit
```

### 分支命名规范

- master/main: 主分支，永远保持稳定，用于发布生产版本。
   >你相不相信乐奈幺永远伟大？

- develop: 开发主分支，所有新功能的开发都从这里开始。

- feature/*: 特性分支，用于开发新功能，完成后合并回 develop。

- hotfix/*: 热修复分支，用于紧急修复线上 bug，直接从 master 创建，修复后同时合并回 master 和 develop。



### 想要下载其他仓库

``git clone <github 仓库 URL>`` 将目标URL的仓库克隆到你本地的当前目录下。

``git pull origin <branch name>`` 从远程仓库下载`<branch name>`分支最新的状态
>git pull 本质上是 git fetch（拉取远程更新信息）和 git merge（合并到本地分支）两个命令的组合，确保你的本地版本与团队同步。

### SSH 和 HTTPS

两种是与远程仓库通信的协议。

HTTPS：像每次进门都需要输入用户名和密码。

SSH：通过配置密钥（id_rsa.pub 公钥放在远程仓库，id_rsa 私钥留在本地），实现免密登录。就像你有一把专属的钥匙，安全又方便。

可以在 github 上设置具体权限

## 回档

``git reset --hard <head>`` 强制移动 HEAD 指针和当前分支的指针到指定的历史提交，并用该提交的内容覆盖工作区和暂存区。

### 保险

 reflog 记录了 HEAD 指针的每一次移动。记录了你的每一次 commit、merge、reset、checkout…… 所有的操作。即使你用 git reset --hard 看似抹去了历史，reflog 里依然有迹可循。当你发现 reset 错了：

 ``git reflog`` 找到你 reset 之前那个正确的提交`head`

``git reset --hard <former head>``回到`<former head>`指针的仓库状态

## .bat 快速push脚本

在 git 仓库所在文件夹下建立如下 bat 脚本

自动 cd 到当前文件夹后，会提示输入 commit ,然后推送到分支（当前为main）

```bat
@echo off
echo Processing...

cd /d "%~dp0"
echo Current path is : %CD%

echo Adding files to git...
git add .

set /p commit_msg="PLZ type in git commit message: "
git commit -m "%commit_msg%"

git push origin main
echo Push to default branch complete

pause
```

## 额外资源

1.[通过玩游戏学习git](https://zhuanlan.zhihu.com/p/1942930062568581085)

## 待完成

``git fetch xx`` //拉取xx仓库
``git remote show xx`` //查看xx仓库
``git pull`` //推送
``git remote -v`` //查看所有仓库
