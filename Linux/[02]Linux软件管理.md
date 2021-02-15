# Linux软件管理

[//]: # (__author__ = "Clark Aaron")

## 资源连接

* [Linux命令大全](https://man.linuxde.net/yum) > <https://man.linuxde.net/yum>

## 管理工具

Linux常使用的软件有deb、rpm包以及源码压缩包三种。

### dpkg

dpkg是Debian基于deb软件包管理的工具。只能管理本地deb包，不能从互联网上下载软件包，也不能解决软件以来问题。

* 【功能】安装软件包:

  ```shell
  dpkg -i <package.deb>                       # 安装软件包
  dpkg -unpack <package.deb>                  # 对deb包进行解包
  ```

* 【功能】删除软件包:

  ```shell
  dpkg -r <packagename>                       # 删除软件包
  dpkg -P <packagename>                       # 删除软件包及配置文件
  ```

* 【功能】查询软件包：

  ```shell
  dpkg -L <packagename>                       # 显示与包有关的文件
  dpkg -l <packagename>                       # 显示该包的信息
  dpkg -l                                     # 显示已安装的包
  dpkg -S <packagename>                       # 查询文件与安装包的关系
  dpkg -c <packagesname>                      # 列出deb包的内容
  dpkg -configure <packagename>               # 配置包
  ```

### rpm

[rpm](https://rpm.org/)（RPM Package mannager）由Red Hat开发的用于管理rpm软件包的软件包管理器。

### yum

yum（Yellow dog Updater Modified）是杜克大学为了提高rpm软件包安装性而开发的一种软件包管理器。能够从指定服务器自动下载rpm包并且自动安装，可
以自动处理依赖关系。

#### yum软件源配置

yum是基于repository的，每一个repository的具体配置是在`/etc/yum.repo.d/`中，全局配置信息在`/etc/yum.conf`中。

* 【功能】仓库源管理：

  ```shell
  # 列出所有仓库。
  yum repolist all
  # 列出可用的仓库
  yum repolist enable
  # 列出不可用的仓库
  yum repolist disabled
  ```

* 【功能】仓库源更换：

  * 首先备份原软件库：

    ```shell
    # 备份/etc/yum.repo.d/CentOS.repo。
    mv /etc/yum.repo.d/CentOS-Base.repo /etc/yum.repo.d/CentOS-Base.repo.backup
    ```

  * 修改配置文件`/etc/yum.repo.d/CentOS.repo`。

  * 更新软件包缓冲：

    ```shell
    yum makecache
    ```

* 【功能】软件包缓存：

  ```shell
  # 清理软件包缓存。
  yum clean all
  # 更新软件包缓存。
  yum makecache
  ```

#### yum软件包管理

* 【功能】安装软件：

    ```shell
    # 安装仓库内软件。
    yum install <package.rpm>
    # 安装本地软件包。
    yum localinstall <package.rpm>
    ```

* 【功能】查询软件：

  ```shell
  yum search <package.rpm>
  yum info <package.rpm>
  # 显示所有已安装的软件。
  yum list installed
  ```

* 【功能】更新软件：

  ```shell
  # 检查可更新的软件。
  yum check-update
  # 更新软件。
  yum update <package.rpm>
  # 系统升级。
  yum upgrade
  ```

* 【功能】卸载软件：

  ```shell
  yun remove <package.rpm>
  ```

* 【功能】重装软件：

  ```shell
  yum reinstall <package.rpm>
  ```

* 【功能】软件依赖：

  ```shell
  yum deplist <package.rpm>
  ```

### apt

apt(Advanced Packaging Tool)是一款安装包管理工具，其中apt-get用于管理deb软件包，apt-。

#### apt软件源管理

* 【功能】软件源更换：

  * 修改`/etc/apt/sources.list`。

  * 添加密钥：

    ```shell
    apt-key adv --keyserver keyserver.ubuntu.com --recv-key <源的16位十六进制码>
    ```

#### apt软件包管理

* 【功能】安装软件:

  ```shell
  apt-get install <packagename>               #  安装软件包
  apt-get install <packagename> --reinstall   # 重新安装软件包
  apt-get -f install                          # 修复安装
  apt-get build-dep <packagename>             # 安装软件相关的编译环境
  apt-get download <packagename>              # 只下载安装包
  ```

* 【功能】更新软件:

  ```shell
  apt-get update
  apt-get upgrade                             # 更新已安装的包
  apt-get dist-upgrade                        # 升级系统
  ```

* 【功能】删除软件

  ```shell
  apt-get remove <packagename>                # 删除软件包
  apt-get remove <packagename> --purage       # 删除软件包以及配置文件
  apt-get autoremove                          # 自动删除不需要的包
  ```

* 【功能】搜索软件

  ```shell
  apt-cache search <packagename>              # 搜索软件包
  apt-cache show <packagename>                # 显示软件包的相关信息
  apt-cache depends <packagename>             # 了解软件包依赖的软件包
  apt-get source <packagename>                # 下载软件包的源代码
  ```

### pacman

pacman是Arch的软件包管理工具，其目的是简化软件包的管理。

#### pacman软件源管理

#### pacman软件包管理

## 源码的打包

### deb

### rpm
