# Linux

[//]: # (__author__ = "Clark Aaron")

Linux操作系统是一种类UNIX操作系统.它诞生于1991年10月5日,是由Linus Torvalds开发的Linux Kernel与GNU计划中的自由软件结合的的类Unix操作系统.其具有多用户、多任务、多线程、支持所有的网络协力的特点;所以广泛运用服务器、程序开发、嵌入式等应用场景.Linux(GNU/Linux)是一套免费使用和自由传播的类UNIX操作系统,继承了Unix以网络为核心的设计思想;其内核由Linus Benedict Torvalds于1991年发布.由于Linux Kernel遵循POSIX标准,所以能运行主要的Unix工具软件、应用程序和网络协议;Linux有终端与界面两种管理方式，其中界面中的X-Windows是一个类Windows的操作界面,Linux支持多种硬件平台,广泛用于服务器与嵌入式;Linux有众多的发行版本,如Red Hat发行的`Red Hat Linux`,`Red Hat Enterprise`,`Redora`,`CentOS`;SUSE发行的`SUSE Linux Enterprise`,`openSUSE`;Debian发行的`Debian`,`Ubuntu`,`Mint`,`Gentoo`,`Arch Linux`,`Mandriva`,`Slackware`,`TurboLinux`。

## 资源连接

> [官方网站](https://www.linux.org/) ☛ <https://www.linux.org/>

* [Linux入门教程](https://www.linux.org/forums/linux-beginner-tutorials.123/) ☛ <https://www.linux.org/forums/linux-beginner-tutorials.123/>

  1. [Linux简介](https://www.linux.org/threads/what-is-linux.4106/) ☛ <https://www.linux.org/threads/what-is-linux.4106/>
  2. [Linux的安装方式](https://www.linux.org/threads/what-type-of-installation-should-i-do-dual-boot-live-cd-fresh-install-virtual-installation.4116/) ☛ <https://www.linux.org/threads/what-type-of-installation-should-i-do-dual-boot-live-cd-fresh-install-virtual-installation.4116/>
  3. [Debian安装](https://www.linux.org/threads/installing-debian.4118/) ☛ <https://www.linux.org/threads/installing-debian.4118/>

## 基础知识

### 程序

程序是编译好的可执行的二进制文件。

### 进程

进程是运行的程序，进程拥有一个4GB虚拟内存。从0~3GB的空间为用户空间，3~4GB的空间为内核空间；每一个进程包含一个PCB（Process Control Block），Linux系统中进程的PCB是结构体task_struct（进程id、进程状态、进程切换时寄存器的值、虚拟地址的信息、控制终端的信息、当前工作目录、umask掩码、文件描述符、信号信息、用户id与组织id、会话与进程组、进程的资源上限）

* `ulimit -a`显示所有进程的资源上限。

#### 进程间的通信

* 共享内存

* 管道

#### 守护进程

Linux中的守护进程类似于Windows中的服务。

### 环境变量

环境变量是操作系统中用来指定操作系统运行时的环境参数，环境变量通常以键值对存储。类似于命令参数，存储在用户空间。

* `PATH`：可执行文件的搜索路径。
* `SHELL`：当前shell程序。
* `TERM`：当前终端类型，决定一些程序的显示方式。
* `LANG`：语言和locale。
* `HOME`：当前用户的家目录。

在`stblib.h`中定义了管理环境变量的函数。

* `getenv()`
* `setenv()`
* `unsetenv()`

在`unistd.h`中定义了创建子进程的函数。

* `fork()`:

## 发展简述

### Debian

Debian是由Ian Murdock与1993年发布的,基于Debian的桌面环境有Ubuntu(根据桌面可分为基于GNOME的Ubuntu、基于KDE的KUbuntu、基于Xface的XUbuntu)，二Mint是基于Debian与Ubuntu发行的.

### Red Hat

Red Hat由Marc Ewing发布的Linux发行版本,目前Red Hat有RHEL(Red Hat Enterprise Linux,提供收费技术支持与更新)、Fedora是Red Hat的技术实验平台、CentOS.

### Gentoo

Gentoo是Linux最年轻的发行版本.

### Mandriva

### CtenOS

* CentOS是一个开源的Linux操作系统,官方提供两种发行版本,分别为CentOS Linux与CentOS Stream;

* [官方网站](https://www.centos.org/) > https://www.centos.org
  1. [官方介绍](https://www.centos.org/about/) > https://www.centos.org/about/
  2. [官方文档](https://) > https://
  3. [官方社区]() > 

### Ubuntu

在Linux系统启动之后,Linux的内核程序启动称为一个单一的内核进程,该进程有权调用计算机的所有资源.当应用程序启动时,内核会分配一定的计算机资源.应用程序与硬件之间的互动,也必须经过内核进行.我们将内核程序的活动称为**内核模式**,而将应用程序的活动称为**用户模式**.应用程序可以通过特定的接口来调用内核功能.用户单次的内核调用称为一次**系统调用**;可以通过`syscalls`命令查看Linux下所有的系统调用

* GNU项目

  * Linux内核
  * GPL协议
  * GNOME桌面
  * GDB调试器
  * GCC编辑器
  * GNU图形工具

* Linux系统概述及安装

  * 多用户多任务的分时操作系统
  * 类UNIX的操作系统
  * Fedora
  * Ubuntu
  * RedHat
  * openSUSE
    * 德国著名Linux发行版，Novel公司维护 YasT软件包管理
  * Debian

## 系统架构

### 文件系统

文件是Linux中基础，具有所有者、所属组、权限、时间（mtime、ctime、atime）等属性；FS（File System，文件系统）是一个由文件组成的系统。Linux中
的FS是以树状结构的形式存在，起点为根目录`/`，每一个目录节点提供归属关系：CD（Child Directory，子目录）与PD（Parent Directory，父目录）；
且由根目录开始的所有途径的目录名和文件名组成该文件的绝对目录，从工作目录开始的所有途径的目录名与文件名组成该文件的相对目录。工作目录是Linux中的
一个变量，表示shell程序当前的工作目录，可以由`pwd`来获取或使用`cd`修改其值。在Linux中，目录是一种特殊的文件，其中`.`表示当前目录，`..`表示父
目录。当FS中新建一个文件时，会在工作目录建立一个指向该文件的HL（Hard Link，硬链接）；文件有HL才会被纳入FS，否则会被删除；而文件的硬链接数目
LC（Link Count，链接数）可以有多个，可以使用`ln`创建和`unlink`删除HL；为保持FS的树状结构，Linux系统推荐使用SL（Soft Link，软链接），新建
SL不会影响LC，其实质是`symbolic link`文件，包含有链接指向文件的绝对路径。编辑文件时，Linux只会将内容的编辑导向SL指向的文件，类似于Windows
的快捷方式，使用`ln -s`创建SL。可以使用`file`来查询文件的类型。

### 内核系统

Linux启动的过程有：内核的引导、运行init、系统初始化、建立终端、用户登录系统。
