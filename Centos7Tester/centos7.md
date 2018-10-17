# Centos7使用记录 #
[https://www.centoschina.cn](https://www.centoschina.cn)<br>
[http://man.linuxde.net/](http://man.linuxde.net/)<br>
[https://www.linuxprobe.com/chapter-06.html](https://www.linuxprobe.com/chapter-06.html)
> 目录<br>
> [一、文件管理](#1)<br>
> &nbsp;&nbsp;[1.1、tar打包](#1.1)<br>
> &nbsp;&nbsp;[1.2、gzip压缩](#1.2)<br>
> &nbsp;&nbsp;[1.3、zip | unzip](#1.3)<br>
> &nbsp;&nbsp;[1.4、查找文件](#1.4)<br>
> &nbsp;&nbsp;[1.5、删除文件](#1.5)<br>
> &nbsp;&nbsp;[1.6、修改权限](#1.6)<br>
> &nbsp;&nbsp;[1.7、重定向](#1.7)<br>
> &nbsp;&nbsp;[1.8、管道命令符](#1.8)<br>
> [二、安装软件](#2)<br>
> &nbsp;&nbsp;[2.1、RPM工具](#2.2)<br>
> &nbsp;&nbsp;[2.2、yum](#2.2)<br>
> [三、系统管理](#3)<br>
> &nbsp;&nbsp;[3.1、systemctl](#3.1)<br>
> &nbsp;&nbsp;[3.2、ps](#3.2)<br>
> &nbsp;&nbsp;[3.3、top](#3.3)<br>
> [四、文件系统](#4)<br>
> &nbsp;&nbsp;[4.1、基础概念](#4.1)<br>
> &nbsp;&nbsp;[4.2、目录结构](#4.2)<br>
> &nbsp;&nbsp;[4.3、常见命令](#4.3)<br>
> [五、硬盘管理](#5)<br>
> &nbsp;&nbsp;[5.1、基础概念](#5.1)<br>
> &nbsp;&nbsp;[5.2、分区实例](#5.2)<br>
> [六、网络](#6)<br>
> &nbsp;&nbsp;[6.1、防火墙](#6.1)<br>
> &nbsp;&nbsp;&nbsp;&nbsp;[6.1.1、firewalld](#6.1.1)
> &nbsp;&nbsp;&nbsp;&nbsp;[6.1.2、ip](#6.1.2)

<h2 id="1">一、文件管理</h2>
<h3 id="1.1">1.1 tar命令</h3>

tar: 将一组文件打包成一个.tar文件。<br>

下列命令将目录下的所有文件打包成"demo.tar"，-c:创建新包，-f:文件名。<br>
<pre><code># tar -cf demo.tar *</code></pre>

下列命令将一个目录包成"demo.tar"，-c:创建新包，-f:文件名，dir:一个目录<br>
<pre><code># tar -cf demo.tar dir</code></pre>

下列命令列出某个包的所有文件-t:列出文件，-f:文件名。<br>
<pre><code># tar -tf demo.tar
1
2
</code></pre>

下列命令解压出某个包的所有文件-x:解包，-f:文件名。<br>
<pre><code># tar -xf demo.tar
</code></pre>

下列命令将目录下的所有文件打包成"demo.tar.gz"，-z:调取gzip压缩，-v:显示进度，-c:创建新包，-f:文件名。<br>
<pre><code># tar -zvcf demo.tar.gz *</code></pre>

下列命令将解压文件"demo.tar.gz"，并展开包，使用tar命令。 -z: 调取gzip来解压，-v:显示进度，-x:解压包，-f: 指定文件<br>
<pre><code># tar -zvxf demo.tar.gz</code></pre>

[更多...](http://man.linuxde.net/tar)

<h3 id="1.2">1.2 gzip</h3>
gzip: 压缩与解压

下列命令将压缩文件"demo.tar"，压缩后生成demo.tar.gz文件。-f:强行压缩demo.tar。<br>
<pre><code># gzip -f demo.tar</code></pre>

下列命令将解压文件"demo.tar.gz"，解压后生成demo.tar文件，-d:解压缩。<br>
<pre><code># gzip -d demo.tar.gz</code></pre>

下列命令将解压文件"demo.tar.gz"，解压后生成demo.tar文件，-d:解压缩。<br>
<pre><code># gzip -d demo.tar.gz</code></pre>

<h3 id="1.3">1.3 zip | unzip</h3>
zip是一个打包与压缩工具，用unzip解压。<br>

下列命令将目录"dir"，压缩并打包成"dir.zip"文件。-v:显示进度，-r: 递归处理子目录。<br>
<pre><code># zip -vr dir.zip dir</code></pre>

下列命令解压"dir.zip"。<br>
<pre><code># unzip dir.zip</code></pre>

<h3 id="1.4">1.4 查找文件</h3>
find 命令<br>
下列命令查找'/'根目录下所有".txt"结尾的文件。<br>
<pre><code># find / -name *.txt</code></pre>

<h3 id="1.5">1.5 删除文件</h3>
rm 命令<br>
下列命令递归删除"dir"目录下的所有文件。<br>
<pre><code>#  rm -rf dir</code></pre>
下列命令删除当前目录的所有日志文件。<br>
<pre><code>#  rm -f *.log</code></pre>

<h3 id="1.6">1.6 修改权限</h3>
chmod 命令<br>
**三种角色类型定义：**<br>
u:User，文件或目录的所有者<br>
g:group,即文件或目录的所属群组<br>
o:other:其他用户<br>
**三种权限类型定义**:<br>
x:数字1,执行权限<br>
w:数字2,写入权限<br>
r:数字4,读取权限<br>
**多个权限为1、2、4的逻辑或**<br>
下列命令修改文件"test"，所有用户读取权限
<pre><code># chmod 444 test</code></pre>

<h3 id="1.7">1.7 重定向</h3>

*命令*

	[命令] > 1.log #指定标准输出为"1.log"，并清空1.log的值
    [命令] >> 1.log #指定标准输出为"1.log"，并追加到末尾

    [命令] 2> 1.log #指定错误输出为"1.log"，并清空1.log的值
    [命令] 2>> 1.log #指定错误输出为"1.log"，并追加到末尾

*实例*

	ip addr > ip.log #将网卡信息写入 ip.log
    ping www.qq.com > ping.log #将ping的结果信息写入 ping.log

    echo 'line1' > log.log # 将'line1'写入log.log，如果文件存在，则清空
	echo 'line2' >> log.log # 将'line2'追加到log.log

上面的实例虽然改变了标准输出，但对于执行错误的信息，依旧会打印到屏幕上。

	ls /dd > ls.log #枚举一个不存在的目录，依然会在屏幕中打印错误信息。
    ls /dd 2> ls.log #枚举一个不存在的目录，将错误信息写入文件。
    ls /dd &> ls.log #将错误信息和标准信息，写入文件。

<h3 id="1.8">1.8 管道命令符</h3>
	

	[命令A] | [命令B] # 将前A命令的输出做为B命令的输入

*实例*

	ls / |grep dev #从ls命令的输出结果中匹配"dev"，支持通配符
	ls / |tr [a-z] [A-Z] #从ls命令的输出结果中，将小写替换成大写

<h2 id="2">二、安装软件</h2>
<h3 id="2.1">2.1 RPM工具</h3>
RPM全称"Redhat Package Manager"，它在本地系统中，以数据库的形式记录了本机的RPM包，以及包之间的依赖关系。RPM包是预先在linux机器上编译并打包的文件，安装快捷。但它**不处理包之间的依赖关系**，以及安装环境必须与编译环境一致。

	rpm -qa #列出系统中安装的所有包
    rpm -ql [包名称] #列出某个包的所有文件

<h3 id="2.2">2.2 yum</h3>
YUM是基于rpm的软件包管理器，它自动处理包之间的依赖关系。

	yum search [包名称] #查找指定的包
    yum install -y [包名称] #安装包
    yum list # 列出所有包（包括未安装的）
    yum localinstall [包名称] #安装本地rpm包

<h2 id="3">三、系统管理</h2>
<h3 id="3.1">3.1 systemctl</h3>
**systemctl**对系统服务的启动、停止等管理。<br>
下列命令查看系统所有服务

	systemctl -al

下列命令查看某个系统服务

	systemctl status firewalld

下列命令启动某个服务

	systemctl start firewalld

下列命令停止某个服务

	systemctl stop firewalld

下列命令设置某个服务开机启动

	systemctl enable firewalld

下列命令禁用某个服务的开机启动

	systemctl disable firewalld 

注册服务<br>
参考: [http://www.jinbuguo.com/systemd/systemd.service.html](http://www.jinbuguo.com/systemd/systemd.service.html)<br>

<h3 id="3.2">3.2 ps</h3>
用于查看系统进程

	ps -ef # 查看所有进程，并线程命令行

<h3 id="3.3">3.3 top</h3>
查看系统状态，包括CPU、内存等。

	top #显示系统状态

![](https://i.imgur.com/5ye6YBf.png)

**第一行**：<br>
00:11:55 当前系统时间<br>
up, 1:27 系统运行时间<br>
2 users 当前有2个用户登录系统<br>
**load average**: 3.06,3.01, 1.79 load average后面的三个数分别是1分钟、5分钟、15分钟的负载情况。
**load average**数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。如果这个数除以逻辑 CPU的数量，结果高于5的时候就表明系统在超负荷运转了。<br>

**第二行**： Tasks 任务（进程）<br>
系统现在共有109个进程，其中处于运行中的有1个，108个在休眠（sleep），stoped状态的有0个，zombie状态（僵尸）的有0个。<br>

**第三行**：cpu状态
**us** 用户空间占用CPU的百分比。<br>
**sy** 内核空间占用CPU的百分比。<br>
**ni** 改变过优先级的进程占用CPU的百分比<br>
**id** 空闲CPU百分比<br>
**wa** IO等待占用CPU的百分比<br>
**hi** 硬中断（Hardware IRQ）占用CPU的百分比<br>
**si** 软中断（Software Interrupts）占用CPU的百分比<br>

**第四行**：内存状态<br>
**total** 物理内存总量<br>
**used** 使用中的内存总量<br>
**free** 空闲内存总量<br>
**buffers** 缓存的内存量<br>

**第五行**：swap交换分区<br>
total 交换区总量<br> 
used 使用的交换区总量<br>
free 空闲交换区总量<br>
cached 缓冲的交换区总量<br>


**第七行以下**：各进程（任务）的状态监控
PID 进程id<br>
USER 进程所有者<br>
PR 进程优先级<br>
NI nice值。负值表示高优先级，正值表示低优先级<br>
VIRT 进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES<br>
RES 进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA<br>
SHR 共享内存大小，单位kb<br>
S 进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程<br>
%CPU 上次更新到现在的CPU时间占用百分比<br>
%MEM 进程使用的物理内存百分比<br>
TIME+ 进程使用的CPU时间总计，单位1/100秒<br>
COMMAND 进程名称（命令名/命令行）<br>

**多U多核CPU监控**<br>
在top基本视图中，按键盘数字1，可监控每个逻辑CPU的状况

<h2 id="4">四、文件系统</h2>

<h3 id="4.1">4.1、基础概念</h3>
在Linux系统中，目录、设备、套接字、打印机等都被抽象成了文件。从“根（/）”目录开始（不同与windows的从盘符开始），采用树形结构来存放文件和目录。目录可以单独挂载到不同磁盘的不同分区。 

![](https://i.imgur.com/uIkAal0.png)

linux支持多种文件系统,常见的如:**ext4**，**xfs**。在磁盘分区后，需要在每个分区上建立文件系统，才能使用。可以理解这些文件系统提供了对磁盘的读取和写入。linux内核抽象出了**VFS**（Virtual File System，虚拟文件系统）接口，提供了统一的API，来操作不同的文件系统。
![](https://i.imgur.com/HPS4fOQ.png)

<h3 id="4.2">4.2、目录结构</h3>
/bin 二进制可执行命令

/dev 设备特殊文件

/etc 系统管理和配置文件

/etc/rc.d 启动的配置文件和脚本

/home 用户主目录的基点，比如用户user的主目录就是/home/user，可以用~user表示

/lib 标准程序设计库，又叫动态链接共享库，作用类似windows里的.dll文件

/sbin 系统管理命令，这里存放的是系统管理员使用的管理程序

/tmp 公用的临时文件存储点

/root 系统管理员的主目录（呵呵，特权阶级）

/mnt 系统提供这个目录是让用户临时挂载其他的文件系统。

/lost+found 这个目录平时是空的，系统非正常关机而留下“无家可归”的文件（windows下叫什么.chk）就在这里

/proc 虚拟的目录，是系统内存的映射。可直接访问这个目录来获取系统信息。

/var 某些大文件的溢出区，比方说各种服务的日志文件

/usr 最庞大的目录，要用到的应用程序和文件几乎都在这个目录。其中包含：

/usr/X11R6 存放X window的目录

/usr/bin 众多的应用程序

/usr/sbin 超级用户的一些管理程序

/usr/doc linux文档

/usr/include linux下开发和编译应用程序所需要的头文件

/usr/lib 常用的动态链接库和软件包的配置文件

/usr/man 帮助文档

/usr/src 源代码，linux内核的源代码就放在/usr/src/linux里

/usr/local/bin 本地增加的命令

/usr/local/lib 本地增加的库

<h3 id="4.3">4.3、常用命令</h3>

*du* : 查看文件和目录大小

	du -sh / #显示指定文件或目录的大小
    du -sh /* #显示指定文件夹下所有子目录的大小

<h1 id="5">五、硬盘管理</h1>
<h3 id="5.1">5.1、基础概念</h3>
linux在"/dev/"目录下保存所有的磁盘设备文件，常见的有"hd":ide硬盘,"sd":sata硬盘,'vd':虚拟硬盘。

*硬盘*

	fdisk -l #查看硬盘信息

![](https://i.imgur.com/ZriFJ2Q.png)

在上图中，可以看到磁盘名称为"/dev/sda"，分区名称为:"/dev/sda1-3"各部分名称解释如下：

![](https://i.imgur.com/AnXNckf.png)

*分区*

硬盘设备是由大量的扇区组成的，每个扇区的容量为512字节。其中第一个扇区最重要，它里面保存着主引导记录与分区表信息。就第一个扇区来讲，主引导记录需要占用446字节，分区表为64字节，结束符占用2字节；其中分区表中每记录一个分区信息就需要16字节，这样一来最多只有4个分区信息可以写到第一个扇区中，这4个分区就是4个**主分区**。

![](https://i.imgur.com/6XAcj6f.png)

从上图可以看出，在分区表中最多只能有4个分区，如果需要更多的分区，可以将其中一个分区做为**扩展分区**，它存储指向下一个扇区（扩展分区表，这里只是个人的理解）的指针，新扇区存储的分区信息称为**逻辑分区**。分区建立后，需要格式化（建立文件系统ext4,xfs..）。

![](https://i.imgur.com/p0tiDYq.png)

*挂载*

将一个磁盘分区关联到一个已经存在的目录。在centos中，使用**mount**命令挂载文件系统(临时),在"/etc/fstab"中存储已经挂载目录信息（永久）。

<h3 id="5.2">5.2、分区实例</h3>


在虚拟机中(WMware)添加硬盘，并完成挂载。<br>
1、添加硬盘，添加步骤略（需关闭虚拟机）。

![](https://i.imgur.com/yl1yIGw.png)

2、开机，并查看硬盘信息

![](https://i.imgur.com/2BN9p4a.png)


3、分区

使用**fdisk**对磁盘分区，参数说明:

>m:查看全部可用的参数<br>
>n:添加新的分区<br>
>d:删除某个分区信息<br>
>l:列出所有可用的分区类型<br>
>t:改变某个分区的类型<br>
>p:查看分区表信息<br>
>w:保存并退出<br>
>q:不保存直接退出<br>


![](https://i.imgur.com/i4fkGFA.png)

4、格式化

**mkfs**对分区格式化（建立文件系统），在命令中输入"mkfs"，按两次"tab"键，会列出所有支持的文件系统。

![](https://i.imgur.com/0M094d1.png)

这里选择ext4，对分区格式化。

![](https://i.imgur.com/NesfxiF.png)	

5、挂载

**mount**对格式化的磁盘挂载到一个已存在的目录，格式"mount [分区] [目录]"，例如:

	mount /dev/sdb1 /fs/sdb1/ #将分区/dev/sdb1挂载到目录/fs/sdb1/

6、开机自动挂载

在/etc/fstab中写入需要挂载的分区。格式："设备文件 挂载目录 格式类型 权限选项 是否备份(0|1) 是否自检(0|1)"。

	
7、查看分区挂载和使用率

	df -h

![](https://i.imgur.com/WUElUxH.png)

<h2 id="6">六、网络</h2>

<h3 id="6.1">6.1、防火墙</h3>

<h3 id="6.1.1">6.1.1、firewalld</h3>

*定义*

firewalld是一个防火墙配置工具，方便用户定义防火墙规则，底层依赖netfilter来实现规则。 

*zone*

使用zone(区域)来定义一组规则，并可以将它绑定到一个网卡上，方便快速切换不同的策略。可以在"/etc/firewalld/zones/"目录中，查看所有区域的定义，以及各个区域的规则。

*实例*

	firewall-cmd --get-default-zone #查看默认区域
	
	firewall-cmd --get-zone-of-interface=ens33 #查看网卡"ens33"的区域

    firewall-cmd --permanent --set-default-zone=public #设置默认区域为public,--permanent:为永久有效
    firewall-cmd --reload #立即生效 

	firewall-cmd --permanent --zone=public --add-port=27017/tcp #为public区域增加开放端口
    firewall-cmd --reload #立即生效 

    firewall-cmd --permanent --zone=public --remove-port=27017/tcp #移除端口
    firewall-cmd --reload #立即生效

    firewall-cmd --info-zone=public #查看public区域基础信息

	firewall-cmd --permanent --zone=public --add-forward-port=port=888:proto=tcp:toport=22:toaddr=192.168.10.10 #端口转发    

备注:使用firewalld配置的防火墙策略默认为运行时（Runtime）模式，又称为当前生效模式，而且随着系统的重启会失效。如果想让配置策略一直存在，就需要使用永久（Permanent）模式。

<h3 id="6.1.2">6.1.2、ip</h3>

	ip addr add [ip] dev [网卡] #给一个网络接口添加IP地址
	ip addr del [ip] dev [网卡] #给一个网络接口删除IP地址
    ip addr #显示所有网卡信息