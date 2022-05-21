title: 【对象储存】backblaze搭配CF实现流量费全免！
categories: 教程
tags: [CDN,CLOUDFLARE,对象储存]
date: 2022-05-12 11:47:00
---
对象储存在大家眼里一般都是富人的玩具，穷人的地狱，对象储存虽然服务优质，但他高昂的价格让众多站长望而止步。

CloudFlare是世界顶级的CDN服务商，他以强大的防御和优质的服务享誉全球。CloudFlare与众多云服务商构建带宽联盟为用户们省下了高昂的流量费。本篇文章将结合我自己在Backblaze（B2）和CloudFlare（CF）的探索和经验，展示一些B2免流技巧。



# 介绍

## 带宽联盟

带宽联盟是以CF为主导和一群具有前瞻性思维的云服务和网络公司，致力于为共同客户降低或免除数据传输（带宽）费用。带宽联盟的合作伙伴现已扩展到总计20个！

官方页：https://www.cloudflare.com/zh-cn/bandwidth-alliance/



# 教程开始

## 解析域名

需要将绑定在CF的域名通过CNAME的方式，解析至f002.backblazeb2.com，并开启黄色小云朵后，就完成了B2于CF的初步结合。

![ecce591630c92573f35a9eca15360102.png](https://sign.omege.cc/2022/05/12/ecce591630c92573f35a9eca15360102.png)

解析后，我们就可以将https://f002.backblazeb2.com/file/bucket_name/file_name中的f002.backblazeb2.com替换为你所解析的二级域名，查看是否可以正常加载，如果正常那么第一步就完成了。

## 隐藏储存桶

完成第一步后，虽然B2已经可以免流量了，但这样会暴露你的bucket_name，别人只需要再将你的域名替换为B2官方的下载域名，你的B2依然会照常扣费。所以我采用CF提供的URL转换来进行隐藏URL中的bucket_name。

我们在`规则`页面点击`转换规则`，之后再点击`新建转换规则`并选择`重写URL`，规则名称随意填写，传入请求匹配按照下图替换填写。并找到下方的路径点击重写到并切换至`Dynamic模式`，将/file/bucket_name中的bucket_name替换为你的bucket_name即可。

![ba1006a52b184d809965d82861cdd47e.png](https://sign.omege.cc/2022/05/12/ba1006a52b184d809965d82861cdd47e.png)

```
#隐藏URL中/file/bucket_name
concat("/file/bucket_name", http.request.uri.path)
```



## 隐藏标头

我们已经隐藏了URL中的储存桶，但是有心人可以通过F12的的Network选项卡暴露出来，这也是对象储存的一个特性。经过我的测试，B2并不会通过标头来暴露bucket_name，但依然会暴露自己是储存对象这个事实，为了避免被盗刷流量而造成高额的费用。所以我采用CF转换规则中的修改响应头来实现标头的隐藏，同时也可以借此来设置跨域和请求方式的限制。

![361f2cff8598b6daf3332656e1a20a73.png](https://sign.omege.cc/2022/05/12/361f2cff8598b6daf3332656e1a20a73.png)

索要隐藏标头如下：

- x-bz-file-name
- x-bz-file-id
- x-bz-content-sha1
- x-bz-info-s3b-last-modified
- x-bz-info-sha256
- x-bz-upload-timestamp



# 结束

教程到了这里，差不多要结束了，本篇主要讲了B2的URL隐藏和标头的隐藏。做了以上这些策略，你的B2几乎已经可以完全隐藏他对象储存的身份了。

参考文献：

[1](https://www.backblaze.com/blog/backblaze-and-cloudflare-partner-to-provide-free-data-transfer/)