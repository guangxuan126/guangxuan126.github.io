---
title: shadowsocks脚本
date: 2018-08-19 20:22:42
tags:
    - tools
---

> 引用自 秋水逸冰 提供的脚本， 原文[链接](https://teddysun.com/486.html)

## 适用环境
系统支持： CentOS 6+, Debian 7+, Ubuntu 12+
内存要求: >=128M
更新日期: 2018年6月1日

## 关于
1. 一键安装 Shadowsocks-Python， ShadowsocksR， Shadowsocks-Go， Shadowsocks-libev 版服务端；
2. 各版本启动脚本启动脚本及配置文件名不在重合；
3. 每次运行可安装一种版本；
4. 支持安装多个版本，且各版本可以共存（需端口号设置成不同）；
5. 若安装多个版本，卸载时需要对应版本；

#### Tips：如果有问题可以参照这篇《[Shadowsocks Troubleshooting](https://github.com/shadowsocks/shadowsocks/wiki/Troubleshooting)》

## 默认配置
服务器端口：自己设定（如不设定，默认从 9000-19999 之间随机生成）
密码：自己设定（如不设定，默认为 teddysun.com）
加密方式：自己设定（如不设定，Python 和 libev 版默认为 aes-256-gcm，R 和 Go 版默认为 aes-256-cfb）
协议（protocol）：自己设定（如不设定，默认为 origin）（仅限 ShadowsocksR 版）
混淆（obfs）：自己设定（如不设定，默认为 plain）（仅限 ShadowsocksR 版）
**备注：** 脚本默认创建单用户配置文件，如需配置多用户，请手动修改相应的配置文件后重启即可。

## 客户端
Windows: shadowsocks-win:[Github](https://github.com/shadowsocks/shadowsocks-windows/releases)
MacOS: ShadowsocksX-NG:[Github](https://github.com/shadowsocks/ShadowsocksX-NG/releases)
Linux: Shadowsocks-Qt5:[Github](https://github.com/shadowsocks/shadowsocks-qt5/wiki/Installation)

## 使用方法
使用root登录，运行以下命令:
```
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

## 安装成功后，有如下提示:
```
Congratulations, your_shadowsocks_version install completed!
Your Server IP        :your_server_ip
Your Server Port      :your_server_port
Your Password         :your_password
Your Encryption Method:your_encryption_method

Your QR Code: (For Shadowsocks Windows, OSX, Android and iOS clients)
 ss://your_encryption_method:your_password@your_server_ip:your_server_port
Your QR Code has been saved as a PNG file path:
 your_path.png

Welcome to visit:https://teddysun.com/486.html
Enjoy it!
```

## 卸载方法
使用root登录，运行以下命令：
```
./shadowsocks-all.sh uninstall
```

## 启动脚本
启动脚本后面的参数含义，从左至右依次为：启动，停止，重启，查看状态。

Shadowsocks-Python 版：
`/etc/init.d/shadowsocks-python start | stop | restart | status`

ShadowsocksR 版：
`/etc/init.d/shadowsocks-r start | stop | restart | status`

Shadowsocks-Go 版：
`/etc/init.d/shadowsocks-go start | stop | restart | status`

Shadowsocks-libev 版：
`/etc/init.d/shadowsocks-libev start | stop | restart | status`

## 各版本配置文件
Shadowsocks-Python 版：
`/etc/shadowsocks-python/config.json`

ShadowsocksR 版：
`/etc/shadowsocks-r/config.json`

Shadowsocks-Go 版：
`/etc/shadowsocks-go/config.json`

Shadowsocks-libev 版：
`/etc/shadowsocks-libev/config.json`