---
layout: post
title:  Ubuntu使用技巧（三）, Mac OS X, 阴影面积, 辛普森悖论
category: linux 
---

# Ubuntu 18.04使用手记

又是两年过去了，这次是Ubuntu 18.04（2018.4.26发布）。

这次的变化还是有点大，Ubuntu舍弃了自己开发的Unity，转回Gnome，连带着好多软件的界面都出现了一定的调整。这个适应过程，要长于之前的几次升级。

>前些年由于Unity界面乏善可陈，Ubuntu的版本升级被吐槽为换壁纸。这次算是换主题吧。

由于这个改变是2017.4做出的，有了1年的过渡期，因此拿到手的Ubuntu 18.04的成品度还是蛮高的。

输入法比原来好，但有些软件存在兼容问题。

内核：4.15

LibreOffice：6.0

Emacs：25.2

# 桌面主题

用腻了系统自带的桌面主题之后，我打算换个新鲜一些的桌面主题，比如Mac OS X风格的。

1.安装主题修改工具

`sudo apt-get install unity-tweak-tool`

2.安装Mac OS X主题

{% highlight bash %}
sudo add-apt-repository ppa:noobslab/themes
sudo apt-get update
sudo apt-get install mac-ithemes-v3 mac-icons-v3
{% endhighlight %}

3.Cairo Dock

做完上面两步之后，基本的Mac OS X风格已经有了，但Mac最经典的Dock启动器还没有。这里介绍一下Cairo Dock。

安装方法：

`sudo apt-get install cairo-dock`

Cairo Dock不仅具有类似Mac OS X的风格，还有其他的风格可供选择下载。比如我使用的是Chrome风格。

4.其他主题

http://www.ubuntuthemes.org/

这个网站收集了很多桌面主题，但是需要注册，因为有些主题是收费的。

# 发行版乱战

Linux以发行版众多闻名于世。最近发现了以下网站，或可对各个发行版进行一个简单的比较。

http://distrowatch.com/

下面对几个主要的参数，进行一下点评：

## Office

主要是3个流派：

1.StarOffice->OpenOffice.org->LibreOffice。最初由Sun主导，后来改为Google主导。

2.KOffice->Calligra Office。KDE项目的成果。

3.GOffice。Gnome项目的成果，和前两个相比，GOffice的组件比较独立，没有什么协同能力。

# 便签软件

主要有两类便签软件：

1.支持超链接的便签。典型的有Gnote和Tomboy，这两个软件都有内容检索的功能。

2.桌面随意贴。典型的有Indicator Stickynotes和Knotes。后者有内容检索的功能，而前者没有。

# ASCII表情

╮(╯_╰)╭

(^ω^)

# 常用英语缩写

FYI：for your information

IFF：if and only if

eta：estimated time of arrival

w/o：without

N.B.:nota bene 注意,留心

# Mac OS X

最近对iOS开发产生了兴趣，于是准备在PC上搭建一个iOS的开发环境。

首先，我搜了一下在Linux上搭建相关环境的方法，搜到了一些结果。但历史比较老，基本都是3、4年前的东西，就算搭好，也不见得有什么用。

于是，目标改为在PC上使用Virtual Box搭建Mac OS X虚拟机。目标版本为Mac OS X 10.10。

1.下载镜像文件。

镜像文件主要有dmg和iso两种。前者必须在Mac OS X中才能执行，而后者和其他OS镜像差别不大。

2.boot

原版镜像由于Apple的硬件检测机制，并不能在PC上运行。这时就需要破解，这一步一般是在boot中做的。

可用的boot工具，早期有empireEFI、HackBoot。较新的有chameleon、Niresh。

# 阴影面积

![](/images/img3/p0.png)

题如上图，已知正方形边长为10，求阴影面积。

解：

旋转图形建立坐标系如下图：

![](/images/img3/p1.png)

阴影部分上下曲边公式如下：

$$x^2+y^2=5^2$$

$$x^2+(y+5\sqrt{2})^2=10^2$$

求解交点坐标：

$$(y+5\sqrt{2})^2-y^2=75$$

$$10\sqrt{2}y+50=75$$

$$y=\frac{5\sqrt{2}}{4}$$

$$x=\sqrt{\frac{175}{8}}$$

用积分法求解阴影面积：

