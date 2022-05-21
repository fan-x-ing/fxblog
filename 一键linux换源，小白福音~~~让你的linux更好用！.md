title: 一键linux换源，小白福音~~~让你的linux更好用！
categories: 教程
tags: [linux,小白,yum源,工具箱]
date: 2021-12-18 12:24:00
---
也有好久没有写文章了，今天就写博客恢复后的第一篇文章吧~

# 为什么要换源？

大家都知道，我们买完vps后会安装系统，大多数小伙伴选择的都是linux系统（centos,debian,ubuntu等）。但是除了deepin，别的linux系统安装完之后下载东西很慢，当然像腾讯云阿里云那些大厂一半已经给你自己换过了源，你也就不用自己换了。但一些小厂是没有的，所以我们要自己换源。

当然，换源也很简单，国内有很多家供你选择：阿里云，腾讯云，华为云等等。但是不管你使用哪种方法，都没有一件脚本简单，所以今天我们来教给大家如何使用一键脚本来换源！！！

## 项目

1. 地址：https://github.com/SuperManito/LinuxMirrors
2. 已经适配的linux系统（复制至github项目开源处）：


| Debian     |  8.0 ~ 11.0  |
| ------------ | :-------------: |
| Ubuntu     | 16.04 ~ 21.04 |
| Kali Linux | 2.0 ~ 2021.2 |
| RHEL       |   7.0 ~ 8.4   |
| CentOS     |   7.0 ~ 8.4   |
| Fedora     |    28 ~ 34    |

> 目前仅支持上述基于 Debian 与 Redhat 系的发行版和及其部分衍生版本 同样支持上述版本中拥有相同底-层核心的其它发行版，例如 [`Armbian`](https://www.armbian.com/) [`Kubuntu`](https://kubuntu.org/) [`Oracle Linux`](https://www.oracle.com/cn/technical-resources) 等

## 当前本项目使用的镜像源列表


| 序号 |    镜像站名称    |                                镜像站地址                                | IPv6 | Kali Linux | Fedora | EPEL |
| :----: | :----------------: | :-------------------------------------------------------------------------: | :----: | :----------: | :------: | :----: |
|  1  |      阿里云      | [mirrors.aliyun.com](https://developer.aliyun.com/special/mirrors/notice) |  √  |     √     |   √   |  √  |
|  2  |      腾讯云      |      [mirrors.cloud.tencent.com](https://mirrors.cloud.tencent.com/)      |  √  |     √     |   √   |  √  |
|  3  |      华为云      |        [mirrors.huaweicloud.com](https://mirrors.huaweicloud.com/)        |  √  |     √     |   √   |  √  |
|  4  |       网易       |                [mirrors.163.com](https://mirrors.163.com/)                |     |           |   √   |     |
|  5  |       搜狐       |               [mirrors.sohu.com](https://mirrors.sohu.com/)               |     |           |       |     |
|  6  |     清华大学     |   [mirrors.tuna.tsinghua.edu.cn](https://mirrors.tuna.tsinghua.edu.cn/)   |  √  |     √     |   √   |  √  |
|  7  |     浙江大学     |             [mirrors.zju.edu.cn](https://mirrors.zju.edu.cn/)             |     |     √     |   √   |  √  |
|  8  |     南京大学     |             [mirrors.nju.edu.cn](https://mirrors.nju.edu.cn/)             |     |     √     |   √   |  √  |
|  9  |     重庆大学     |             [mirrors.cqu.edu.cn](https://mirrors.cqu.edu.cn/)             |     |     √     |   √   |  √  |
|  10  |     兰州大学     |              [mirror.lzu.edu.cn](https://mirror.lzu.edu.cn/)              |  √  |           |   √   |  √  |
|  11  |   上海交通大学   |             [mirror.sjtu.edu.cn](https://mirror.sjtu.edu.cn/)             |  √  |     √     |   √   |  √  |
|  12  |  哈尔滨工业大学  |             [mirrors.hit.edu.cn](https://mirrors.hit.edu.cn/)             |  √  |     √     |       |  √  |
|  13  | 中国科学技术大学 |            [mirrors.ustc.edu.cn](https://mirrors.ustc.edu.cn/)            |  √  |     √     |   √   |  √  |

注意，所有的镜像站均支持 `Debian` `Ubuntu` `CentOS` 镜像源，建议优选选择大厂企业提供的，速度会更快更稳一些。

### 脚本部署

1. 一键更换国内系统源（通过ssh命令行使用）：

```perl
bash <(curl -sSL https://gitee.com/SuperManito/LinuxMirrors/raw/main/ChangeMirrors.sh)
```

2. 安装过程中，可以自己选择源：

![I5AX.png](https://q2.a1pic.cn/2021/12/18/I5AX.png)

## Docker一键安装脚本

1. Docker一键安装脚本：

```perl
bash <(curl -sSL https://gitee.com/SuperManito/LinuxMirrors/raw/main/DockerInstallation.sh)
```

Docker CE：Docker Community Edition 镜像仓库，用于下载并安装相关软件包。

Docker Hub：Docker Hub 镜像仓库，就是Docker镜像仓库的加速器，默认是用的是官方的。

注意：本脚本安装包含`Docker Engine`与 `Docker Compose`，可以自己选择版本和下载源，也可以自己选择镜像源。

### 最后总结及常见问题解决方法

1. 如果你在安装过程中提示`Command 'curl' not found`，那说明你没有安装curl，需要执行：

```perl
sudo apt install -y curl  或  sudo yum install -y curl
```

2. 当提示 `Command 'wget' not found` 时说明你没有安装装 `wget` 软件，这时候需要安装wget，需要执行：

```perl
sudo apt install -y wget  或  sudo yum install -y wget
```

**注意：apt和yum分别是Ubuntu以及centos的安装命令**

总的来说，这个工具箱对小白是十分友好的，他也是开源了的。如果你怕之后这个工具箱闭源而无法调用github文件使用的话，可以把文件下载下来，自己部署到自己的vps或者放在大厂的储存对象中，自己使用也是很不错的。