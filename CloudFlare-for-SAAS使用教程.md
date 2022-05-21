title: CloudFlare for SAAS使用教程
categories: 分享
tags: [CDN,CLOUDFLARE]
date: 2022-05-08 15:51:00
---
CloudFlare（之后简称为CF）是世界领先的CDN服务商，之前我们通过[*CloudFlare* Partner](https://www.cloudflare.com/zh-cn/partners/)来CNAME接入，但是近期*CloudFlare* Partner的api失效，也就是说，不能通过这个方式来CNAME接入了。但是，CF官方又放出了另一个产品，好像是为了弥补CloudFlare Partner一样。没错，就是SAAS，官方CNAME接入。

![7f0fb40e89221ddbad10aa5c3b74d2b9.png](https://sign.omege.cc/2022/05/08/7f0fb40e89221ddbad10aa5c3b74d2b9.png)

**准备**：

1. CloudFlare账号一枚

1. 空闲域名一枚

1. ~~脑子一个~~

1. 耐心MAX



# 教程开始

1. 绑定域名（已有绑定域名的可以跳过这一步）

使用SAAS需要有一款域名通过NS的方式绑定在CloudFlare上，可以挑一个无用域名绑定。也可以绑定tk，ml这些免费域名。



2. 绑定支付方式（已绑定的可以跳过这一步）

SAAS需要绑定支付方式，支持Paypal以及银行卡等方式，这里推荐paypal，绑定方便。

也可以在第三步的时候再绑定。



3. 开通自定义主机名（SAAS）

我们进入CloudFlare的域名管理页面，点击SSL/TLS选项，进入自定义主机名，再点击启动CloudFlare for SaaS。

![30a61726dee28e5617a66801e2af0c14.png](https://sign.omege.cc/2022/05/08/30a61726dee28e5617a66801e2af0c14.png)



4. 设置退回源

退回源就是设置源站ip的地方，点击DNS模块，随意解析一个主机记录，A记录至你的源站IP，再回到SAAS，将退回源设置成你所解析的域名就行了。

[scode type="yellow"]解析一定要打开黄色小云朵[/scode]



5. 绑定二级域名

点击SAAS页面中的添加自定义主机名，填入所要接入的站点域名。

[scode type="red"]一定要写入要接入的站点域名，不要放入顶级域名[/scode]



6. 验证域名所有权

这里去域名服务商那里解析2条TXT记录即可。

[scode type="yellow"]是要去需要cname接入域名的DNS[/scode]

[scode type="yellow"]只需要解析顶级域名前面那部分即可[/scode]

![3ed80342e23134682c5c675fdc101c58.png](https://sign.omege.cc/2022/05/08/3ed80342e23134682c5c675fdc101c58.png)

7. 域名解析

验证成功后，只需要去域名DNS解析处，在对应域名解析退回源.cdn.cloudflare.net。



## 总结

SAAS虽然好，但是也是免费条数限制的，并接入方式相比之前也麻烦了许多，但是好在比较稳定。