$$\begin{align}
\frac{S}{4} & =\int_0^{\sqrt{\frac{175}{8}}}\sqrt{(5^2-x^2)}-(\sqrt{(10^2-x^2)}-5\sqrt{2})\mathrm{d}x \\
& = \int_0^{\sqrt{\frac{175}{8}}}\sqrt{(5^2-x^2)}\mathrm{d}x - \int_0^{\sqrt{\frac{175}{8}}}\sqrt{(10^2-x^2)}\mathrm{d}x + 5\sqrt{2} \cdot \sqrt{\frac{175}{8}} 
\end{align}$$

查常用积分表，可得：

$$\int \sqrt{a^2 - x^2}\mathrm{d}{x} = \frac12 \left(x\sqrt{a^2 - x^2} + a^2\arcsin\frac xa\right) + C$$

$$\begin{align}
\frac{S}{4} & =\left[\frac{25}{16}\sqrt{7} + \frac{25}{2}\arcsin(\frac{\sqrt{\frac{7}{2}}}{2})\right] - \left[\frac{125}{16}\sqrt{7} + 50\arcsin(\frac{\sqrt{\frac{7}{2}}}{4})\right] + \frac{25}{2}\sqrt{7} \\
& = \frac{25}{4}\sqrt{7} + \frac{25}{2}\arcsin(\frac{\sqrt{\frac{7}{2}}}{2}) - 50\arcsin(\frac{\sqrt{\frac{7}{2}}}{4})
\end{align}$$

$$S=25\sqrt{7} + 50\arcsin(\frac{\sqrt{\frac{7}{2}}}{2}) - 200\arcsin(\frac{\sqrt{\frac{7}{2}}}{4})\approx 29.27625$$

参考：

https://www.zhihu.com/question/60697114

网传无锡小升初题，求阴影面积

http://wuli.wiki//online/ITable.html

积分表

http://wuli.wiki//online/

小时物理百科

# 辛普森悖论

![](/images/img2/Simpson.png)

如果分专业来看，你就会发现：在各个专业女生的录取率其实都是更高的。之所以会产生“总体录取率女生偏低”这一结果，是因为女生大部分都报考了那些本身就难以录取的学院，而男生则大部分报考了那些录取率本身就偏高的学院。

参考：

https://mp.weixin.qq.com/s/5jZ2dzLInLtUw7rWZF4mtg

张忠元：渣男受女生欢迎？当心统计陷阱

https://mp.weixin.qq.com/s/o1a2YlYritcOrsLN2YuLmA

神奇的霍特林法则：为什么汉堡王总是开在麦当劳旁边？

https://mp.weixin.qq.com/s/eq4MllJta5NmaLARPpvang

公交车总迟到？你大概掉进了“等待时间悖论”

https://zhuanlan.zhihu.com/p/43934918

诡异的布雷斯悖论：为什么越是修新路，城市反而更堵了！

https://mp.weixin.qq.com/s/-0VMucGBq4Trb_9FnsW6KQ

10大反直觉的数学结论

https://mp.weixin.qq.com/s/FqY19sTQd7GPdGSsB5L9eQ

数学大反例合集

https://mp.weixin.qq.com/s/EICefFM3dfv5A6V9kVqGWw

吸烟致癌的迷思是如何破除的

https://mp.weixin.qq.com/s/NlJ4-b5SjIjPGgvLUuSxFw

孩子，有时候并不是生活欺骗了你，而是你可能还不懂概率统计……

# Linux参考资源+

https://mp.weixin.qq.com/s/snQ3T86usv4rXz0MMQvFfQ

如何回答性能优化的问题，才能打动阿里面试官？

https://www.cnblogs.com/zhouyu629/p/3734494.html

一次心惊肉跳的服务器误删文件的恢复过程

https://mp.weixin.qq.com/s/A8TnhOFLQOhEqphE760yvw

15个相见恨晚的Linux神器，你可能一个都没见过

https://mp.weixin.qq.com/s/oKtu3AA9D3y--xMDQ8EARw

携程一次Dubbo连接超时问题的排查

https://mp.weixin.qq.com/s/4o_cSzWeJdLJMObJBhaZlw

计算机系统中的内存

https://mp.weixin.qq.com/s/OWGi1htNugOv81ZFPinRGw

汇编实现的memcpy和memset

https://www.jianshu.com/p/fad3339e3448

浅析Linux中的零拷贝技术
