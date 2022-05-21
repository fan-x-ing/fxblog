title: 宝塔面板安装iFileSpace，一键搭建专属的私人网盘系统
categories: 教程
tags: [宝塔,iFileSpace,云盘,OneDrive,COS]
date: 2021-09-14 12:22:00
---
`iFileSpace`是一个款个人文件管理工具，在线网盘。是一款可以快速部署的在线网盘系统，支持本地和储存对象（`阿里云oss`，`华为云obs`，`onedrive`），可以部署在`公网服务器`，`nas`，`树莓派`等。可以代替百度网盘等，自主搭建，数据可控！！！支持多用户，`webdav`等

![fanxing/599e30914111753.png](https://b.idccq.cn/tc/fanxing/toGBPN5w.webp)



**iFileSpace功能如下**：

- 支持第三方存储（目前支持阿里云oss，华为云obs，OneDrive）。
- 第三方存储不受服务器带宽限制，客户端直传。
- 支持`WebDav`。
- 支持相册备份。
- 文件及文件夹管理、分享。
- 支持直链分享、密码分享、群组分享及用户间分享。
- 支持视频、图像、音频、文本、Office 文档、PDF 在线预览。
- 支持多用户，多存储空间，多存储策略。
- 提供`IOS`，`Android`客户端。
- 提供`windows`,`macos`桌面客户端，管理分享文件更方便。
- 支持定时文件扫描，自动更新用户文件夹下文件、目录。
- 单文件打包，部署更简单。
- 提供Docker版。
- Web版支持自定义Logo及首页。



# 开始搭建

## 简介

官网：https://ifile.space/

下载：https://ifile.space/download

文档：https://ifile.space/docs/home

演示：https://demo.ifile.space



## 准备

- 宝塔版面
- nginx
- Supervisor管理器



## 开始部署

1. 新建站点，略过~~

2. 下载程序，在官网点击`下载`，找到`linux`版本下载，之后`上传`到网站的根目录`解压`，解压后有一个`ifile`文件。

3. 配置`Supervisor管理器`，如下图：

![fanxing/484910914113002.png](https://q2.a1pic.cn/B2Ut.webp)



4. 在`Supervisor管理器`日志处查看：

![fanxing/e77a90914113147.png](https://q2.a1pic.cn/B3o3.webp)



5. 查看账户密码

这里是看不到账号密码的，我们需要在终端出输入以下代码：

```
cd /www/wwwroot/halo.vsvs.xyz  #首先进入目录，注意修改为自己的。
 ./ifile -resetpass  #执行密码初始话命令
2021/09/08 09:02:16 重置密码成功： OHDMGPLk
```

- 用户名：admin，密码：就是上面的密码。
- 登录地址：启动后浏览器打开 http://127.0.0.1:3030 访问，如果你是用服务器安装的就需要用<你的服务器IP:3030>来访问了。
- 如果不能访问，记得在宝塔安全里面放行3030端口。

6. 设置域名访问

这里我们需要在宝塔面板反代，ssl记得在反代前申请好。

![fanxing/471e30914113942.png](https://q2.a1pic.cn/B4N1.webp)



这样就安装完成了