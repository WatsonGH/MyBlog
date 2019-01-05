# Git #
Git是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理

#### 版本库 ####
版本库又名仓库，英文名repository，可以简单的理解为一个目录。这个目录里面有你所有需要被git管理的文件和子目录的文件。

#### Git配置文件 ####
git的三个配置文件
1. 安装目录\etc\gitconfig 文件: 包含系统上每一个用户及他们仓库的通用配置。 如果使用带有 --system 选项的 git config 时，它会从此文件读写配置变量。
2. C:\\Administrator\.gitconfig 或 ~/.config/git/config 文件：只针对当前用户，所以一般会存在用户Administrator文件夹。 可以传递 --global 选项让 Git 读写此文件。
3. 当前使用仓库的 Git 目录中的 config 文件（就是 .git/config）：--local针对该仓库。


## Git命令 ##
**git config [--system][--global][--local] --list**---检查配置信息<br/><br/>
**git config [key]**---检查指定key的配置信息，比如:user.name<br/><br/>
**git clone [url]**---克隆远程端仓库到本地<br/><br/>
**git remote**---查看当前的远程库<br/><br/>

**git init**---初始化一个目录为git管理的仓库(**repository**)。其实就是在该目录下生成 **.git** 的文件夹(隐藏)<br/><br/>
**git status**---查看当前仓库的状态(文件的改动创建)<br/><br/>
**git diff [file]**---比较指定的文件当前的状态与本地主分支上的文件的区别<br/>
>对于修改的前的信息会以-开头并标红，对于修改后的信息会以+开头并标绿
>![git diff命令](https://i.imgur.com/HPQPHFz.png)

**git add [file1 file2] [*]**---把文件交给git管理，多个文件用空格隔开，add的操作是把文件加入暂存区stage<br/><br/>
**git commit -m ""**---把暂存区的文件提交到本地主分支<br/><br/>
**git commit -m ""**---把暂存区的文件提交到本地主分支<br/><br/>
