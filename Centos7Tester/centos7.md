# Centos7使用记录 #
[https://www.centoschina.cn](https://www.centoschina.cn)<br>
[http://man.linuxde.net/](http://man.linuxde.net/)
> 目录<br>
> [一、文件管理](#1)<br>
> &nbsp;&nbsp;[1.1、tar打包](#1.1)<br>
> &nbsp;&nbsp;[1.2、gzip压缩](#1.2)<br>
> &nbsp;&nbsp;[1.3、zip | unzip](#1.3)<br>
> &nbsp;&nbsp;[1.4、查找文件](#1.4)<br>
> &nbsp;&nbsp;[1.5、删除文件](#1.5)<br>
> &nbsp;&nbsp;[1.6、修改权限](#1.6)<br>
> [二、安装软件](#2)<br>
> &nbsp;&nbsp;[2.1、RPM工具](#2.2)<br>
> &nbsp;&nbsp;[2.2、yum](#2.2)<br>
> [三、系统管理](#3)<br>
> &nbsp;&nbsp;[3.1、systemctl](#3.1)<br>

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

下列命令解压出某个包的所有文件-x:解压，-f:文件名。<br>
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


<h2 id="2">二、安装软件</h2>
<h3 id="2.1">2.1 RPM工具</h3>
RPM全称"Redhat Package Manager"，它在本地系统中，以数据库的形式记录了本机的RPM包，以及包之间的依赖关系。RPM包是预先在linux机器上编译并打包的文件，安装快捷。但它**不处理包之间的依赖关系**，以及安装环境必须与编译环境一致。

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



