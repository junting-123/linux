#Linux学习

##计算机硬件介绍
	CPU--中央处理器--进行逻辑运算和调度其他设备工作
	内存条--存储临时数据
	显卡--处理计算机图形相关工作
	主板--集成电路板，将所有元件连接在一起
	硬盘--磁盘用于存储计算机数据
	cpu处理的数据来源于内存

---输入设备，键盘鼠标，能够发送设备
---输出设备，显示屏
---主机部分，机箱，保护零件

##计算机存储单位
	二进制bit
	常见单位
	bit--位
	byte--字节
	KB---千字节
	GB---千兆字节
	
	8位===1字节
	8bit===1Byte
	1024KB===1MB
	1024MB===1GB
	1024GB===1TB

##硬件
	1.cpu
	服务器cpu在2-4颗，单核cpu是4核，总量在16-256G左右
	2.内存
	a.内存解决的是cpu和磁盘之间的速度不平等，cpu处理过快，磁盘速度太慢，内存是cpu和硬盘间的桥梁
	b.默认下，cpu是从内存中读写数据，内存从磁盘中获取数据
	---内存的容量和处理速度直接决定电脑的数据传输效率
	---内存数据是临时存放，断电数据会丢失，数据重要需要把内存数据写入磁盘，永久保存
	---程序运行时，数据会加载到内存中执行，在断电和重启，数据会自动从内存中释放
	---内存加速（多通道设计）
    内存在厂家设计的时候，如果型号、频率、版本一致的内存条，就能组成多通道设计。

##利用内存提升网站访问效率
	高并发场景下，内存的搭配优化
	网站的流入流量，写入的数据，优先加载到内存中，利用内存告诉读写，当数据到一定数量后，一次性写入磁盘

	优点：适合高并发，高性能网站应用，微博，秒杀活动
	缺点：断电，程序崩溃，数据没来得及写入磁盘，内存数据丢失
	解决办法：使用UPS不间断电源

##挖矿和显卡
	挖矿需要大量的计算芯片，购买大量的显卡设备，能够挖出更多的虚拟币	

##BIOS
	主板设置系统

##云服务器优点，阿里云、腾讯云
	1、操作和升级部署更方便
	2、访问更快
	3、存储更便捷
	4、更安全稳定

##Linux
	开源、自由传播、支持多用户同时操作系统、多任务、支持多CPU、多线程的操作系统
	
	主要运用于服务器端、无人机、物流机器人、嵌入式开发

##为什么用虚拟机？
	1、利用虚拟机安装Linux与真实机器没任何区别
	2、通过ssh命令，通过网络远程连接服务器，进行部署操作
	3、利用虚拟机可创建Linux，练习集群技术
	4、虚拟机操作不会影响宿主机，它是软件技术

环境准备
1、centos7的系统iso镜像文件（阿里云开源镜像网站）
2、VM安装包
3、xshell远程连接工具

##远程连接
	window用户：单独安装xshell或MobaXterm等ssh软件
	Linux用户：使用ssh命令，进行远程安全的加密远程连接

	1、确保ip地址查看正确
	通过ip addr show查看linux网络ip地址
	ip地址为：192.168.216.128

	2、安装xshell软件，并远程连接
	新建会话进行配置

	2、使用ssh进行远程连接
	ssh  root@192.168.216.128  #远程连接命令


##Linux目录

	1、linux目录分隔符特点
	第一个斜杠 代表路径的起点，根目录
	第二个斜杠开始，就是目录之间的一个分隔符

	2、Linux目录结构
	/     #根目录
	/dev  #存放抽象硬件
	/lib  #存放系统库文件
	/sbin  #存放特权级二级制文件
	/var   #存放经常变化的文件
	/home  #普通用户目录
	/etc   #存放配置文件目录
	/boot  #存放内核与启动文件
	/bin   #存放二进制文件（可执行命令）
	/usr   #存放安装程序（软件默认目录）
	/mnt   #文件挂在目录（u盘、光驱）
	/root  #特权用户目录
	/opt   #大型软件存放目录（非强制）

##Linux 核心命令
###cd 命令 
	#change directory 
	cd 可选参数  文件夹

	几个特殊的目录
	. 当前目录
	.. 上级目录
	- 上次目录
	~ 当前系统登录的用户家目录

###ls 
	#list 列出文件夹内容

	命令行  空格  参数（可写可不写）     空格        文件，文件夹（可写可不写）
	ls                                          /opt 根目录下的opt文件夹
	ls           -a  all显示所有文件及隐藏文件     /opt
	ls           -a                         如果不写输出一个点，显示当前文件夹
	ls

基本命令用法一般
1、一般情况，linux参数可选，可写可不写，不同参数作用不一样
2、Linux命令间必须有一个或多个空格

 	-a all的意思，显示所有文件以及隐藏
	-l 详细的输出文件夹中内容
	-h 输出文件大小
	--full-time 显示时间
	-F 在不同文件结尾，输出不同的特殊符号
		以/结尾  文件夹
		以*结尾  可执行文件
		以@结尾  软连接
		普通文件类型，结尾什么都没有

命令提示符
	whoami 我是谁，显示当前登录用户
	hostname 显示当前机器主机名
	pwd 显示当前目录绝对路径

