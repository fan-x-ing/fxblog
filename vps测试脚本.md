title:  vps测试脚本
categories: 分享
tags: [linux,vps,测试脚本]
date: 2021-08-21 12:20:00
---
## 前言

我相信很多买vps的人再vps买来之后都会跑一边脚本，来测试vps的性能。我今天给大家推荐一个



## SuperBench.sh

老鬼大佬的SuperBench测试脚本
**特点**

- 改进了显示的模式，基本参数添加了颜色，方面区分与查找
- I/O测试，更改了原来默认的测试的内容，采用小文件，中等文件，大文件，分别测试IO性能，然后取平均值
- 速度测试替换成了 Superspeed 里面的测试，第一个默认节点是，Speedtest
  默认，其他分别测试到中国电信，联通，移动，各三个不同地区的速度

### 使用指令

```
wget -qO- --no-check-certificate https://raw.githubusercontent.com/oooldking/script/master/superbench.sh | bash
```