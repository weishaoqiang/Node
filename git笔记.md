# git笔记
## git init命令
- 初始化一个git仓库
## git status命令
- 通过git status查看当前的命令查看仓库状态
## touch 命令
- touch app.js创建文件，这个不属于git命令，是shell命令创建文件的命令
## mr命令
- 用于删除文件的命令
## mkdir 命令
- 用于创建文件夹
## git add <file>命令
- 提交多个文件的命令： * / --all / -A ,告诉git当前所有的文件被git管理。
- <file>是文件路径，往git仓库添加文件，让git来管理当前添加进去的文件
- 如果不提示错误，那么就说明添加的文件已经被git所管理了，但是还没有提交。
## git commit命令
- git commit -m '提交信息说明描述' ,这个命令就是把add进来的文件进行提交,这样这个文件就被提交到了git的仓库永久管理起来了。
## git config的命令
- git config user.email '<邮箱>'和 git config user.name '<用户名>'
- 在git使用之前，需要配置user.name和user.email。
- 作用方便团队合作。
## git config --list
- 查看配置项目有没有成功,比如邮箱和username。如果成功，就能看到看到刚刚配置的信息。
## 查看提交日志git log
- 通过这个命令可以查看修改的日志
- git log --online 这个命令可以查看简易的日志。
## git oneline
- 查看简单的提交日志。
## git reflog
- 查看所有提交过的状态，就算版本回退版本之后可以查看所有的提交对话。
## clear 命令，清空这个控制台的对话信息

## git reset --hard回退版本命令
## git分支 branch说明
- 主分支-master
- 测试分支-debug分支
- 开发分支-dev分支，开发代码一般就在这个分支上开发

## git branch 创建分支的命令
- git branch ： 查看分支
- git branch '分支名字' ： 创建分支
- git checkout '分支名字' ：切换分支
- git branch -d '分支名字' ： 删除分支，关键点事不能够在当前分支上进行删除当前分支操作
## git merge 命令
- 用于合并分支
- git merge '分支名' 合并分支名字。

## git push [仓库地址] [分支名称], git pull [仓库地址] [分支名称], git clone命令
- 提交，拉取，克隆代码

## 仓库初始化创建分支注意事项
- 跟目录必须有内容，如果是空的仓库是创建不了分支的
