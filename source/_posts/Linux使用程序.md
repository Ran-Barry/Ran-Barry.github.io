---
title: Linux使用程序
date: 2020-02-12 20:32:30
tags: Linux学习
categories: Linux学习
---

## 文件和文件夹操作

### 1.创建/删除空目录 - **mkdir/rmdir**
<!--more-->
```
[root ~]# mkdir abc
[root ~]# mkdir -p xyz/abc
[root ~]# rmdir abc
```

### 2.创建/删除文件 - **touch/rm

```
[root ~]# touch readme.txt
[root ~]# touch error.txt
[root ~]# rm error.txt
rm: remove regular empty file ‘error.txt’? y
[root ~]# rm -rf xyz
```

* touch命令用于创建空白文件或修改文件时间。在Linux系统中一个文件有三种时间：
  * 更改内容的时间 - mtime
  * 更改权限的时间呢 - ctime
  * 最后访问时间 - atime
* rm的几个重要参数
  * -i: 交互式删除，每个删除项都会进行询问
  * -r：删除目录并递归的删除目录中的文件和目录
  * -f：强制删除，忽略不存在的文件，没有任何提示

### 3.切换和查看当前工作目录 - **cd/pwd**
说明：
> cd命令后面可以跟相对路径（以当前路径作为参照）或绝对路径（以/开关）来切换到指定的目录，也可以用cd .. 来返回上一级目录。请大家想一想，如果要返回到上上一级目录应该给cd命令加上什么样的参数呢？

### 4.查看目录内容 - **ls**

* -l：以长格式查看文件和目录
* -a：显示以点开头的文件和目录（隐藏文件）
* -R：遇到目录要进行递归展开（继续列出目录下面的文件和目录）
* -d：只列出目录，不列出其他内容
* -s/-t：按大小/时间排序

> ls -l 可以简写为ll

### 5.查看文件内容 - **cat/tac/head/tail/more/less/rev/od**

* cat: 由第一行开始显示内容，并将所有内容输出
* tac: 从最后一行倒序显示内容，并将所有内容输出
* rev：从每一行的最后一个字符显示到第一个字符
* head：只显示头几行
* tail：只显示后几行
* more：根据窗口大小，一页一页的显示文件内容
* less：和more类似，但其优点可以往前翻页，而且进行可以搜索字符
* od：以八进制、十进制、十六进制和ASCII码的格式来显示文件或者流
  * od [-A 地址进制] [-t 显示格式] 文件名
  * -A 指定地址进制包括：
    * o:八进制（系统默认值）
    * d：十进制
    * x：十六进制
    * n：不打印位移值
  * -t：指定数据的显示格式的主要参数有：
    * c：ASCII字符或反斜杠序列（如\n）
    * d：有符号十进制数
    * f：浮点数
    * o：八进制（系统默认值）
    * u：无符号十进制数
    * x：十六进制数

### 6.拷贝/移动文件 - **cp/mv**

```
[root ~]# mkdir backup
[root ~]# cp sohu.html backup/
[root ~]# cd backup
[root backup]# ls
sohu.html
[root backup]# mv sohu.html sohu_index.html
[root backup]# ls
sohu_index.html
```

