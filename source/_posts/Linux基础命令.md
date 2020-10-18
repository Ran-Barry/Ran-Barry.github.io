---
title: Linux基础命令
date: 2020-02-12 20:30:22
tags: Linux学习
categories: Linux学习
---

## 基础命令
【语句格式】
> 命令名称  [命令参数] [命令对象]

<!--more-->
### 1.获取登录信息 - **w/who/last/lastb**

```
admintor@admintor-PC:~/Desktop$ w
 12:32:22 up  2:57,  1 user,  load average: 0.86, 1.18, 1.13
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
admintor tty1     :0               09:35    2:57m  4:45  11.21s /usr/bin/startdde
admintor@admintor-PC:~/Desktop$ clear

admintor@admintor-PC:~/Desktop$ w
 12:32:28 up  2:57,  1 user,  load average: 0.79, 1.16, 1.13
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
admintor tty1     :0               09:35    2:57m  4:45  11.21s /usr/bin/startdde
admintor@admintor-PC:~/Desktop$ who
admintor tty1         2020-02-08 09:35 (:0)
admintor@admintor-PC:~/Desktop$ whoami
admintor
admintor@admintor-PC:~/Desktop$ last
admintor tty1         :0               Sat Feb  8 09:35   still logged in
reboot   system boot  4.15.0-30deepin- Sat Feb  8 17:34   still running
admintor tty1         :0               Fri Feb  7 11:43 - 18:32  (06:49)
reboot   system boot  4.15.0-30deepin- Fri Feb  7 19:42 - 18:32  (-1:-9)
admintor tty1         :0               Wed Feb  5 10:21 - 14:43  (04:21)
reboot   system boot  4.15.0-30deepin- Wed Feb  5 18:19 - 14:43  (-3:-36)
admintor tty1         :0               Tue Feb  4 09:32 - 18:16  (08:44)
reboot   system boot  4.15.0-30deepin- Tue Feb  4 17:31 - 18:17  (00:45)
admintor tty1         :0               
```

### 2.查看自己使用的Shell - **ps**

```
admintor@admintor-PC:~/Desktop$ ps
  PID TTY          TIME CMD
19593 pts/1    00:00:00 bash
20057 pts/1    00:00:00 ps
```

### 3.查看命令的说明和位置 - **whatis/which/whereis**

#### whatis
【功能】在whatis库中搜寻特定的命令 

【语法】whatis COMMAND

```
admintor@admintor-PC:~/Desktop$ whatis ps
ps (1)               - report a snapshot of the current processes.
admintor@admintor-PC:~/Desktop$ whatis python
python3.7 (1)        - an interpreted, interactive, object-oriented programming language
python (1)           - an interpreted, interactive, object-oriented programming language
```

#### whereis
【功能】 查找文件、手册页、命令等的相关位置

【语法】 whereis options argument

【常用选项】 

```
-b:只查找二进制文件位置
-m:只查找手册页部分
```

【实例】
```
admintor@admintor-PC:~/Desktop$ whereis ps
ps: /usr/bin/ps /usr/share/man/man1/ps.1.gz
admintor@admintor-PC:~/Desktop$ whereis python
python: /usr/bin/python /usr/bin/python2.7-config /usr/bin/python3.5-dbg /usr/bin/python2.7 /usr/bin/python3.5dm-config /usr/bin/python3.5 /usr/bin/python3.5m /usr/bin/python3.5dm /usr/bin/python3.5-dbg-config /usr/lib/python2.7 /usr/lib/python3.5 /etc/python /etc/python2.7 /etc/python3.5 /usr/local/bin/python3.7 /usr/local/bin/python3.7m /usr/local/bin/python3.7m-config /usr/local/lib/python3.7 /usr/local/lib/python2.7 /usr/local/lib/python3.5 /usr/include/python2.7 /usr/include/python3.5m /usr/include/python3.5dm /usr/share/python /usr/share/man/man1/python.1.gz
```

#### which
【功能】 查看**可执行命令**的路径

【语法】which COMMAND
```
admintor@admintor-PC:~/Desktop$ which ps
/usr/bin/ps
admintor@admintor-PC:~/Desktop$ which python
/usr/bin/python
```

### 4.清除屏幕上显示的内容 - **clear**

### 5.查看帮助文档 - **man/info/help/apropos**
```
admintor@admintor-PC:~/Desktop$ ps --help

Usage:
 ps [options]

 Try 'ps --help <simple|list|output|threads|misc|all>'
  or 'ps --help <s|l|o|t|m|a>'
 for additional help text.

For more details see ps(1).
admintor@admintor-PC:~/Desktop$ man ps
PS(1)                                                    User Commands                                                    PS(1)

NAME
       ps - report a snapshot of the current processes.

SYNOPSIS
       ps [options]

DESCRIPTION
...
```

### 6.查看系统和主机名 - **uname/hostname**

```
admintor@admintor-PC:~/Desktop$ uname
Linux
admintor@admintor-PC:~/Desktop$ hostname
admintor-PC
```

### 7.时间和日期 - **date/cal**

```
admintor@admintor-PC:~/Desktop$ date
2020年 02月 08日 星期六 15:56:50 CST
admintor@admintor-PC:~/Desktop$ cal
      二月 2020         
日 一 二 三 四 五 六  
                   1  
 2  3  4  5  6  7  8  
 9 10 11 12 13 14 15  
16 17 18 19 20 21 22  
23 24 25 26 27 28 29  
                      
admintor@admintor-PC:~/Desktop$ cal 5 2017
      五月 2017         
日 一 二 三 四 五 六  
    1  2  3  4  5  6  
 7  8  9 10 11 12 13  
14 15 16 17 18 19 20  
21 22 23 24 25 26 27  
28 29 30 31     
```

### 8.重启和关机 - **reboot/shutdown**

### 9.退出登录 - **exit/logout**

### 10.查看历史命令 - **history**

```
admintor@admintor-PC:~/Desktop$ history
...
441  whatis python
442  whereis ps
443  whereis python
444  which ps
445  which python
446  ps --help
447  man ps
448  uname
449  hostname
450  date
451  cal
452  cal 5 2017
453  history
admintor@admintor-PC:~/Desktop$ !452
```
> 查看到历史命令后，可以用！历史命令编号来重新执行该命令；通过history -c 可以清除历史命令。
