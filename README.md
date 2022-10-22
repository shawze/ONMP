# 介绍

Forked form https://github.com/xzhih/ONMP

适用于安装了Entware固件的onmp一键安装命令,  forked `xzhih`的项目修正部分错误，适配B860等盒子, 同时增加samba、aria2等工具, 目前已经在Padavan、LEDE、梅林、B860A盒子上测试成功.

后续待增加功能【todolist】：

- 中闪B860A等盒子，一键安装entware, 
- 脚本更改opkg为国内源
- php8 目前运行不正确 [部分php程序不能正常运行]
- 部分web程序不能正常安装、未更新至新版

```
=======================================================
(1) 安装基础工具包[否则脚本无法运行]
(2) 开启Swap[小内存时需开启,否则MaraDB易安装失败]
-------------------------------------------------------
(3) 安装Nginx&MaraDB&PHP[会删除网站目录, 请注意备份]
(4) 安装Node与配置服务器
(5) 设置数据库密码
(6) 重置数据库
(7) 数据库自动备份
(8) 安装网站程序
(9) 添加Nginx服务器代理
(10) 删除网站
(11) 更新网站目录到默认网站
(12) 全部重置[会删除网站目录, 请注意备份]
(13) 卸载Nginx&MaraDB&PHP
-------------------------------------------------------
(14) 开启Redis
(15) Samba[文件共享]
(16) Aria2[下载工具]
(17) 磁盘链接到/opt/mnt
(18) entware更改为国内源
(0) 退出
=======================================================
```

Web安装目录

```
(1) phpMyAdmin（数据库管理工具）
(2) WordPress（使用最广泛的CMS）
(3) Owncloud（经典的私有云）
(4) Nextcloud（Owncloud团队的新作，美观强大的个人云盘）
(5) h5ai（优秀的文件目录）
(6) Lychee（一个很好看，易于使用的Web相册）
(7) Kodexplorer（可道云aka芒果云在线文档管理器）
(8) Typecho (流畅的轻量级开源博客程序)
(9) Z-Blog (体积小，速度快的PHP博客程序)
(10) DzzOffice (开源办公平台)
(11) Kodbox(可道云)
(12) AriaNG(Aria WebUI)
(13) Piwigo(开源相册)
```



# 安装教程

## 1. 安装 Entware

Entware-ng 是一个适用于嵌入式系统的软件包库，使用 opkg 包管理系统进行管理，现在在官方的源上已经有超过 2000 个软件包了，可以说是非常的丰富；

[在 LEDE 上使用 Entware](https://github.com/xzhih/ONMP/wiki/在-LEDE-上安装-Entware)

[在梅林上使用 Entware](https://github.com/xzhih/ONMP/wiki/在梅林上安装-Entware)

[在 Padavan 上使用 entware](https://github.com/xzhih/ONMP/wiki/在-Padavan-上安装-Entware)

修改为[北京外国语大学开源软件镜像站](https://mirrors.bfsu.edu.cn/entware/)

```
sed -i 's|bin.entware.net|mirrors.bfsu.edu.cn/entware|g' /opt/etc/opkg.conf
```

## 2. 安装onmp

- 一键命令(githubusercontent.com易连接失败； 使用此命令前确认 curl 是否安装)

```
$ sh -c "$(curl -kfsSl https://raw.githubusercontent.com/shawze/ONMP/master/oneclick.sh)"
```

- 一键安装如果出错，可以按以下步骤一步步安装：

```
# 进入 entware 挂载目录
cd /opt && opkg install wget unzip  wget-ssl 

# 下载软件包
wget --no-check-certificate -O /opt/onmp.zip https://github.com/shawze/ONMP/archive/master.zip 

# 解压
unzip /opt/onmp.zip
mv /opt/ONMP-master /opt/onmp
cd /opt/onmp

# 设置权限
chmod +x ./onmp.sh 

# 运行
sh onmp.sh 
```



# ONMP 命令使用教程

```
管理：onmp open
启动、停止、重启: onmp start|stop|restart
查看网站列表: onmp list 
Nginx 管理命令:  onmp nginx start|restart|stop
PHP 管理命令: onmp php start|restart|stop
Redis 管理命令: onmp redis start|restart|stop
```
