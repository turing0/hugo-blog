---
title: Linux下C语言学习
abbrlink: linux-c
date: 2020-04-17 08:13:58
tags: [C, Linux]
categories: 
  - [Code]
  - [Linux]
---

系统Ubuntu  18.04

<!--more-->

# C环境准备

更新库：`sudo apt update；`

更新软件：`sudo apt upgrade;`

下载vim：`sudo apt install vim；`

下载gcc：`sudo apt install gcc`

下载gdb：`sudo apt install gdb`

为了方便写代码，在编辑器中加入行号：cd etc/wim；sudo vi vimrc什么都不要改，只在最后一行加上set nu；保存退出。

# 第一个Linux下的C程序

打开terminal

`vi hello.c`

按i进入输入模式

```c
#include <stdio.h>

int main(int argc, char *argv[]){
    printf("hello world!\n");


    return 0;
}
```

按esc推出输入模式，保存退出

编译hello.c

`gcc -o hello hello.c -Wall`

执行

`./hello`

## 完整的演示

```c
$ vi main.c
$ gcc main.c  #生成可执行程序
$ ./a.out  #运行可执行程序
hello world!
$   #继续等待输入其它命令
```

## 分步骤编译

### 编译（Compile）

将源文件编译成目标文件需要使用`-c`选项，例如：

`gcc -c hello.c`

就将 hello.c 编译为 hello.o。

一个源文件会生成一个目标文件，多个源文件会生成多个目标文件，源文件数目和目标文件数目是一样的。通常情况下，默认的目标文件名字和源文件名字是一样的。

 如果希望自定义目标文件的名字，那么可以使用`-o`选项，例如：

`gcc -c hello.c -o a.o`

这样生成的目标文件的名字就是 a.o。

### 链接（Link）

在`gcc`命令后面紧跟目标文件的名字，就可以将目标文件链接成为可执行文件，例如：

`gcc hello.o`

就将 hello.o 链接为 a.out。

在`gcc`命令后面紧跟源文件名字或者目标文件名字都是可以的，`gcc`命令能够自动识别到底是源文件还是目标文件：如果是源文件，那么要经过编译和链接两个步骤才能生成可执行文件；如果是目标文件，只需要链接就可以了。

 使用`-o`选项仍然能够自定义可执行文件的名字，例如：

`gcc hello.o -o hello.out`

这样生成的可执行文件的名字就是 hello.out。