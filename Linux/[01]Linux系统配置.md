# Linux系统配置

[//]: # (__author__ = "Clark Aaron")

Linux系统的开源就决定了Linux系统的高度自定义的特性。在搭建好Linux环境之后，我们可以个性化定制来便于自己的使用。

## 桌面环境

### Gnome

GNOME(The GNU Network Object Model Environment, GNU网络对象模型环境), 即GNOME项目(属于GNU项目的子项目); 典型的GNOME桌面环境包括面板、
菜单、窗口、工作区、Nautilus文件管理器、桌面、首选项。

* 安装`X Window System`

  ```shell
  yum groupinstall "X Window System"
  ```

* 安装`GNOME Desktop` 与`Graphical Administration Tools`

  ```shell
  yum groupinstall "GNOME Desktop" "Graphical Administration Tools"
  ```

* 进入桌面环境

  ```shell
  startx
  ```

* 设置默认运行

  ```shell
  ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
  ```

### KDE

KDE(K Desktop Environment, K桌面环境), 先于GNOME桌面环境.是TrollTech公司的专利技术.开发语言为C++.提供Qt/KOM/OpenParts开发平台组合。

### 个性化

#### 修改用户目录名称

* 修改配置文件`~/.config/user-dirs.dirs`中信息。
* 修改实际目录名。
* 更新配置文件：

  ```shell
  source ~/.config/user-dirs.dirs
  ```

#### 更换shell

* 下载zsh,并按装oh-my-zsh。

* 【功能】设置默默shell:

  ```shell
  chsh -s /bin/zsh
  ```

* 【功能】

## 网络环境

### 防火墙

防火墙是保护网络的，其配置文件`/etc/sysconfig/iptables`。

* 【功能】开启防火墙服务：

  ```shell
  systemctl start firewalld
  ```

* 【功能】查询防火墙状态：

  ```shell
  systemctl status firewalld
  ```

* 【功能】关闭防火墙服务：

  ```shell
  systemctl stop firewalld
  ```

* 永久设置功能: `firewall-cmd --permanent`;

* 查看防火墙状态:`firewall-cmd --state`;
  
* 更新防火墙规则:`firewall-cmd --reload`;

* 检查防火墙规则: `firewall-cmd --check-config`;

* 智能帮助: `firewalld-cmd --get-automatic-helpers`;

* 获取日志信息: `firewall-cmd --get-log-denied`;
  
* 获取默认区域: `firewall-cmd --get-default-zone`;

* 获取当前域: `firewall-cmd --get-active-zones`;

* 获取服务: `firewall-cmd --get-services`;

* 查看已开放端口:`firewall-cmd --zone=public --list-ports`;

* 查看区域信息:`firewall-cmd --get-active-zones`;

* 查看指定接口所属区域:`firewall-cmd --get-zone-of-interface=eth0`;
  
* 拒绝所有包:`firewall-cmd --panic-on`;
  
* 取消拒绝状态:`firewall-cmd --panic-off`;
  
* 查看是否拒绝:`firewall-cmd --query-panic`;

* 列出支持的zone:`firewall-cmd --get-zones`;
  
* 列出支持的服务:`firewall-cmd --get-services`;
  
* 查看指定服务是否开放:`firewall-cmd --query-service ftp`;
  
* 临时开放ftp服务:`firewall-cmd --add-service=ftp`;
  
* 永久开放ftp服务:`firewall-cmd --add-service=ftp --permanent`;
  
* 查看防火墙规则:`iptables -L -n`;
* 查看指定端口是否开放:`firewall-cmd --zone= public --query-port=80/tcp`;
* 开放指定端口:`firewall-cmd --zone=public --add-port=80/tcp --permanent`;
* 删除指定端口:`firewall-cmd --zone= public --remove-port=80/tcp --permanent`;

### 科学上网

#### SSR

#### v2ray

<!-- https://www.hijk.pw/centos-one-click-install-v2ray/ -->

### 远程连接

#### SSH

ssh服务守护进程，ssh服务由openssh、openssl组成。ssh服务端产生密钥对（公钥768bit，私钥256bit），在确认IP之后，将公钥发送给客户端，客户端将私钥与公钥结合成密钥对返回给服务端确认，建立一个密钥对传输。

ssh1无密钥校验技术，ssh2支持RSA与DSA密钥。

## 开发环境

### pkg-config用法

* 简述: --- `pkg-config`是获某一个库/模块的所有编译相关信息的工具.

* 获取一个第三方库的头文件信息:

  ```shell
  pkg-config --cflags gtk+-2.0 // gtk+-2.0 作为举例,可以更换为其他模块名
  ```

* 获取一个第三方库的库文件信息:

  ```shell
  pkg-config --libs gtk+-2.0
  ```

* 获取一个模块的头文件及库文件信息:

  ```shell
  pkg-config --cflags --libs gtk+-2.0
  ```
