title: NGINX和MySQL手动安装[笔记]
categories: 教程
tags: [服务器,linux,笔记,nginx,MySQL]
date: 2022-01-15 12:26:00
---
关于我为什么要学手动安装nginx以及mysql这件事呢，还是要关于我想把cloudreve教程重写一遍的原因。昨天我看了好兄弟`AHdark`的cloudreve的安装教程，我又看了看我的，然后发现我教程真垃圾。方法单一，讲解粗略。所以我就打算把这个教程重新写一遍，但是有一种方法要用到纯nginx和mysql环境。由于我入坑vps一直是用的宝塔版面，所以对这方便一概不懂，然后今天就开始学，这也算是做一个笔记吧。
我是使用centos的用户，所以本篇所有方法仅适用于centos系统。

# MySQL安装

## YUM安装

由于centos系统的yum源中没有内置mysql，所以我们需要下载官方的rpm包。但是他内置了mysql的分支`mariadb`，mariadb也是兼容mysql的。但是出于某些原因，我还是要安装mysql。

1. 前往mysql官网下载官方rpm包
2. 安装官方rpm包
3. 安装mysql

命令如下

```
wget https://dev.mysql.com/get/mysql80-community-release-el7-4.noarch.rpm
yum install -y mysql80-community-release-el7-4.noarch.rpm
yum install -y mysql
```

这样mysql就安装完成了

# NGINX安装

## 官方代码编译安装

由于centos官方的yum源中，内置的nginx的版本十分老旧，已经无法正常使用，虽然nginx的官方也有像mysql一样的rpm包，但是我选择编译安装nginx。

以下安装的所有东西根据你当前系统来定，如果已经案追昂过了，那就不需要再安装了。

1. gcc
   由于nginx需要gcc环境，所以我们安装gcc

```
yum install gcc-c++
```

2. pcre
   PCRE是一个perl库，nginx的http模块需要pcre来解析正则表达式，所以我们安装pcre库。

```
yum install -y pcre pcre-devel
```

3. zilb
   zilb支持许多压缩和解压缩的格式，nginx需要用zilb来对http包的内容进行gzip压缩。

```
yum install -y zlib zlib-devel
```

4. openssl
   openssl是个很强大的安全套接密码层，包括了主要的证书秘钥管理以及ssl功能。nginx还支持https，所以要用openssl。

```
yum -y install pcre  pcre-devel zlib  zlib-devel openssl openssl-devel
```

完成这些之后，我们就可以开始安装nginx了

首先我们要在你的centos服务器下载nginx的源代码包。可以前往nginx官网进行下载。官网上拥有三种版本，我们只需要下载`Stable version`最新的稳定版就可以了。

我们复制链接，然后在服务器上下载即可。

```
wget https://nginx.org/download/nginx-1.20.2.tar.gz
# 如果报错那就输入yum install wget来进行安装wget就行
```

然后我们需要把压缩包解压到/usr/local/目录

```
tar -xvf nginx-1.20.2.tar.gz -C /usr/local
```

然后我们要用需要进入到nginx-1.20.2目录，来用cofigure创建一个makefile文件，来为后边的编译做准备，没有这个的话编译会报错的。

```
./cofigure \
--prefix=/usr/local/nginx \
--pid-path=/var/run/nginx/nginx.pid \
--lock-path=/var/lock/nginx.lock \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log \
--with-http_gzip_static_module \
--http-client-body-temp-path=/var/temp/nginx/client \
--http-proxy-temp-path=/var/temp/nginx/proxy \
--http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
--http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
--http-scgi-temp-path=/var/temp/nginx/scgi \
--with-http_stub_status_module \
--with-http_ssl_module \
--with-file-aio \
--with-http_realip_module
```

由于上边得配置文件吧临时文件目录放到了/var/temp/nginx，我们要在/var/temp处新建nginx文件夹

```
mkdir /var/temp/nginx -p
```

然后回到ssh，使用`make`进行编译。这里直接输入make就行。然后再输入`make install`，进行安装即可。

安装完后，我们可以进入安装位置/usr/local/nginx进行查看结构，指令如下：

```
cd /usr/local/nginx
ll
```

## 启动nginx

我们需要进入nginx的sbin目录，然后输入`./nginx`即可。

## 查看是否启动

直接在ssh处输入`ps -aux | grep nginx`即可，ps是查看系统当前的进程状态

## 关闭nginx

```
./nginx -s stop # 强制关闭
./nginx -s quit #等待当前进程结束后再关闭
```

## 重载nginx配置文件

```
./nginx -s reload
```
