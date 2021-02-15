# BIOS

BIOS（Basic Input and Output System，基本输入与输出系统）是一个用于计算机开启时进行硬件平台初始化和操作系统引导的程序。由于BIOS是固化在ROM（以前是固化在EPROM，现在多用flash ROM）中的程序，所以又被称为固件。BIOS主要有四个基础功能：BIOS中断程序、BIOS设置程序、BIOS上电自检、BIOS系统选择

* BIOS中断程序：是衔接操作系统与计算机硬件之间的接口，操作系统可以通过该接口调用硬件资源。
* BIOS设置程序：是BIOS支持用户设定CMOS参数的程序，通过这些参数的设置来使计算机性能得到优化。
* BIOS上电自检：又称POST（Power On Self Test），对计算机硬件资源进行检查和初始化。
* BIOS系统选择：在POST通过之后，按照CMOS中设定的启动顺序寻找系统的引导记录并将系统控制权交给系统引导记录。

## 计算机启动原理

* 电源供电：在计算机电源供电稳定之后，电源产生一个复位脉冲使CPU进行复位（CS寄存器复位为ffffH，IP寄存器复位为0000H），CPU会到CS:IP读取指令执行，第一条指令一般为跳转指令（跳转到ROM程序开始执行）。
* POST：CPU读取到ROM程序后，开始对硬件资源进行检查并按照CMOS的参数进行初始化，在检测到其他硬件有BIOS（例如显卡BIOS，执行后屏幕会显示硬件信息）存在时，跳转到其他BIOS执行后返回，在这一步会有热启动或冷启动的判断。
* 系统引导：在完成POST之后会按照CMOS中设定的顺序查找MBR，MBR位于磁盘的第0柱面第0磁头第1扇区，共有512B。其中前446B（0000H~01bdH）为引导程序，随后的64B（01beH~01fdH）为DPT。

## BIOS的类型

* Award BIOS: Ctrl+Alt+Esc, Delete
* AMI BIOS:Delete,Esc
* Phoenix:F10,F1,F2,Ctrl+Alt+S,Ctrl+Alt+INS

## BIOS的设置

## BIOS的更新

## BIOS的发展

* Dual BIOS
* Safe BIOS
* KeyBIOS
* TwinBIOS
* CSS
* EFI BIOS

## BIOS的管理

