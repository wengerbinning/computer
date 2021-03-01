# Linux的系统管理

[//]: # (__author__ = "Clark Aaron")

Linux的系统管理是Linux经常使用的管理命令,包括账户管理、文件管理、设备管理、进程管理、服务管理以及其他的系统管理。

## 账户管理

在Linux中账户拥有UID、GROUP及备注信息等属性;其中UID判断用户的依据,管理员的UID为0,系统用户的UID为1~999,普通用户的UID从1000开始;用户组是用于批量管理用户,其具有用户组ID的属性,系统用户组GID为0。

在批量管理用户时，可以通过修改配置文件来管理。

* 【配置文件】账户信息:`/etc/passwd`;
* 【配置文件】账户密码:`/etc/shadow`;
* 【配置文件】用户组信息:`/etc/group`;
* 【配置文件】sudo授权:`/etc/sudoers`;

### 用户的管理

* 【功能】创建普通用户:

  ```shell
  # 创建默认参数的用户。
  useradd <username>
   # 创建指定家目录所属路径的用户。
  useradd -b <path> <username>
  # 创建指定注释信息的用户。
  useradd -c <content> <username>
  # 创建指定家目录的用户。
  useradd -d <homepath> <username>

  useradd -p <password> <username>    # 创建指定密码的用户
  useradd -r <username>               # 创建系统用户
  useradd -u <UID>  <username>        # 创建指定UID的用户
  useradd -g <groupname> <username>   # 创建指定用户组的用户
  ```

* 【功能】查看用户信息:

  ```shell
  cat /etc/passwd                     # 查看所有用户信息
  cat /etc/passwd | grep <username>   # 查看指定用户信息
  id <username>                       # 查看指定用户信息
  whoami                              # 查看当前登录用户信息
  compgen -u                          # 查看所有用户
  hostname                            # 显示主机名
  uname                               # 显示系统信息
  top                                 # 动态显示进程信息
  ps -aux                             # 显示当前时刻的进程信息
  su <username>                       # 切换用户
  sudo                                # 以管理员权限执行命令,配置文件在/etc/sudoers
  ```

* 【功能】修改用户信息：

  ```shell
  # 修改指定用户的密码。
  passwd <user>
  # 修改用户的UID。
  usermod -u <UID>  <user>
  ```

* 【功能】删除普通用户:

  ```shell
  userdel <username>                  # 默认选项删除用户
  userdel -r <username>               # 删除用户以及家目录与 mail spool
  ```

* 【功能】用户间的通信:

  ```shell
  echo "Hello" | write <username>     # 用另一个用户通信
  ```

### 用户组管理

* 【功能】创建用户组:

  ```shell
  # 创建默认参数的用户组。
  groupadd <group>
  # 创建指定GID的用户组。
  groupadd -g <GID> <group>

  groupadd -r <group>
  # 创建系统用户组
  groupadd -s <groupname>
  ```

* 【功能】修改用户组：

  ```shell
  groupmod -g <GID> <groupname>              # 修改用户组的GID
  ```

* 【功能】查看组信息：

  ```shell
  cat /etc/group                    # 查看所有用户组信息
  cat /etc/group | grep <groupname> # 查看指定用户组信息
  groups                            # 查看当前用户所在组的信息
  compgen -g                        # 查看用户组信息
  ```

* 【功能】切换用户组：

  ```shell
  newgrp <userGroupName>            # 切换用户组
  ```

* 【功能】删除用户组:

  ```shell
  groupdel <groupname>              # 删除用户组
  ```

## 文件管理

* 【功能】新建文件:

  ```shell
  # 新建一个空的文件。
  touch <file>
  # 通过重定向的方式创建文件。
  echo <content>  > <file>
  # 创建一个硬链接文件。
  ln <sources file> <object>
  # 创建一个目录。
  mkdir <directory>
  ```

* 【功能】查看文件:

  ```shell
   # 查看文件内容。
  cat <file>
  # 从最后一行开始显示。
  tac <file>
  # 带行号显示文件。
  nl <file>
  # 格式化显示文本内容。
  printf <format string> <content>
  # 分页查看文件内容。
  more <file>
  # 分页查看文件内容，可以前翻。
  less <file>
  # 显示文件的头部，默认显示头部10行内容。
  head <file>
  # 显示文件的尾部。
  tail <file>
  # 以二进制的方式显示
  od  <file>
  # 统计文件字节数、行数、字数。
  wc -clw <file>
  export                  # 显示环境变量
  ls                      # 显示目录下的所有内容;
  stat                    # 详细显示文件或目录信息;
  pwd                     # 显示工作目录
  diff                    # 比较两个文件
  # 根据路径显示文件名。
  basename <path>
  # 根据文件名显示路径。
  dirname <file>
  ```

* 【功能】修改文件:

  ```shell
  chgrp <groupname> <filename>       # 修改文件所有者所在组
  chown <username> <filename>        # 修改文件所有者
  chmod <number> <filename>          # 修改文件属性
  # 使用字符串替换的方式批量修改文件名。
  rename <oldstring> <newstring> <file>
  # 转换文件编码格式。
  iconv <source file> -f <source type> -t <goal type> -o <goal type>
  # 将文件的制表符转换为空白字符。
  expand -t 4 <file>
  # 将文件的空白字符转换为制表符。
  unexpand -t 4 <file>
  # 将文本转化为适合打印的格式。
  pr -h <title> -l <line> <file>
  # 将文件内容以字符为单位反序输出。
  rev <file>
  ```

* 【功能】复制文件:

  ```shell
  cp <sourcefilename> <objectfilename>     # 复制文件
  cp -r <sourcefilename> <objectfilename>  # 复制目录
  ```

* 【功能】移动文件:

  ```shell
  mv <sourcefilename> <objectfilename>    # 移动或重命名
  cd <WorkingDirectory>                   # 切换工作目录
  ```

* 【功能】删除文件:

  ```shell
  rm <filename>                           # 移除文件或目录;
  rmdir <directoryname>                   # 删除空目录
  rm -r <directoryname>                   # 删除目录及其子目录;
  # 检查和删除重复内容
  uniq -cdu <file>
  # 删除文件，不能删除目录。
  unlink <file>
  ```

* 【功能】内容查询

  ```shell
  find <filename>                    # 查找文件,不常使用,对硬盘有损伤
  find / -name "*.c"                 # 发现根目录下的所有c文件
  which <filename>                   # 查找文件,查找$PATH中的内容
  whereis <filename>                 # 查找文件,在数据库中寻找,使用updatedb更新数据库
  locate <filename>                  # 查找文件,同上
  grep <filename>
  ```

* 【功能】其他操作：

  ```shell
  # 创建或更新slocate数据库文件。
  updatedb
  ```

在远距离的文件传输中,经过压缩后再传输会节省很多资源,常用的解压软件有`compress`与`tar`;在Linux中`tar`是常用的压缩工具。

* 【功能】压缩文件:

  ```shell
  tar -cvf <*.tar> <filename>                 # 仅打包文件
  tar -zcvf <*.tar.gz> <filename>             # 以gzip方式压缩并打包
  tar -jcvf <*.tar.bz2> <filename>            # 以bzip2方式压缩并打包
  ```

* 【功能】解压文件:

  ```shell
  tar -xvf <*.tar>  <path>                    # 解包
  tar -zxvf <*.tar.gz> <path>                 # 以gzip方式解压并解包
  tar -jxvf <*.tar.bz2> <path>                # 以bzip2方式解压
  ```
  
## 设备管理

* 【功能】显示设备信息：

  ```shell
  #　显示磁盘uuid。
  blkid
  # 检查磁盘。
  fsck
  # 查看已挂载磁盘信息。
  df
  #　查看文件内存信息。
  du
  ```

  > Note：开机时自动执行`etc/re.d/re.local`脚本文件。

* 【功能】挂载外部设备：

  ```shell
  # 挂载外部设备。
  mount <option> <devicename>
  ```

  > Note：挂载配置文件`etc/fstab`。

* 【功能】卸载外部设备：

  ```shell
  # 卸载外部设备。
  umount <option> <devicename>
  ```

* 【功能】存储设备分区：

  ```shell
  fdisk
  ```

* 【文件】自动挂载的配置文件`etc/fstab`：

  ```shell
  <设备名> <挂载点> <文件系统类型> <挂载选项>
  ```

## 任务管理

### 进程管理

* 【功能】查询进程信息：

  ```shell
  # 打印所有运行的进程。
  ps -a
  ps -aux
  ```

* 【功能】树状形式显示进程。

  ```shell
  # 以树状的形式显示所有进程。
  pstree
  ```

* 【功能】监控进程所使用的资源。

  ```shell
  top
  htop
  ```

* 【功能】设置和改变进程的优先级。

  ```shell
  nice
  renice
  ```

* 【功能】结束进程。

  ```shell
  kill
  killall
  pkill
  ```

* 【功能】控制系统资源在shell和进程上的分配量。

  ```shell
  ulimit -a
  ```

* 【功能】所有登陆用户的信息。

  ```shell
  w
  who
  whoami
  ```

* 【功能】进程全剧正则匹配输出。

   ```shell
   pgrep
   ```

  * 【功能】后台执行进程：

    ```shell
    # 将后台进程调到前台。
    fg %<>
    # 将前台进程调到后台。也可以通过Ctrl+Z实现。
    bg
    # 现实后台运行进程。
    jobs
    ```

* 【功能】报告进程见通信设施状态。

  ```shell
  ipcs -p -m
  ```

### 计划作业

* 【命令】`crontab`：定时执行任务。
  
  ```shell
  # 进入任务编辑模式。
  crontab
  # 进入默认编辑器任务编辑模式。
  crontab -e
  # 显示需要执行任务。
  crontab -l
  # 取消定时任务。
  crontab -r
  # 指定脚本定时计划。
  ```

  > Note：无论是进入任务编辑模式，还是脚本执行，格式都是`<minute> <hour> <day> <month> <week> <command>`。该命令是基于crond服务的。

* 【命令】`at`：定时执行任务。

  ```shell
  # 进入任务编辑模式。
  at <hour>:<minute>
  # 显示所有需要执行的任务。
  atq
  #显示定时任务详细内容。
  at -c <number>
  # 删除定时任务。
  atrm <number>
  ```

## 服务管理

在原来的`service`与`chkconfig`工具的基础上,开发了`systemctl`工具;

* 【功能】启动服务:

  ```shell
  systemctl start <serviceName>             # 启动服务
  systemctl enable <serviceName>            # 开机启动服务 
  ```

* 【功能】重启服务:

  ```shell
  systemctl restart <serviceName>
  ```

* 【功能】查询状态:

  ```shell
  systemctl status <serviceName>          # 查看服务状态
  systemctl is-enabled <serviceiceName>   # 查看服务是否开机启动
  systemctl list-unit-files | grep enabled # 查看已启动的服务
  systemctl --failed                      # 查看启动失败的服务
  ```

* 【功能】关闭服务:

  ```shell
  systemctl stop <serviceName>            # 关闭服务
  systemctl disable <serviceName>         # 开机禁用服务
  ```

## 网络管理

* 【功能】命令的别名:

  ```shell
  alias   <name> = <command>
  unaliax <name>
  ```

* 【功能】网络的连通信:

  ```shell
  ping <IP>
  netsat
  ```

* 【功能】手动同步时间: `ntpdate -u cn.pool.ntp.org`,利用NTP服务;

* 【命令】`exec`：用于调用并执行指令的命令。

  ```shell
  exec <option> <partameter>
  ```

  > * `-c`：在空环境值执行指定的命令。

* 【命令】`lsof`：是一个集系统管理与系统安全的工具。
* 【命令】`tcpdump`：
* 【命令】`route`：路由表。
* 【命令】`arp`：
