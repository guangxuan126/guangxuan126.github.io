---
title: 微信小程序-QR二维码
date: 2018-02-24 20:38:56
et: wxapp-qrcode
tags:
  - public
  - tutorials
---

>2017年1月9日凌晨，小程序正式上线！2017年9月27日上午10点「QR二维码」正式上线。

![图自：腾讯网](https://images.gxuann.cn/archives/wxapp-qrcode-banner.png)<br>
### 概述
暑假的时候我就寻思着可以研究研究这小程序，明确需求之后，觉得可以做一个二维码生成器，原因嘛，比较简单在github上找到了一个可以生成二维码的js，直接调用就行；一直拖到开学才开工，我记得当时9月份还在备考二级，然后没事的时候研究研究这个小程序，差不多2周，初版就成型了，然后急急忙忙地就向微信提交了代码审核，当时我还一直在想会不会因为功能太单一了当做demo就给我退回来了，结果过了1天的审核期，收到了过审通知，立马上线了第一个版本。<br>
这个版本的问题也超级多，最大的问题就是生成的二维码保存之后是空白的（后来发现了这个问题出在哪里了，原作者的js文件没有上色，导致绘制出一个透明的二维码，所以保存之后是空白的。）等到了十一假期的时候修正了这个错误，还添加了保存按钮，当时自豪地把这个版本称为2.0新时代。<br>
一个简单的UI一个简单的JS库支撑着这个版本度过了3个月，期间我还加入了反馈功能，这样就可以接收到用户在使用过程中遇到的一些问题或者一些反馈。在这三个月的时间里，这个小程序积累了1400+个用户，日平均活跃量20上下，我个人对这个数据是比较满意的。<br>
在这个寒假了我重写了这个小程序，使用了MinUI和WeUI这两种样式库，在这过程中通过使用框架也了解了什么是组件化开发，在设计完UI之后，我觉得之前使用JS文件生成二维码最大的缺点就是不支持emoji表情，我大概看了下原作者的JS文件，为了支持中文将字符进行了转码，这样输入emoji之后也同样会被转码，生成二维码之后就会乱码；为了解决这个问题，我找到了PHP中有个QRCODE库，将它架在服务器上，生成二维码的时候使用`wx.request(OBJECT)`这个API向服务器发送`GET`请求， 这样就通过参数生成二维码，**这个操作会在浏览器内完成，不会生成图片，也不会被保存到服务器上**；除了以上两点，我还调用了`wx.scanCode(OBJECT)`这个api，可以用来识别二维码，这样这个小程序的功能就全了。

#### QRCode 3.0 新功能
- 新的UI:结合使用了Minui & WeUI
- 支持FontAwesome字体
- 添加了扫描二维码的功能

---

### 关于&说明
1.PHP Qr Code：[官网 phpqrcode.sourceforge.net](http://phpqrcode.sourceforge.net/)
2.MinUI：[Github项目地址](https://github.com/meili/minui)
3.WeUI： [Github项目地址](https://github.com/Tencent/weui-wxss/)
4.微信官方小程序开发手册： [官网地址](https://mp.weixin.qq.com/debug/wxadoc/dev/)

#### 关于PHPQrCode
```PHP
$value=$_GET['detail'];  
$errorCorrectionLevel = "H";
$matrixPointSize = "10";
QRcode::png($value, false, $errorCorrectionLevel, $matrixPointSize);  
```
以上四句是部分代码，用于生成二维码的`QRcode::png`方法一共有6个参数：
1.`$value`：用于转换的数据。
2.`$outfile`：默认为`false`，不生成文件，只将二维码图片返回，否则需要给出存放生成二维码图片的路径.
3.`$errorCorrectionLevel`：控制二维码容错率，不同的参数表示二维码可被覆盖的区域百分比.
4.`$matrixPointSize`：控制生成图片的大小.
5.`$margin`：控制生成二维码的空白区域大小.
6.`$saveandprint`：保存二维码图片并显示出来，`$outfile`必须传递图片路径.

#### 使用
ok，说了这么多感谢大家的支持，打开微信扫描下面任意一个二维码就可以直接访问「QR二维码」

---
![](https://images.gxuann.cn/archives/gh_db3301df811e_258.jpg)
![](https://images.gxuann.cn/archives/gh_db3301df811e_258_normal.jpg)

---
