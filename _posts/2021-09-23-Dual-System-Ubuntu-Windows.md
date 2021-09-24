---
layout: post
title:  "Dell工作站双硬盘安装Win10和Ubuntu双系统"
date:   2021-09-23 14:01:00 +0800
categories: others
---


由于之前的双系统安装主要在笔记本上进行，而且未遇到过双硬盘的情况，因此过程较为简单顺利。本文主要记录在已预先装好Win10系统的双硬盘(SSD+HDD)工作站上安装Ubuntu双系统的过程，对单硬盘的情况也有一定参考价值。

本文主要参考资料：
- Dell Inspiron 5488 双硬盘安装 Win10 Ubuntu 双系统: <https://empvalley.com/2020/08/28/win10-ubuntu-dual-boot/>
- Ubuntu20.04+Win10双系统安装（联想电脑、ssd+hdd双硬盘方案）: <https://blog.csdn.net/szm1234/article/details/113245656?spm=1001.2014.3001.5501>
- windows10安装ubuntu双系统教程（绝对史上最详细）: <https://www.cnblogs.com/masbay/p/10745170.html>
- Create a bootable USB stick on Windows: <https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview>

## 0. 环境描述
### 硬件环境
型号Dell Precesion 5820; 内存32GB; 硬盘256GB固体硬盘+2T机械硬盘
### 软件环境
Windows 10专业版; Ubuntu20.04; USB系统盘制作工具[Rufus](https://rufus.ie/en/); BIOS模式为UEFI

注: 可以通过“win+R”进入“运行”，输入“msinfo32”，回车确定后查看系统信息中的BIOS模式。

## 1. 制作Ubuntu系统盘
[Rufus](https://rufus.ie/en/)官网下载安装文件，同时[Ubuntu](https://ubuntu.com/download/desktop)官网下载镜像文件，Rufus制作系统盘选项如下：
![Rufus](/img/ubuntu_rufus.png)

## 2. 硬盘分区
根据[windows10安装ubuntu双系统教程（绝对史上最详细）](https://www.cnblogs.com/masbay/p/10745170.html)中的介绍，在固态硬盘即“磁盘0”中分出1000MB以用来安装Ubuntu系统的EFI，在2T的机械硬盘中分出约1T用来作为Ubuntu系统挂载`/home`,`/目录`以及做交换空间`\swap`.
![windows_partition](/img/ubuntu_windows_partition2.png)

## 3. 使用U盘进行安装
需要注意的是，在正式安装之前需要先对一些设定进行修改。这一步参考[Dell Inspiron 5488 双硬盘安装 Win10 Ubuntu 双系统](https://empvalley.com/2020/08/28/win10-ubuntu-dual-boot/)，主要包括关闭磁盘加密以及设置BIOS。

完成修改后，便可插入U盘并重启电脑，启动选项选择U盘，便会出现Ubuntu的图标，并提示在进行磁盘检查，之后便进入Ubuntu主页面，选择`Install Ubuntu`
![welcome](/img/ubuntu_welcome.jpg)

后续安装选项中，我选择了`Normal installation`，同时没有选择安装时下载更新。

下一步便是关于分区的安装选项，需要注意的是，自己之前在单硬盘情况下安装时，由于只需要在一块硬盘中给Ubuntu系统分出足够空间即可（不需要考虑在哪个盘安装引导的问题），所以如果在**installation type**这一步时Ubuntu系统能够检测到同时安装了windows系统，那么这里直接选择`Install Ubuntu alongside Windows 10`即可（当然单硬盘也可以选择自定义安装，从而根据自己需求来自定义分区）。而对于双硬盘情况下的安装，由于需要将Ubuntu启动引导与Windows10的启动引导安装到同一个硬盘上，所以必须选择自定义安装`Something else`

### Ubuntu 分区设置
网上的各种教程和经验贴里有各种或详细或简单的Ubuntu分区方法，这里采用的是相对简单的但是感觉比较好用的一种。总的来说只需要4个分区
- EFI引导，逻辑分区，SSD上分出的1000MB
- 交换空间swap area, 逻辑分区，HDD上分出32GB
- /home目录，主分区，HDD上分出400多GB
- /目录，逻辑分区，HDD上分出400多GB
![efi](/img/ubuntu_efi.jpg)
![root](/img/ubuntu_root.jpg)
![home](/img/ubuntu_home_partition.jpg)

**重要:** 分区完成后便是选择安装启动项的位置，或安装启动引导器的设备，这里需要在上面的分区列表中找到刚刚分好的Ubuntu的EFI引导所对应的设备名称，如“/dev/nvme0n1p6”，然后在引导设备的下拉列表中选中对应的选项，最后点击`install now`即可。
![sel_efi](/img/ubuntu_select_efi.jpg)
### 安装
在确认最终的设置信息后，便会开始安装进程
![finish](/img/ubuntu_partition_finish.jpg)
最开始需要先设置时区和用户信息，之后便安心等待即可。安装完成后按照提示重启电脑，便能看到双系统的启动引导了，一般第一行为Ubuntu，第三行为windows10.