### 7.文件重命名 - **rename**

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# rename .htm .html *.htm
```
### 8.查找文件和查找内容 - **find/grep**

【find】：find 路径 参数 文件名
参数：
* -name：根据文件名查找
* -perm：根据文件权限查找
* -prune：该选项可以排除某些查找目录
* -user：根据文件属主查找
* -group：根据文件属组查找
* -mtime -n | +n 根据文件更改时间查找
* -type：根据文件类型查找、
  * -f: 文件
  * -d：目录
  * -c：字符设备文件
  * -b：块设备文件
  * -l：链接文件
  * -p：管道文件
* -size -n +n 按文件大小查找
【grep】：grep [选项] [文本] 文件
> 说明：grep在搜索字符串时可以使用正则表达式，如果需要使用正则表达式可以用grep -E 或直接使用egrep

### 9.创建链接和查看链接 -**ln/readlink**

软链接：
* 存放另一个文件的路径的形式
* 可以跨文件系统，硬链接不可以
* 可以对一个不存在的文件名进行链接，硬链接必须有源文件
* 可以对目录进行链接

硬链接：

* 以文本副本的形式存在，不占用实际空间
* 不允许给目录创建硬链接
* 只有在同一个文件系统中才能创建
* 删除其中一个硬链接文件并不影响其他有相同inode号的文件

> 【ln】：[参数] [源文件目录] [目标文件或目录]

主要参数：
* -i:交互模式，文件存在则提示用户是否覆盖
* -s 软链接（符号链接）
* -d 允许超级用户制作目录的硬链接
* -b 删除，覆盖以前建立的链接

### 10.压缩/解压缩和归档/解归档 - **gzip/gunzip/xz**

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# wget http://download.redis.io/releases/redis-4.0.10.tar.gz
--2018-06-20 19:29:59--  http://download.redis.io/releases/redis-4.0.10.tar.gz
Resolving download.redis.io (download.redis.io)... 109.74.203.151
Connecting to download.redis.io (download.redis.io)|109.74.203.151|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1738465 (1.7M) [application/x-gzip]
Saving to: ‘redis-4.0.10.tar.gz’
100%[==================================================>] 1,738,465   70.1KB/s   in 74s
2018-06-20 19:31:14 (22.9 KB/s) - ‘redis-4.0.10.tar.gz’ saved [1738465/1738465]
[root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*
redis-4.0.10.tar.gz
[root@iZwz97tbgo9lkabnat2lo8Z ~]# gunzip redis-4.0.10.tar.gz
[root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*
redis-4.0.10.tar
```

### 11.归档和解归档 - **tar**

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# tar -xvf redis-4.0.10.tar
redis-4.0.10/
redis-4.0.10/.gitignore
redis-4.0.10/00-RELEASENOTES
redis-4.0.10/BUGS
redis-4.0.10/CONTRIBUTING
redis-4.0.10/COPYING
redis-4.0.10/INSTALL
redis-4.0.10/MANIFESTO
redis-4.0.10/Makefile
redis-4.0.10/README.md
redis-4.0.10/deps/
redis-4.0.10/deps/Makefile
redis-4.0.10/deps/README.md
...
```

> 说明：归档（也称为创建归档）和解归档都使用tar命令，通常创建归档需要-cvf三个参数，其中c表示创建（create），v表示显示创建归档详情（verbose），f表示指定归档的文件（file）；解归档需要加上-xvf参数，其中x表示抽取（extract），其他两个参数跟创建归档相同。

### 12.将标准输入转成命令行参数 - **xargs**

下面的命令会将查找当前路径下的html文件，然后通过xargs将这些文件作为参数传给rm命令，实现查找并删除文件的操作

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# find . -type f -name "*.html" | xargs rm -f
```

下面的命令讲a.txt文件中的多行内容变成一行输出到b.txt文件中，其中<表示从a.txt中读取输入，>表示讲命令的执行结果输出到b.txt中

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# xargs < a.txt > b.txt
```

> 说明：这个命令就像上面演示的那样常在管道（实现进程间通信的一种方式）和重定向（重新指定输入输出的位置）操作中用到，后面的内容中会讲到管道操作和输入输出重定向操作。

### 13.显示文件或目录 - **basename/dirname**

### 14.其他相关工具

* sort - 对内容排序
* uniq - 去掉相邻重复内容
* tr - 替换指定内容为新内容
* cut/paste - 剪切/粘贴内容
* split - 拆分文件
* file - 判断文件类型
* wc - 统计文件行数、单词数、字节数
* iconv - 编码转换

```
[root ~]# cat foo.txt
grape
apple
pitaya
[root ~]# cat bar.txt
100
200
300
400
[root ~]# paste foo.txt bar.txt
grape   100
apple   200
pitaya  300
        400
[root ~]# paste foo.txt bar.txt > hello.txt
[root ~]# cut -b 4-8 hello.txt
pe      10
le      20
aya     3
0
[root ~]# cat hello.txt | tr '\t' ','
grape,100
apple,200
pitaya,300
,400
[root ~]# split -l 100 sohu.html hello
[root ~]# wget https://www.baidu.com/img/bd_logo1.png
[root ~]# file bd_logo1.png
bd_logo1.png: PNG image data, 540 x 258, 8-bit colormap, non-interlaced
[root ~]# wc sohu.html
  2979   6355 212527 sohu.html
[root ~]# wc -l sohu.html
2979 sohu.html
[root ~]# wget http://www.qq.com -O qq.html
[root ~]# iconv -f gb2312 -t utf-8 qq.html
```