###pwd
	#print work directory 打印工作目录的意思

###su
	#su命令用户切换

	语法
	su - 用户名 # 完全的环境变量用户切换

###logout
	退出当前的用户

###mkdir
	mkdir 文件夹
	mkdir {文件夹1，文件夹2，...}      #创建多个平行文件
	mkdir junting{1..100}
	mkdir  -p ./文件夹1/文件夹2/文件夹3  #创建递进文件夹
	
###touch
	1、创建普通文件，在Linux下后缀格式仅仅是个名字
	2、修改文件时间

###cp
	cp 复制文件 复制之后的文件名  
	cp 复制的文件  ./junting1/  #复制放入其他文件夹
	cp 复制的文件  ./junting1	/JUNTING.txt #复制放入其他文件夹并改名
	

###rm（危险）
	1、mv 命令
	a.mv ./junting.txt ./junting/junting18
	mv 要移动的文件  移动后文件夹
	b.mv junting* ./oldboy
	所有以junting开头的文件，文件夹，都移动到oldboy目录下
	c.mv junting.txt junting.txxt
	移动并改名


	2、rm 命令
	a.rm 普通文件
	b.rm -r 文件夹
	*删除文件夹必须加上-r
	c.rm -d 空文件夹
	d.rm -f 文件夹（强制删除不提示）

###帮助命令
	#man + 命令
	查看帮助，输入q 退出
	#命令  --help
	#help 命令

	#shutdown -r / reboot重启
	#shut down 关机

###vi/vim编辑器
	#ESC + :wq 保存并退出 / :q! 不保存退出
	vim 不存在时，会自动创建
	2、输入i进行输入模式
	#vim 文件 / cat + 文件

###重定向文件
	#cat douyin.txt > ./douyin2.txt（重新覆盖写入）
	#cat douyin.txt >> ./douyin2.txt(追加写入)

###grep 
	过滤字符串命令

###cut
	#cut -c 4-6 alex.txt (每行从第4个切割刀第6个字符)

###sort排序
	#sort -n sort.txt(针对数字从小到大排序，加个r从大到小)


##创建用户流程
	1、useradd chaoge（.bash_profile 用户个人的配置）
	2、系统读取/etc/login.defs(用户定义文件)，和/etc/default/useradd（用户默认配置文件）俩文件中定义的规则创建新用户
	3、向/etc/passwd和/etc/group文件中添加用户和组信息，向/etc/shadow和/etc/gshadow中添加密码信息
	4、根据/etc/default/useradd文件中配置的信息创建用户家目录
	5、把/etc/skel中所有的文件复制到新用户家目录中

	#useradd 用户名 #创建新用户
	#passwd  用户名 #更改用户密码
	#id 用户名      #查看用户的信息
	#userdel -rf chaoge #删除用户
	#w             #查看登录用户
	#last          #登录用户时间详情
	#su - 用户名    
	#sudo          #临时权限变root
	#chmod u+x filename.txt #给文件的user属主添加可执行权限
	#chmod 0 filename.txt   #取消文件所有的权限

	r  #可读权限
	w  #可写权限
	x  #可执行权限

##正则表达式（三剑客）
	1、grep:文本过滤工具
	2、sed:stream editor,流编辑器
	3、awk:Linux的文本报告生成器（格式化文本），linux上是gawk

##grep
	grep [options] [pattern] file
	命令  参数      匹配模式   文件数据
	功能：从文本文件或管道数据流中筛选匹配的行和数据

	参数选项         解释说明
	-v              排除匹配结果
	-n              显示匹配行与行号
	-i              不区分大小写
	-c              只统计匹配的行数
	-E              使用egrep命令
	--color=auto    为grep过滤结果添加颜色
	-w              只匹配过滤的单词
	-o              只输出匹配的内容

##sed
	sed [选项] [sed内置命令字符] [输入文件]

##awk
	awk [option] 'pattern[action]' file
	awk 参数      '条件动作'         文件


##程序包管理器
	程序包
	操作系统发行版本光盘
	文件服务器
	镜像站点	

##rpm命令
	安装软件包
	rpm [OPTIONS] [PACKAGE_FILE]
	#i表示安装 v显示详细过程 h以进度条显示 每个#表示2%进度
	1、rpm -ivh filename.rpm 安装软件
	2、rpm -Uvh filename.rpm 升级软件
	3、rpm -e filename.rpm   卸载软件
	4、rpm -qpi filename.rpm 查询软件描述信息
	5、rpm -qpl filename.rpm 列出软件文件信息
	6、rpm -qf filename      查询文件属于那个RPM的命令格式

##yum命令
	自动解决依赖关系
	Yum,红帽系列rpm包管理工具
	apt-get,deb包管理工具
	zypper,suse的rpm包管理工具

#shell
	shell与用户直接对话，把用户的输入，解释给操作系统
	Linux中常用 *.sh 脚本文件
	shell脚本称为bash shell 程序，通常由vim编辑

	1、赋予脚本可执行权限，以相对绝对路径执行
	2、使用解释器执行
	3、如果没有指定sheban，脚本执行的时候，默认用当前shell去解释

	Linux底层命令都支持shell语句，以及结合三剑客（grep,sed,awk）进行高级用法


