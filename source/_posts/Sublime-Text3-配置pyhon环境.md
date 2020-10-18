---
title: Sublime Text3 配置pyhon环境
date: 2020-03-13 09:23:28
tags: 软件安装
categories: 软件安装
---
### Sublime Text3 配置python环境详解。
<!--more-->

#### Sublime Text3配置python环境

安装参考以前文章，下面说配置

打开安装好的 sublime text 3，选择编译环境
![0e3b5e9cfb36e436416f187edb061fd0.png](./Sublime-Text3-配置pyhon环境/SublimePython01.png)


然后输入
> print("你好")

然后保存为.py后缀文件

回到主界面，Ctrl+B运行

![89d3fe035435cc1dc56fff80ffd225fc.png](./Sublime-Text3-配置pyhon环境/SublimePython02.png)


中文成功输出，证明配置好了，但还需要按一个插件来支持 input

安装SublimeREPL插件，使Sublime支持input

安装好，试着调用。

```
num = input("今天几月几日:")
print(num)
```

跟 Ctrl+B 直接编译不同，利用插件来编译需要先手动 Ctrl+S 保存

**常规调用：**

![69d5a1b9e9dfe5c1aff1d2e1e1775f36.png](./Sublime-Text3-配置pyhon环境/SublimePython03.png)

然后弹出一个新的框，进行输入输出。

![fbe8fc6a38764b3605c069357dafdf37.png](./Sublime-Text3-配置pyhon环境/SublimePython04.png)

**设置快捷键调用：**

![ded30527af9e541ca4cf0e79bf907cf2.png](./Sublime-Text3-配置pyhon环境/SublimePython05.png)

左边是系统默认设置，我们在右边窗口输入以下设置（另一个 Alt + End 是终止编译的快捷键），Ctrl+S 保存

![bc715187792b855d583c10db6cc44403.png](./Sublime-Text3-配置pyhon环境/SublimePython06.png)

```markdown
[ 
    { 
        "keys": ["f4"], 
        "caption": "SublimeREPL: Python - RUN current file", 
        "command": "run_existing_windoww_command", 
        "args": { 
            "id": "repl_python_run", 
            "file": "config/Python/Main.sublime-menu"
        } 
    },
        { 
            "keys": ["alt+end"], 
            "command": "exec", 
            "args": {"kill": true} 
        } 
]
```

切换不方便，可以打开两个视图：

![c33682bb046be44ffbe99139d83ea249.png](./Sublime-Text3-配置pyhon环境/SublimePython07.png)

本文参考：
链接：[https://www.zhihu.com/question/22904994/answer/800236870](https://www.zhihu.com/question/22904994/answer/800236870)
