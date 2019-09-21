#	shell基本命令

##	1、Shell

shell提供了你与操作系统之间通讯的方式。这种通讯可以以交互方式（从键盘输入，并且可以立即得到响应），或者以shell script(非交互）方式执行。shell script是放在文件中的一串shell和操作系统命令，它们可以被重复使用。本质上，shell script是命令行命令简单的组合到一个文件里面

Shell基本上是一个命令解释器，类似于DOS下的command。它接收用户命令（如ls等），然后调用相应的应用程序。较为通用的shell有标准的Bourne shell (sh）和C shell (csh）

###	1.1、交互式shell和非交互式shell

交互式模式就是shell等待你的输入，并且执行你提交的命令。这种模式被称作交互式是因为shell与用户进行交互。这种模式也是大多数用户非常熟悉的：登录、执行一些命令、签退。当你签退后，shell也终止了。

shell也可以运行在另外一种模式：非交互式模式。在这种模式下，shell不与你进行交互，而是读取存放在文件中的命令，并且执行它们。当它读到文件的结尾，shell也就终止了

用cat /etc/shells查看安装了哪些Shell 

 ### 1.2、常见的GUI(图形用户接口) Shell  

1、Gnome：  包含了 Panel （用来启动此程式和显示目前的状态）、桌面 （应用程式和资料放置的地方）及一系列的标准桌面工具和应用程式，并且能让各个应用程式都能正常地运作，是Linux操作系统上最常用的图形桌面环境之一  

2、KDE：  K桌面环境(K Desktop Environment)的缩写。一种著名的运行于 Linux、Unix 以及FreeBSD等操作系统上的自由图形桌面环境，整个系统采用的都是 TrollTech 公司所开发的Qt程序库（现在属于Digia公司）。KDE是Linux 操作系统上流行的桌面环境之一。KDE 是一个网络透明的现代化桌面环境，支持Linux、 FreeBSD、Unix、其它类Unix、Mac OS X和微软的Windows  

3、Xface：  xFace是开源的基于Web技术的移动应用开发平台，允许开发者使用HTML、CSS及JavaScript技术开发智能移动终端的应用程序 

 ### 1.3、常见的CLI(命令行界面) Shell  

**sh:** Bourne shell(是一个交换式的命令解释器和命令编程语言), 史蒂夫·伯恩在⻉尔实验室时编写。1978年随Version 7 Unix⾸次发布  

**csh:** C shell,主要是为了让用户更容易的使用交互式功能，并把ALGOL风格的语法结构变成了C语言风格。 ⽐尔·乔伊在加州⼤学伯克利分校时编写。1979年随BSD⾸次发布。  bash: Bourne-Again shell, 1987年由布莱恩·福克斯为了GNU计划⽽编写。原先是计划⽤在GNU操作系统上，但能运⾏于⼤多数类Unix系统的操作系统之上，包括Linux 与 MacOS 都将它作为默认shell。是应⽤最⼴的 Shell 

**zsh:** Z shell, 名称的含义是 “The last shell you’ll ever need!”，Zsh 对 Bourne shell做出了⼤量改进，同时加⼊了其他shell的某些功能，强化了⾃动补全功能，还加⼊了插件机制，定制性⾮常⾼，功能最为强⼤  

##	2、Bash快捷键

**ctrl + f ：前进一个字符**

**ctrl + b：后退一个字符**

**ctrl + a ：回到行首**

**ctrl + e ：回到行尾**

**ctrl + w ：向左删除一个单词**

**ctrl + u ：向左删除全部**

**ctrl + k ：向右删除全部**

**ctrl + y ：粘贴上次删除的内容**

**ctrl + l ：清屏**

**ctrl + c ：终结一个前台作业**

**ctrl + i ：水平制表符**

**ctrl + o ：产生一个新行**

##	3、目录结构

Linux 采用了一种不同的方式, 在路径名中不使用驱动器盘符。在 Linux 中,你会看到下面这种路径: /home/Rich/Documents/test.doc ,路径本身并没有提供任何有关文件究竟存放在哪个物理磁盘上的信息

Linux虚拟目录中比较复杂的部分是它如何协调管理各个存储设备。在Linux PC上安装的第一块硬盘称为根驱动器。根驱动器包含了虚拟目录的核心,其他目录都是从那里开始构建的

![1](/home/w/总结/Day02/1.jpg)

```
/					系统根目录,通常不会在这里存储文件
boot				启动目录
bin 				系统二进制目录,存放普通用户级的GNU命令
sbin 				系统超级二进制目录,存放管理员级别的GNU命令
usr 				资源目录 (User System Resources)
	bin 			用户二进制目录,存放用户级的GNU命令
	sbin 			用户超级二进制目录,存放管理员用户的GNU命令
	local
		bin
		sbin
opt					第三方开发的程序 (option), 意为选装
dev 				设备目录
	null			无底洞 (丢弃一切写入其中的数据)
	zero 			无限0数据流 (常用来产生一个特定大小的空白文件, 或安全销毁文件)
	shm 			内存文件夹
	random 			随机数发生器
	urandom 		非阻塞的随机数发生器
etc 				系统配置文件目录 (et cetera)
proc 				当前的进程、运行状态信息的目录
root 				管理员家目录
home 				用户的家目录
media 				媒体目录,可移动媒体设备的常用挂载点,一般是系统自动挂载到这里
mnt 				挂载目录,另一个可移动媒体设备的常用挂载点,一般是留给用户手动挂载
lib					系统库目录,存放系统和应用程序的库文件
srv 				服务目录,存放本地服务的相关文件
sys 				系统目录,存放系统硬件信息的相关文件
run 				运行目录,存放系统运作时的运行时数据
tmp 				临时目录,可以在该目录中创建和删除临时工作文件
var 				可变目录,用以存放经常变化的文件,比如日志文件
```

###	3.1、目录操作

绝对路径：/usr/local/bin

相对路径：../foo/bar

```
pwd					显示当前目录的绝对路径
ls ./				显示当前目录的文件
ls -l ./			以列表形式显示文件
ls -lh ./			以人类友好的方式显示文件列表
ls -A ./			显示隐藏文件
cd XXX				切换文件目录
cd -				回到上一次所在的位置
mkdir abc			创建名为abc的目录
mkdir -p a/b/c		创建三层目录结构a/b/c
rmdir				删除一个空的目录
```

###	3.2、文件操作

**cp/mv/rm的通用参数**

-i：覆盖前面的提示

-n：如果目标文件已存在，则停止操作

-f：如果目标文件已存在，则强制操作，覆盖前不提示

-r：递归对文件夹执行某操作(mv不需要-r)

```
cp aa ../bb/		将aa文件移动到../bb目录
mv aa ../bb			将aa文件移动到../并更名为bb
rm foo				删除名为foo的文件
rm -r foo			删除文件夹				
touch abc			在当前文件夹创建一个abc文件，如果已存在则跳过
ln -s abc def		为abc文件创建一个软连接
alias				自定义别名
```

**history**

bashrc配置显示时间：export HISTTIMEFORMAT="[%y-%m-%d_%T]

修改bashrc后使其生效：source ~/.bashrc 或 . .bashrc

**ln命令详解**

它的功能是为某一个文件在另外一个位置建立一个同步的链接

####	3.2.1、硬链接：ln foo bar

它会在你选定的位置上生成一个和源文件大小相同的文件

只能在同一个分区内创建

一个文件的多个硬链接相当于一个文件有多个名字，多个硬链接在磁盘上只占用一个文件的大小

修改硬链接时，所有同源的硬链接都会发生改变

####	3.2.2、软连接：ln -s foo bar

ln –s 源文件 目标文件

它只会在你选定的位置上生成一个文件的镜像，不会占用磁盘空间

也可跨分区创建

内部只记录目标文件的路径，类似于Windows下的快捷方法

通过软连接修改文件，源文件也会发生修改

**查看文件内容：**

```
cat  		由第一行开始显示文件内容
tac  		从最后一行开始显示，可以看出 tac 是 cat 的倒着写
nl   		显示的时候，顺道输出行号
more 		一页一页的显示文件内容
head 		只看头几行
tail 		只看尾巴几行
less 与 more 类似，但是比 more 更好的是，他可以往前翻页
```

##	4、文件压缩

###	4.1、tar

可以将多个文件合并为一个文件，打包后的文件后缀亦为tar。tar文件格式已经成为POSIX标准

格式是：tar 功能 选项 文件

**压缩：tar -czf abc.tar.gz abc/**

**解压：tar -xzf abc.tar.gz**

-c：create 创建新的tar文件

-x：extract、get 解开tar文件

-t：list 列出tar文件中包含的文件的信息

-r：append 附加新的文件到tar文件中

-u：update 用已打包的文件的较新版本更新tar文件

-A：catenate、concatenate 将tar文件作为一个整体追加到另一个tar文件中

-d：diff、compare 将文件系统里的文件和tar文件里的文件进行比较

-delete： 删除tar文件里的文件。注意，这个功能不能用于已保存在磁带上的tar文件

###	4.2、zip

**压缩：zip -r abc.zip abc/**

**解压：unzip abc.zip**

```
-n				  指定压缩比
-t				  把压缩文件的日期设成指定的日期
-F 				  尝试修复已损坏的压缩文件
-g 				  将文件压缩后附加在既有的压缩文件之后，而非另行建立新的压缩文件
-L 				  显示版权信息
```

将 /home/html/ 这个目录下所有文件和文件夹打包为当前目录下的 html.zip

```
zip -q -r html.zip /home/html
```

如果在我们在 /home/html 目录下，可以执行以下命令

```
zip -q -r html.zip *
```

从压缩文件 cp.zip 中删除文件 a.c

```
zip -dv cp.zip a.c
```

##	5、find文件查找

用来在指定目录下查找文件，任何位于参数之前的字符串都将被视为欲查找的目录名，如果使用该命令，不设置任何参数，则find命令将在当前目录下查找子目录遇文件，并查找的内容全部显示出来

查找当前文件夹下的全部文件：find ./

只查找文件：find ./ -type f

只查找目录：find ./ -typr d

只查找链接：find ./ -type l

按名称查找：find ./ -name '*.py'

按文件大小查找：find ./ -size +1k -size -5k

按权限查找：find ./ -perm 0644

```
-grep
	参数：
		-i：忽略大小写
		-I：忽略二进制文件
		-r：递归查找目录
		-n：打印行号
		-c：只显示匹配到的个数
		-l：只显示匹配到的文件列表
		-o：只显示匹配到的单词
		-v：忽略制定的字段
		-E：通过正则表达式匹配
		--include=‘*.py’仅包含py文件
		--exclude=‘*.js’不包含js文件
find DIR -name ‘*.XXX’找到目录下的所有名字匹配的文件
which		精确查找当前可执行的命令
whereis		查找所有匹配的命令
```

找到文件夹/tmp/xyz/x下所有的权限为642，大小在10K到100K之间的log文件

```
find /tmp/xyz/ -perm 0642 -size +10K -size -100K -name '*.log'
```

##	6、echo

echo命令的功能是在显示器上显示一段文字，一般起到一个提示的作用

```
显示字符串：
echo ‘It is a test’
结果是：
It is a test
```



















