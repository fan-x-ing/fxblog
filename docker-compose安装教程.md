title: docker-compose安装教程
categories: 教程
tags: [linux,docker,宝塔]
date: 2021-08-31 12:20:00
---
宝塔版面安装docker就不说了，在应用商店安装即可。但是怎么安装`docker-compose`呢？宝塔并没有这个插件，我们只能手动安装了。这篇文章就教大家如何安装`docker-compose`。



# 教程开始

![1](https://q2.a1pic.cn/BWoE.webp)

## 指令安装docker

先说下安装`docker`，别习惯了一键安装，就忘了指令。命令如下：

```
curl -sSL https://get.docker.com/ | sh
systemctl enable --now docker
```



## 安装docker-compose

这个方法是最简单的，如果要别的版本，把`1.28.5`替换成你想要的版本就行。

```
curl -L https://github.com/docker/compose/releases/download/1.28.5/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

安装完成后再检查下版本，命令如下：

```
docker-compose -v
```



## pip安装docker-compose

我们这里以安装过宝塔版面的centos7.6来作示范。

注意：我们这里要安装`python`>=3.5，如果是宝塔使用试验版进行安装。

```
yum -y install epel-release  #安装了宝塔这个就不需要安装了。
yum -y install python-pip
pip install docker-compose
```

接下来需要检查`pip`版本，命令：pip --version



## 卸载

如果你是使用`curl`安装的`docker-compose`，那么请通过下面这个指令：

```
sudo rm /usr/local/bin/docker-compose
```



如果你是使用`pip`安装的，请使用下面的指令：

```
pip uninstall docker-compose
```



## 结尾

项目：https://github.com/docker/compose

文档：https://docs.docker.com/compose/install/