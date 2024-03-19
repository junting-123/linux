#主要目标
	1、git基础知识——提交、分支、提交树上移动
	2、创建github仓库


##1、git基础
	git 是一个开源的分布式版本控制系统，用于跟踪文件的变化并协调多人开发项目。
	git 原理是将文件存储在一个仓库中，该仓库可以在开发者之间共享和访问。每个开发者可以克隆仓库，对文件进行修改和提交。
	（这种分布式方式使得多个开发者可以同时进行独立工作）

	github 是基于git的代码托管平台，一般用户只能使用公共仓库，且代码要公开。

###1.1 git 主要指令
	初始化一个git仓库
	git init

	1、git commit #提交暂存区到本地
	2、git branch (branchname) #创建分支
	3、git checkout (branchname) #切换分支
	4、git merge #合并分支
	(如果分支1和分支2都改了同一处地方，merge之后，git就不知道用哪个了)

###1.2 git 特性（引用）
	1、HEAD #指向你正在其基础上进行工作的提交记录（分离出来）

	git log查看提交记录的哈希值
	2、相对引用
	a.使用^向上移动1个提交记录
	b.使用~<num>向上移动多个提交记录
	eg.main^相当于“main 的 parent 节点”
	git checkout main^

	2、可以使用-f让分支强制指向另一个提交
	eg.git branch -f main HEAD~3

	3、撤销变更
	git reset(本地)/git revert（远程）
	eg.git reset HEAD~1

	4、提交一些复制到当前位置
	git cherry-pick 后面跟提交的名字

##2、github仓库

###2.1 linux环境下通过ssh连接到github
	1.设置git用户和邮箱
	git config --global user.name "junting-123"
	git config --global user.email "791533482@qq.com"

	2.生成SSH密钥
	ssh-keygen -t rsa //直接敲3次回车

	3.在github上添加ssh密钥
	cat /home/junting/.ssh/id_rsa.pub //复制到github上（Settings-->SSH andGPG keys-->New SSH key）,title随意

	4.测试认证是否成功
	[root@localhost data]# ssh -T git@github.com

###2.2 创建和管理存储库
	1、创建README文件 #便于用户理解和导航你工作