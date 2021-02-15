# Windows注册表管理

[//]: # (__author__ = "Clark Aaron")
[//]: # (__version__ = "v0.0")

注册表实质是一个庞大的数据库，存储了关于计算机硬件的全部配置信息、系统和软件的初始化信息、应用软件和文档文件的关联关系、硬件设备的说明以及各种状态信息和数据；注册表编辑器Regedit是管理注册表的工具。注册表由五大根键、子健、键值项、键值，在win98中将子健称为主键。

* `HKEY_CLASES_ROOT`：包含启动应用程序所需要的全部信息。
* `HKEY_CURRENT_USER`：管理与当前登录用户有关的信息。
* `HKEY_LOCAL_MACHINE`：保存了Windows的信息，包含了应用程序、驱动程序以及硬件信息。
* `HKEY_USERS`：包含所有的用户配置文件的前活动用户信息。
* `HKEY_CURRENT_CONFIG`：是HKEY_LOCAL_MACHINE的映射，

## 基础键值项

| 键值项 | 主键 | 类型 | 键值 | 说明 |
|:------:|:---- |:---:|:---- |:---- |
| InitialKeyboardIndicators | HKEY_USERS\\.DEFAULT\Control Panel\Keyboard | REG_SZ | {0,2} | 让<kbd>NumLock</kbd>登录后自动开启,0表示关闭,2表示开启 |
| WaitTokillAppTimeOut | HKEY_USERS\\.DEFAULT\Control Panel\Desktop | REG_SE | (0,2000) | 设置"关闭无响应程序"的等待时间 |
| IoPageLockLimit | HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Memory Management | DWORD | (0,4000) | IO缓存大小 |

## cmd

计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor\autorun 

## Diretx

* `dxdiag`

## Administrator

`计算机\HKEY_LOCAL_MACHINE\SAM\SAM`

* Windows 1998登录时点击取消直接进入系统的解决：在`HKEY_LOCAL_MACHINE\Network\Logon`新建DWORD的`MustBeValidated`，值为1；`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Winogon`新建一个DWORD的`MustBeValidated`，值为1；并在Msdos.sys中增加`BootFailSafe=0`来禁止安全模式；即可完成登录时必须输入密码。
* NumLock键登录时开启`HKEY_USERS\.DEFAULT\Control Panel\Keyboard`修改`InitialKeyboardIndicators`值为2，为0时关闭。
* 系统还原功能`HKET_LOCAL_MACHINE\Software\Policies\Microsoft\WindowsNT\SystemRestore`中的`DisableSR`，值为1时开启，0时关闭。
* 磁盘不足警告的临界值`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\LanmanServer\Parameters`中的`DiskSpaceThreshold`的百分比值，默认为10（10%）。
* 磁盘不足时无警告`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`中的`NoLowDiskSpaceChecks`，值为1时启用，0时关闭。
* 媒体设备自动运行`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`中的`NoDriveTypeAutoRun`，255时所有驱动器，181时CD-ROM驱动器。
* 自动保存桌面`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`中的`NoSaveSettings`，0时关闭，1时开启。
* 自动登录`HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\Winlogon`中的`AutoAdminLogon`为1时启动自动登录，`DefaultDomainName`设置默认域名，`DefaultUserName`设置默认用户名，`DefaultPassword`设置默认密码。
* 禁止当前用户访问驱动器`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`中的`NoViewOnDrive`，8时限制D盘。
* 隐藏驱动器`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`中的`NoDrive`,值为8时隐藏D盘。
* 屏蔽任务栏设置`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`中的`NoSetTaskbar`为1时屏蔽设置中的任务栏设置。
* 屏蔽运行与搜索窗口`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`中的`NoRun`为1屏蔽运行，`NoFind`为1屏蔽搜索，`NoClose`为1屏蔽关闭计算机。
* 禁止修改系统字体大小`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\System`中的`NoSizeChoice`为1。
* 隐藏修改系统显示属性`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\System`中的`NoDisAppearancePage`为1隐藏外观，`NoDispScrSavPage`为1隐藏屏幕保护程序，`NoDispSettingPage`为1隐藏桌面、主题、设置，`NoDispCPL`为1时隐藏显示组件。
* 禁止修改桌面背景`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\ActiveDesktop`中的`NoChangingWallPaper`为1禁用。
* 禁止修改系统主题`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Expolorer`中的`NoThemesTab`为1禁用。
* 隐藏控制面板`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`中的`NoControlPanel`为1时隐藏。
