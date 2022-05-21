title: Cloudreve安装教程！
categories: 教程
tags: [Cloudreve,宝塔版面,LNMP]
date: 2022-05-02 16:38:00
---
# 项目介绍

Cloudreve是一款由Aaron开发的网盘程序，由于Cloudreve部署方式简单-功能强劲，所以做自建网盘等是一个很好的选择。

项目：https://github.com/cloudreve/Cloudreve

文档：https://docs.cloudreve.org/

演示：https://demo.cloudreve.org/

以下是Cloudreve所支持的一些功能：

- ☁️ 支持本机、从机、七牛、阿里云 OSS、腾讯云 COS、又拍云、OneDrive (包括世纪互联版) 作为存储端
- 📤 上传/下载 支持客户端直传，支持下载限速
- 💾 可对接 Aria2 离线下载，可使用多个从机机点分担下载任务
- 📚 在线 压缩/解压缩、多文件打包下载
- 💻 覆盖全部存储策略的 WebDAV 协议支持
- ⚡ 拖拽上传、目录上传、流式上传处理
- 🗃️ 文件拖拽管理
- 👩‍👧‍👦 多用户、用户组
- 🔗 创建文件、目录的分享链接，可设定自动过期
- 👁️‍🗨️ 视频、图像、音频、文本、Office 文档在线预览
- 🎨 自定义配色、黑暗模式、PWA 应用、全站单页应用
- 🚀 All-In-One 打包，开箱即用
- 🌈 ... ...



# 教程开始

## 准备

1. VPS或物理机一台
2. 域名一枚(不介意也可以使用IP访问)
3. 安装宝塔版面或aapanel



本次采用 <font color="red">LNM+Mysql+宝塔版面+Redis</font>来部署。

[scode type="yellow"]服务器一定要安装Linux系统！[/scode]

### 更换yum源

目前已知的yum源有很多，但是我们要挑选适合自己的yum源。
[post cid="21" cover="https://sign.omege.cc/2022/05/01/d8c465dc9dd09115b09fc360a3695b6b.png"/]

如果是国内外大厂的机器，无需进行这一步，他们已经提前预配到系统中了。



## 部署

1. 安装宝塔版面（已安装的可跳过）

**Centos**：

```shell
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh ed8484bec
```

**Ubuntu/Deepin**：

```shell
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh ed8484bec
```

**Debian**：

```shell
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh ed8484bec
```



2. 安装LNM/Redis

宝塔版面在安装好第一次进入面板时，会提醒你安装LNM，根据自己需求安装即可。

随后进入软件商店安装Redis。



3. 创建数据库

此时进入宝塔版面新建数据库即可，GUI界面也是十分简单！



4. 拉取项目

我们需要获取Cloudreve的源文件，可以自己下载后传至服务器，也可以直接使用服务器wegt进行拉取。

[post url="https://github.com/cloudreve/Cloudreve" title="Cloudreve." intro="支持多家云存储驱动的公有云文件系统." /]

```shell
apt -y install wget
wget https://github.com/cloudreve/Cloudreve/releases/download/3.5.3/cloudreve_3.5.3_linux_amd64.tar.gz
```



5. 解压文件

```shell
tar -zxvf cloudreve_3.5.3_linux_amd64.tar.gz
rm -f cloudreve_3.5.3_linux_amd64.tar.gz
```



6. 给予权限

```shell
chmod +x cloudreve
```



7. 编写配置文件

```shell
vim conf.ini
```

配置内容：

```
[System]
; 运行模式
Mode = master
Listen = :5212
Debug = false
SessionSecret = 23333
HashIDSalt = something really hard to guss

[Database]
Type = mysql
Port = 3306
User = 填写你创建数据库时的用户名
Password = 填写你创建数据库时的密码
Host = 127.0.0.1
Name = 填写你数据库名
TablePrefix = cd_
Charset = utf8

[Redis]
Server = 127.0.0.1:6379
Password =
DB = 0
```



8. 启动项目

```
./cloudreve
```

[scode type="yellow"]首次启动项目会出现管理员账号密码，一定要记录下来，方便一会登录[/scode]



9. 暂停项目

为了后边的进程守护，所以我们先暂停项目。同时点键盘上的CTRL+C即可



10. 设置进程守护

[scode type="yellow"]一定要先启动项目停止后再进行进程守护[/scode]

```shell
vim /usr/lib/systemd/system/cloudreve.service
```

内容如下：

```
[Unit]
Description=Cloudreve
Documentation=https://docs.cloudreve.org
After=network.target
After=mysqld.service
Wants=network.target

[Service]
WorkingDirectory=/root
ExecStart=/root/cloudreve
Restart=on-abnormal
RestartSec=5s
KillMode=mixed

StandardOutput=null
StandardError=syslog

[Install]
WantedBy=multi-user.target
```

管理命令：

```shell
# 更新配置
systemctl daemon-reload

# 启动服务
systemctl start cloudreve

# 重启服务
systemctl restart cloudreve

# 设置开机启动
systemctl enable cloudreve
```



11. 设置反代

首先，我们要在宝塔新建站点，数据库和php版本都不需要。

![022af43f06bb0ca395306fa2463258f0.png](https://sign.omege.cc/2022/05/02/022af43f06bb0ca395306fa2463258f0.png)

之后设置反代

![632d9dc33e2ccd716bbafea05d5a1953.png](https://sign.omege.cc/2022/05/02/632d9dc33e2ccd716bbafea05d5a1953.png)

名称随意填写，目标URL一定要填写`http://127.0.0.1:5212`



12. 安装完成

打开你所绑定的域名

![d98803223c8ed7925331a336d2908069.png](https://sign.omege.cc/2022/05/02/d98803223c8ed7925331a336d2908069.png)

这样就安装完成了，然后用你第八步中复制的账号密码来登录，然后在用户管理新建一个方便自己记忆的管理员账号，就可以投入使用了。



## 后续

下一篇我打算写Cloudreve的各个储存的对接,从机离线下载,以及邮件配置等和Cloudreve相关的一些子教程，争取在2-3篇文章内，将cloudreve的基础使用以及一些高级玩法给写出来。
