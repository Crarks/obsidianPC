[安装资料](https://blog.csdn.net/mukes/article/details/115693833?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522170392647116800184116590%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=170392647116800184116590&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-4-115693833-null-null.142^v99^pc_search_result_base1&utm_term=git&spm=1018.2226.3001.4187)    

Git Bash：Git Bash 提供了一个模拟 Linux 终端的命令行界面，在这里可以执行 Git 命令。它是一种强大的工具，适用于熟悉 Linux 或 macOS 终端界面的开发人员。您可以在 Git Bash 中输入各种 Git 命令，比如克隆代码库、提交更改、合并分支等。    
Git CMD：Git CMD（也称为 Git 命令提示符）是另一种在 Windows 上运行 Git 命令的命令行界面。它提供了与 Git Bash 类似的功能，适用于喜欢使用 Windows 命令提示符的用户。    
Git FAQs：Git FAQs 是一份常见问题解答文档，提供了关于 Git 的常见疑问和解决方法。它包含了一些常见的问题和解答，可以帮助您解决在使用 Git 过程中遇到的问题。   
Git GUI：Git GUI 是一个图形化界面工具，用于执行 Git 操作。它提供了直观的用户界面，有助于不熟悉命令行的开发人员进行版本控制、提交更改、查看历史记录等操作。   
Git Release Notes：Git Release Notes（版本说明）是每个 Git 版本的详细信息记录，包含了新功能、改进、修复的问题和已知问题等内容。通过查看版本说明，您可以了解特定版本的 Git 更新情况和变更点。  


# git 的学习

[链接显示的内容](#连接到的文章内的部分)  
使用方式 命令行：git bash或者cmd    ide插件     gui  
git的主要功能有创建仓库，克隆仓库，打开仓库  
配置好环境变量后可以在cmd里运行，也可用git bash  
一些git bash里的命令和linux一致

git -v  
--global：全局配置，对所有仓库生效  
--system：系统配置，对所有用户生效  

配置用户名：git config --global user.name "xxx"  
配置邮箱：git config --global user.email "xxx"  
配置密码：git config --global credential.helper store  
查看配置信息：git config --global --list  

**创建仓库**（即把文件夹给到git管理  
切换到文件夹下后 git init（已经有目录的话  
或者git init 目录名  
创建成功后会有一个隐藏文件夹.git

**克隆仓库**
git clone http地址 .git

### git结构
工作区(working directory) .git 所在目录，文件区  
暂存区(staging Area/index).git/index，实际上git进行版本控制的主要区域  
本地仓库(local repository).git/objects，git存储代码和版本信息主要位置  

**git命令**
+ git status 查看仓库状态  
+ git add 添加到暂存区  
+ git commit 提交暂存区中的文件(文件名可以是文件夹或包含通配符)  （-m "代码提交说明" 可以忽略进入vim模式 e.g.git -m "balala" test.txt ，git commit --amend可以修改描述
+ git ls-files 列出当前 Git 仓库中跟踪的文件（它的作用是显示 Git 仓库中已跟踪文件的列表,包括已修改、已暂存和已提交的文件）
+ git log 查看提交记录（--oneline简介记录
+ git reflog 查看修改记录
+ git reset 版本退回（--soft保留工作区与暂存区内容 --hard丢弃工作区与暂存区 --mixed保留工作区丢弃暂存区）e.g.git reset --soft **Head^ [^1]**直接返回上一个版本
+ git diff 查看工作区，暂存区，本地仓库之间的差异；查看不同版本的差异
	+ 默认工作区和暂存区差异 
	+ git diff head查看工作区和版本库  
	+ --cached查看暂存区和版本库    
	+ id1 id2比较两个版本差异
+  git rm 文件名 在工作区和暂存区中删除文件
+ .gitignore 文件中可以录入忽略文件名对不想管理文件进行忽略(不能已添加到版本库)啊啊啊没看明白pass
+ lesson 10

**ssh**
非堆成加密Secure Shell Protocol
[github官方教程](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)  
目录：C:\Users\Crark/.ssh/id_rsa
有.pub后缀为公钥，上一个是私钥
p.s. 还是要在.ssh文件夹里添加一下config文件配置一下端口和host啥的

**关联本地远程仓库**
git remote add origin git@github.com:Crarks/test.git  
git branch -M main(:main)（关于git的分支branch问题,简单来说就是保持本地与远程分支一致。
git push -u origin main  
git remote -v 查看对应远程

**git远程管理**
git push
git pull (<远程仓库名><远程分支名>:<本地分支名>)

**VS远程管理**
qaq，用vs好方便哦，都不用我push了
新建终端 crtl+shift+~  

**分支**
git branch xx（创建  -d删除分支
git switch（切换  
git merge xx（在main分支里合并分支 ，合并后不会消失 
git log --graph --oneline --decorate --all（查看分支情况
git checkout xx（切换/修复  
rebase啥啥啥的
还有fetch啥啥啥的
[^1]:Head^或head~用来代指上一个版本n  e.g.head2/3表示2/3个版本以前

