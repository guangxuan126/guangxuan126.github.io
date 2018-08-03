---
title: 重新安装Windows的简易教程
date: 2017-08-20 19:00:54
tags:
    - tutorials

---

### 环境准备

&ensp;&ensp;<i class="fa fa-check-square-o"></i>系统镜像
&ensp;&ensp;<i class="fa fa-check-square-o"></i>U盘一个（>8GB）
&ensp;&ensp;<i class="fa fa-check-square-o"></i>一台计算机


### 开始之前
请确认
&ensp;&ensp;<i class="fa fa-dot-circle-o" aria-hidden="true"></i>BIOS启动模式为`UEFI`
&ensp;&ensp;<i class="fa fa-dot-circle-o" aria-hidden="true"></i>硬盘为`GPT分区`

 <i class="fa fa-exclamation-circle"></i>符合上面确认规则的用户或之前计算机有安装、激活过Windows10的用户可以直接跳过这一步.<br>
`BIOS`请参阅厂商说明书调整至`UEFI`
`GPT分区`转换：<i class="fa fa-exclamation-triangle" aria-hidden="true"></i>下面的操作会清除硬盘内所有信息，请提前做好备份
先进入Windows安装环境，然后在任何步骤开始之前按`Shift+F10`进入`命令提示符`然后输入以下命令(命令需要逐条运行)
<i class="fa fa-question-circle" aria-hidden="true"></i>`disk X 这里的X指的是目标磁盘`
```CMD
diskpart
list disk
sel disk X
clean
convert gpt
```

### 正式开始
#### 制作安装介质
**方法1**：使用`UltraISO`或其他同类软件可以轻松地将系统镜像写入U盘，具体操作可简述：通过软件打开镜像后，点击`启动>写入硬盘映像`硬盘驱动器选择U盘，然后点击`格式化`，最后点击`写入`，等待写入完成之后即可关闭此软件。
**方法2(不推荐)**：这是个简单粗暴的方法，将U盘手动格式化成`FAT32`；然后打开镜像，将里面所有内容复制到U盘即可。不推荐的原因是这个操作有可能会发生未知错误。

#### 安装windows
当一切准备就绪后，插入U盘，打开计算机，在开机引导之前进入一次性引导菜单（TIPS:由于各品牌电脑进入方式不同，具体按键建议自行Google，这里以DELL的电脑为例）出现DELL logo时，按`F12`进入一次性引导菜单，选择刚才制作的U盘，即可进入Windows安装环境。
紧接着，可以理解成正常安装软件那样，下一步，根据提示选择需要安装的版本、同意许可之后会让用户选择安装方式`升级`和`自定义`,这里需要选择`自定义`然后根据需要分配磁盘空间，选择需要安装的目标分区，点击下一步即可。
<i class="fa fa-refresh fa-spin fa-fw"></i><span class="sr-only">Loading...</span>等待安装完成...
点击重启即可完成安装。

#### 完善阶段
重启之后，计算机就可以正常进入系统并且含有基本驱动程序，这时候需要去安装必要驱动、更新系统补丁、选择性安装功能补丁和驱动。
强烈不建议使用第三方驱动安装程序，请自行去电脑品牌官网下载符合当前配置的驱动程序。
这里附上一些常见品牌的技术支持页面，可在这里查找到相关驱动程序：

|      |      |
| :------------- | :------------- |
| [Dell支持](http://www.dell.com/support/home/cn/zh/cndhs1?~ck=mn) | [Lenovo支持](http://support.lenovo.com.cn/lenovo/wsi/index.html) |
| [Acer支持](https://www.acer.com.cn/ac/zh/CN/content/support/) | [MSI支持](https://cn.msi.com/support/) |
| [ASUS支持](https://www.asus.com.cn/support/) | [HP支持](https://support.hp.com/cn-zh) |

---

### More
#### 系统镜像可以在这里下载：[MSDN-Manual](http://tc.gxuann.cn/msdn/index.html)
#### 附上一些图以说明其中步骤的注意点：
>如果之前未安装和激活过Windows10，则会出现下面这个界面，点击`我没有产品密钥`以继续安装。

![](https://images.gxuann.cn/installwindows_i1.png)

---

>在分区完成后会发现多出来2-3个容量在500MB以内的小分区，这是系统自动分出的ESP引导分区和Recovery恢复分区，注意这里需要正确选择安装Windows的分区。

![](https://images.gxuann.cn/installwindows_i2.png)

---

>关于安装介质的制作，`写入硬盘镜像`窗口中，红色框内可直接默认，不用修改；`格式化`窗口内也是默认就好。

![](https://images.gxuann.cn/installwindows_i4.png)

---

#### 最后一点
**不推荐 不推荐 不推荐** 大家使用第三方驱动安装程序，请尽量去厂商官网下载符合自己计算机的驱动程序！

<br>
&&
end
