+++
title = "Debian 12 安装小记"
date = 2024-11-06T00:00:00+08:00
lastmod = 2024-11-12T22:41:26+08:00
tags = ["Linux", "GFW"]
categories = ["Linux"]
draft = false
toc = true
+++

本文采取的安装方式为最小网络安装（netinst CD image），使用的安装镜像为 `debian-12.7.0-amd64-netinst.iso` 。


## GRUB引导选择界面 {#grub引导选择界面}

不要使用第一个安装方式，没法调整细节

{{< figure src="/ox-hugo/_20241106_100713screenshot.png" >}}

进入高级选项

{{< figure src="/ox-hugo/_20241106_100729screenshot.png" >}}

使用专家模式图形化安装

{{< figure src="/ox-hugo/_20241106_100746screenshot.png" >}}


## 专家模式安装流程 {#专家模式安装流程}

按提示操作即可

> 顺带一提，Debian安装程序的图形界面显示在tty5，切换到tty4就能看到日志。

{{< figure src="/ox-hugo/_20241106_100858screenshot.png" >}}

在运行了 `load installer compones from installation media` 之后就有下面的选项了，继续下一步

> 注意在分配好磁盘之后，整个系统的挂载点为 `/target` ，如果要 `chroot` 的话就要使用这个位置 （Arch Linux 一般为 `/mnt` ）

{{< figure src="/ox-hugo/_20241106_101025screenshot.png" >}}

选择镜像源，最好选一个速度最快的镜像来加速下载

> 网上有些说法说不要设置这个，以防止后面的安装卡在安全更新那里，但是实测设不设置都没影响，不设置反而影响其他包的下载速度。

{{< figure src="/ox-hugo/_20241106_101107screenshot.png" >}}

从这里开始就要注意了，如果碰到安装很慢的问题，就参考[下载缓慢](#下载缓慢)

{{< figure src="/ox-hugo/_20241106_101450screenshot.png" >}}

这可能是最难解决的一个问题，解决了这个难点之后后续的安装流程就很简单了，不再赘诉。


## 下载缓慢 {#下载缓慢}

**表现：** 一直卡在 `retrieving file` ，在tty4的日志上看到正在拉取security源的数据

**解决方法：** 可以采取 [完整CD(full CD sets)](https://www.debian.org/releases/stable/debian-installer/) 离线安装，也可以

**不要勾选安全更新，之后自己设置**

{{< figure src="/ox-hugo/_20241106_101616screenshot.png" >}}

**原因：**

> 1.  国内不同地方/不同运营商对Debian官方源的支持都不一样，有的地方很快，有的地方慢得完全没法用
> 2.  不管用什么方法都没法绕过安全更新，安装程序总是会用官方security源，[这种方法因而不能奏效](https://www.cnblogs.com/microestc/p/16172451.html)（无法影响已经启动的拉取进程）

自动更新，默认不开启

{{< figure src="/ox-hugo/_20241106_101700screenshot.png" >}}


## 总结 {#总结}

1.  Debian安装程序还是不错的，基本傻瓜式操作
2.  如果使用一开始的快速安装方式，十有八九会因为网络问题而放弃
3.  由于GFW的存在，可能会碰到各种奇怪的问题， **一定要看日志** ，弄清楚问题在哪里


## 参考资料 {#参考资料}

1.  <https://forums.debiancn.org/t/topic/2123/18>
2.  <https://emacs-china.org/t/debian-12/27421/2?u=1chen>
