#	1、系统管理

##	1.1、查看进程状态

Linux是一个多任务操作系统，同一时刻允许多个任务同时工作，运行中的每一个任务就是一个进程

###	1.1.1、ps命令

ps(process status)：用来chakan 进程的状态，显示的是执行代码那一瞬间的进程状态

```
w@W-PC:~$ ps
  PID TTY          TIME CMD
32447 pts/0    00:00:00 bash
32456 pts/0    00:00:00 ps
```

ps命令支持三种不同类型的命令参数：

Unix的参数：前面加 -，如ps -ef

BSD的参数：前面不加-，如ps aux

GNU的参数：前面加--，如ps --pid 666

**ps -ef**

-e：参数制定显示所有运行在系统上的进程

-f：参数扩展了输出

```
w@W-PC:~$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 20:03 ?        00:00:02 /sbin/init splash
root         2     0  0 20:03 ?        00:00:00 [kthreadd]
```

```
UID：			启动这些集成的用户
PID：			进程的ID
PPID：			父进程的进程号
C：				进程生命周期中的CPU使用率
STIME：			进程启动时的系统时间
TTY：			进程启动时的终端设备
TIME：			程序累计占用CPU的时间
CMD：			进程运行的命令
```

**ps aux**

a：显示跟任意终端关联的所有进程

u：采用基于用户格式显示

x：显示所有的进程，包括未分配任何终端的进程

```
w@W-PC:~$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 225440  9236 ?        Ss   20:03   0:02 /sbin/init splash
root         2  0.0  0.0      0     0 ?        S    20:03   0:00 [kthreadd]
```

```
USER：			执行这个进程的用户
PID：			进程ID
%CPU：			当前进程的CPU占用
%MEM：			当前进程的内存占用
VSZ：			进程占用的虚拟内存大小，以KB为单位
RSS：			进程占用的物理内存大小
TTY：			进程启动时的终端设备
STAT：			进程状态
START：			进程启动时刻
TIME：			程序累计占用CPU的时间
COMMAND：			启动进程的命令
```

**关于STAT**

+ 代表当前进程状态的双字符状态码
+ 第一个字符表示进程的状态

```
O：				代表正在运行
S：				代表在休眠
R：				代表可运行，正在等待CPU
Z：				代表僵化，进程已结束但父进程已经不存在了
T：				代表停止
```

+ 第二个参数进一步说明进程的状态

```
<：				该进程运行在高优先级上
N：				该进程运行在低优先级上
L：				该进程有⻚面锁定在内存中
S：				该进程是控制进程			
1：				该进程是多线程的
+：				该进程运行在前台
```

###	1.1.2、top命令

top可以持续查看进程的状态

```
top - 22:09:55 up  2:06,  1 user,  load average: 0.64, 0.72, 0.61
Tasks: 191 total,   1 running, 189 sleeping,   0 stopped,   1 zombie
%Cpu(s):  2.0 us,  0.7 sy,  0.0 ni, 97.1 id,  0.2 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7862.6 total,    705.9 free,   1398.7 used,   5758.0 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   5750.0 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND              
 1206 root      20   0  485964 156860 120176 S   5.3   1.9   6:40.68 Xorg                 
 2199 w         20   0  612864  40764  30764 S   2.7   0.5   0:00.35 deepin-terminal      
 3304 w         20   0 1093272 151760  73356 S   1.7   1.9   4:09.48 deepin-wm       
```

**头信息**

```
1、系统运行的整体状态: 开机时⻓,登陆用户数,系统负载
系统负载：load averange：0.00,0.02,0.05
分别代表：一分钟负载，五分钟负载，十五分钟负载
负载值越高代表服务器压力越大
负载值不要超过CPU的核心数，如果超过了意味着很多进城在等待使用CPU
与uptime命令的结果一样(查看系统状态)
2、任务情况: 任务总数,运行中的数量,休眠数量,停止数量,僵尸进程数量
3、CPU使用情况
user(us)用户态占用
system(sy)内核态占用
idle(id)空闲的CPU
4、内存占用情况: 内存总量, 空闲内存, 使用的内存, 缓冲区占用的内存
5、交换空间的占用
交换分区是一种将内存数据保存到硬盘的技术,一般在内存不足的时候使用
```

**进程区信息**

```
PID：进程的ID
USER: 进程属主的名字
PR: 进程的优先级
NI: 进程的谦让度值
VIRT: 进程占用用的虚拟内存总量量
RES: 进程占用用的物理理内存总量量
S: 进程的状态 (与 ps 基本相同)
%CPU: 进程使用用的CPU时间比比例例
%MEM: 进程使用用的内存占可用用内存的比比例例
TIME+: 自自进程启动到目目前为止止的CPU时间总量量
COMMAND: 进程所对应的命令行行行名称,也就是启动的程序名
```

**进程太多时,可以通过 -p 参数指定需要查看的进程ID**

```
top -p PID1,PID2,PID3,...
```

###	1.1.3、htop命令

安装：sudo apt install htop

![1](/home/w/总结/Day04/1.png)

#	2、进程的管理

##	2.1、kill

kill：杀死进程或者给进程发信息

​	-1(HUP)：平滑重启

​	-9(KILL)：强制杀死进程

​	-15(TERM)：正常终止进程(kill的默认信号)

pkill：按名字处理进程

killall：处理名字匹配的进程

#	 3、其他状态

##	3\.1内存状态

可以通过 -m 或 -g 参数调整 free 命令显示数值的单位

```
w@W-PC:~$ free
              total        used        free      shared  buff/cache   available
Mem:        8051336     1441572      648024      435872     5961740     5865028
Swap:             0           0           0
```

##	3.2、硬盘

iostat : 查看硬盘写入和读取的状态

df -lh : 查看硬盘分区，及每个分区的剩余空间

du -hs ./ : 查看当前目录占用的硬盘大小

##	3.3、网络状态

ifconfig ：查看网卡状态, 常用用来检查自身 IP 地址

netstat -natp： 查看网络连接状态

```
-a : 显示所有选项
-t : 显示所有与TCP相关的选项
-u : 显示所有与UDP相关的选项
-x : 显示所有与Unix域相关的套接字选项
-n : 拒绝显示别名,能显示数字的全部转换为数字显示
-p : 显示建立相关连接的程序名
-l : 显示所有状态为Listen的连接
-e : 显示扩展信息,如当前链接所对应的用户
-c : 间隔一段时间执行一次netstat命令
-s : 显示统计信息。对每种类型进行汇总
```

**ping -i 0.5 -c 100 xxx.xxx.xxx.xxx**

```
-i : 间隔
-c : 数量
-q : 安静模式，只打印结果
```

```
lsof -i :			 看占用用端口口的程序
lsof -i tcp：		查看所有 TCP 连接
lsof -u abc：		查看用用户 abc 打开的所有文文件
lsof -p 123：		查看 pid 为 123 的进程打开的所有文文件
```

**路由追踪: traceroute [HOST]**

DNS查询

```
dig 
host 
```

##	3.4、时间和日期

date：查看日期与时间

cal：查看日历

##	3.5、下载

curl：执行HTTP访问

wget：下载文件

scp：在服务器之间上传或下载文件：scp root@x.x.x.x:/root/abc ./abc