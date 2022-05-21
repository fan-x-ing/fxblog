title: ABout WebP
categories: 闲谈
tags: [GOOGLE,WebP,图片,速度优化]
date: 2022-01-07 12:24:00
---
 说到**WebP**大家可能都会疑惑，这究竟是什么？我们所熟悉的图片格式一般都为`png`，`GIF`，`JPG`等等。这突然崩出来一个从来没见过的格式，还叫什么**WebP**，这到底是什么？

# 介绍

  **WebP**是一种同时提供了有损压缩与无损压缩（可逆压缩）的图片文件格式，派生自影像编码格式VP8，被认为是WebM多媒体格式的姊妹项目，是由Google在购买On2 Technologies后发展出来，以BSD授权条款发布。

  WebP最初在2010年发布，目标是减少文件大小，但达到和JPEG格式相同的图片质量，希望能够减少图片档在网络上的发送时间。2011年11月8日，Google开始让WebP支持无损压缩和透明色（α通道）的功能，而在2012年8月16日的参考实做libwebp 0.2.0中正式支持。根据Google较早的测试，WebP的无损压缩比网络上找到的PNG档少了45%的文件大小，即使这些PNG档在使用pngcrush和PNGOUT处理过，WebP还是可以减少28%的文件大小。

  WebP支持的像素最大数量是16383x16383。有损压缩的WebP仅支持8-bit的YUV 4:2:0格式。而无损压缩（可逆压缩）的WebP支持VP8L编码与8-bit之ARGB色彩空间。又无论是有损或无损压缩皆支持Alpha透明通道、ICC色彩配置、XMP诠释数据。

  WebP有静态与动态两种模式。动态WebP（Animated WebP）支持有损与无损压缩、ICC色彩配置、XMP诠释数据、Alpha透明通道。

> 以上摘取自百度百科

  看完上边专业的介绍后大家可能已经知道WebP大概是个什么东西了，WebP呢，就是一个压缩率挺高的一个压缩格式罢了。

## 兼容性

  当前网页浏览器当中，**Google Chrome**和**Opera**原生支持静态与动态的WebP格式，而Google Chrome自12版开始支持WebP的渐进式解码功能。

  此外所有可以原生播放WebM影像的浏览器，也可以透过javascript来显示WebP影像。又Pale Moon 26+浏览器仅支持静态的WebP图像。Firefox浏览器亦在65.0版本支持WebP图像。网页浏览器GNOME Web和KDE图片浏览器Gwenview也支持WebP。

  图像软件当中，**Picasa**（从3.9版本起）、**PhotoLine**、**Pixelmator**、**ImageMagick**、**XnView**、**IrfanView**、**GDAL**、**Aseprite**和**GIMP**（2.10起）皆原生支持WebP格式。

  苹果在**macOS Sierra**及**iOS 10**的早期beta版本中加入了WebP支持。而在2016年9月7日发布的iOS 10和macOS Sierra GM种子版本中却移除了WebP的支持。
![rOKD.webp](https://q3.a1pic.cn/2022/01/07/rOKD.webp)


## 效果

> <center>在质量相同的情况下，WebP格式图像的体积要比JPEG格式图像小40%</center>
>
> <center>by Google</center>



## 优点

  WebP和别的格式比起来，就是在于它拥有良好的压缩算法，可以提供高速的加载速度，如今圆梦驿站已经几乎把所有图片转换为WebP格式了，当然还有一些漏网之鱼（我太懒了

  除了这些，同时它还具有了稳定性和统一性

![对比 PNG 原图、PNG 无损压缩、PNG 转 WebP（无损）、PNG 转 WebP（有损）的压缩效果（转自ahdark)](https://q2.a1pic.cn/2022/01/07/rYXO.webp)

​  通过上图，我们可以得出结论：

- WebP有损的压缩率达到百分之78.9，超出了PNG等众多格式
- 转换后的WebP格式，支持 Alpha 透明和 24-bit 颜色数，不存在 PNG8 色彩不够丰富和在浏览器中可能会出现毛边的问题
- WebP在压缩后画质变化不大（肉眼几乎无法分辨

  实测我的网站确实快了不少，从一个网页将近10m到一个网页只有2m不到，现在圆梦驿站已经几乎秒开了，后续的话我会尝试写一篇圆梦驿站的框架，来给大家详细的讲讲

参考：[Ahdark的博客](https://ahdark.com/technology/604.shtml)