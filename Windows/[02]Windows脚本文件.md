# Windows脚本文件

[//]: # (__author__ = "Clark Aaron")

脚本文件即批量处理终端命令的程序，又可以称为批处理文件；Windows支持`*.bat`或`*.cmd`批处理文件。

## 基础语法

* 【功能】文档注释：

  ```cmd
  @rem <comment>
  ```

* 【功能】回显功能：

  ```cmd
  @rem 该命令不执行回显功能。
  @<command>
  @rem 关闭回显功能。
  echo off
  @rem 打开回显功能。
  echo on
  ```

* 【功能】变量参数：

  ```cmd
  @rem 使用set创建变量。
  set <variable> = <value>
  @rem 创建让用户输入变量带有提示符。提示符输出到标准输出中。
  set /p <varlable> = <prompt>
  @rem 创建数值表达式的变量。
  set /a <variable> = <experssion>
  @rem 命令参数的显示，%0~9与%*，%*所有参数。
  echo %1
  ```

* 【语法】分支语句：

  ```cmd
  @rem if分支的使用格式。
  if [not] <string1>==<string2> <command> [else <expression>]
  @
  ```

* 【语法】循环语句：

  ```cmd
  @rem for的使用格式，variable只能是字符。
  for {%%|%}<variable> in (<set>) do <command> [<commandlineoptions>]
  @rem 遍历E与F盘目录下所有文件。
  for /r %%f in (e:,f:) do (@each %%f)
  @rem 使用迭代器测试192.168.43.0下所有IP地址。
  for /l %%i in (1,1,255) do(@ping 192.168.43.%%i)
  ```

  > Note：在脚本文件中使用%%，在cmd中使用%。
