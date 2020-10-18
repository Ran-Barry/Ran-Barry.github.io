---
title: binwalk安装使用
date: 2020-01-18 11:14:45
tags: 软件安装
categories: 软件安装
---

网上也有这个安装教程，我是看完之后根据自己的安装总结一下。以备以后使用。
这个软件就是对图片进行分析，看是否包含有文件压缩包。
<!--more-->
#### **1.下载**
github项目：[安装链接](https://github.com/devttys0/binwalk)
需要已经下载python，python2或python3都行。
下载完zip文件，下载完解压。
#### **2.安装**
打开文件夹，在目录里按**Shift+右键**，打开命令窗口。输入
**python setup.py install**
安装完成
#### **3.配置**
到自己到python安装目录找到Script目录，打开，因为刚刚已经安装完成，所以里面应该有叫binwalk的没有后缀的文件。根据我的经验，可以不用理他。因为按照正常方式，要是需要用binwalk，需要输入命令比较多一点，想简单一点，可以按照下面的方法。（也是根据网上的一些教程来的，感觉这个挺方便的）。

 新建一个文件夹（可以在python那个安装目录），并把文件夹的路径加入到系统变量path里（这样在cmd里就可以直接运行了。）    
 在文件夹里新建一个binwalk.bat文件，内容为以下代码。（代码来自网上教程，自己操作过，莫得问题）
 
```
@echo off
echo * suggest: you'd better to input the parameters enclosed in double quotes.echo * made by pcat
python "%~dp0\p_binwalk.py" %1 %2 %3 %4 %5 %6 %7 %8 %9
```

再新建一个p_binwalk.py文件
```
import sys
import binwalk

if __name__ == "__main__":
    lst=sys.argv
    if len(lst)<2:
        print("No files.")
        exit()
    try:
        if lst[1][0]=='-':
            binwalk.scan(*lst[2:],signature=lst[1])
        elif lst[1][0]!='-':
            binwalk.scan(*lst[1:],signature=True)
    except:
        pass
```
 只要这个文件夹的路径在系统变量path里和这2个文件存在着，那么你就可以在cmd里像linux那样使用binwalk了。
 #### **4.常用命令**
 -e 分解出压缩包
```
 binwalk -e 555.gif
```
-D或者--dd分解某种类型的文件（在windows里要用双括号括起来）
```
binwalk -D=jpeg 555.gif
```
-M 递归分解扫描出来的文件（得跟-e或者-D配合使用）

```
binwalk -eM 555.gif
```
