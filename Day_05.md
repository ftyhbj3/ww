#	1、Shell编程

##	1.1、Shell脚本

通过Shell中的各种命令，开发者和运维人员可以对服务进行维护工作

Shell脚本一般是以 .sh结尾的文本文件，也可省略扩展名

##	1.2、脚本首行

在Shell脚本中，#开头的是文本注释，但是#！开头的这句话比较特殊，他会告诉Shell应该使用哪个程序执行当前脚本

常见的：

```
#!/bin/sh
#!bin/bash
#!/user/bin/env bash
```

##	1.3、第一个脚本

创建cpu-count.sh文件，并通过vim写入

```
#/bin/bash

echo "Hello"
echo "I am `whomi`"
echo "I love Linux"
echo "The CPU in my PC has `cat /proc/cpuinfo |grep -c processor` cores"
exit 0
```

执行chmod a+x cpu-count.sh 对脚本授予可执行的权限

输入 ./cpu-count.sh 执行脚本

查看脚本的退出状态：echo $?

```
Linux中的所有程序执行结束后的所有状态码
状态码为 0 表示正常，正整数表示异常退出
```

#	2、变量

##	2.1、定义

变量的定义与其他语言差距不大，需要注意的是赋值前后没有空格

```
a=1
b=mmm
```

##	2.2、使用

变量的使用，在变量名前面加上 $ 符号

```
echo "---$a---\n===$b==="
printf "---$a---\n===$b===\n"
```

##	2.3、引号的差别

```
echo "---$a---\n===$b==="

------\n======

echo '---$a---\n===$b==='

---$a---\n===$b===
```

##	2.4、定义Shell的全局变量

定义：export ABC=666

在终端运行：soutce ./test.sh

##	2.5、常用环境变量

```
$PATH : 		可执行文件目录
$PWD : 			当前目录
$HOME : 		家目录
$USER : 		当前用户名
$UID : 			当前用户的 uid
```

#	3、if语句

```
if command
then
	commands
elif command
then
	commands
else
	commands
fi
```

if 语句检查判断的依据实际上是, 后面所跟命令的状态码: 

0 为 true, 其他值为 false

```
if ls /x
then
	echo 'exist x'
else
	echo 'not exist x'
fi
```

条件测试命令：

shell 提供了一种专用做条件测试的语句[]

这一对方括号本质上是一个命令, 里面的条件是其参数, 所以 [] 的前面和后面必须有空格, 否则会报错

他有三种比较方法：

```
if [ condition ]
then
	commands
fi
```

**数值比较**

```
n1 -eq n2		检查n1是否与n2相等
n1 -ge n2		检查n1是否大于或等于n2
n1 -gt n2		检查n1是否大于n2
n1 -le n2		检查n1是否小于或等于n2
n1 -lt n2		检查n1是否小于n2
n1 -ne n2		检查n1是否不等于n2
```

**字串比较**

```
str1 = str2			检查str1是否和str2相同
str1 != str2		检查str1是否和str2不同
str1 < str2			检查str1是否比str2小
str1 > str2			检查str1是否比str2大
-n str1				检查str1的⻓度是否非0
-z str1				检查str1的⻓度是否为0
```

**文件比较**

```
-d file				检查file是否存在并是一个目录
-e file				检查file是否存在
-f file				检查file是否存在并是一个文件
-r file				检查file是否存在并可读
-w file				检查file是否存在并可写
-x file				检查file是否存在并可执行
-s file				检查file是否存在并非空
-O file				检查file是否存在并属当前用户所有
-G file				检查file是否存在并且默认组与当前用户相同
file1 -nt file2		检查file1是否比file2新
file1 -ot file2		检查file1是否比file2旧
```

#	4、for循环语句

Shell 中的循环结构有三种: for 、 while 和 until , 这里重点介绍 for 循环

seq START END 语句用来产生一个数字序列

2. $[ NUM1 + NUM2 ] 语句用来进行基本的数学运算
3. [[ ... ]] 语句用来更方便的进行比较判断

格式：

```
for 变量 in 序列 do
	要执行的命令
done
```

#	5、函数

  定义时 function 不是必须的,可以省略

```
function foo() {
	echo "---------------------------"
	echo "Hello $1, nice to meet you!"
	echo "---------------------------"
}
```

在终端或脚本中直接输入函数名即可,不需要小括号
传参也只需将参数加到函数名后面,以空格做间隔,像正常使用命令那样

```
foo seamile
```

参数

```
bar() {
	echo "执行者是 $0"
	echo "参数量是 $#"
	echo "全部的参数 $@"
	echo "全部的参数 $*"
	if [ -d $1 ]; then  # 检查传入的第一个参数是否是文件夹
		for f in `ls $1`
		do
        	echo $f
		done
	elif [ -f $1 ]; then
		echo 'This is a file: $1' # 单引号内的变量不会被识别
		echo "This is a file: $1" # 如果不是文件夹, 直接显示文件名
	else
		echo 'not valid' # 前面都不匹配显示默认语句
	fi
}
```

#	6、获取用户输入

```
read -p "请输入一个数字:" num
echo "您输入的是:$num"
```



































































