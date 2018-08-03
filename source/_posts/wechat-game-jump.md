---
title: 微信小游戏「跳一跳」 高分神器！
date: 2018-01-06 10:14:18
et: wechat_game_jump
tags:
  - tutorials
---
  &emsp;&emsp;2017年12月28日，微信正式公布小游戏产品，其中第一批开放了15款H5小游戏，“跳一跳”即是其中之一。游戏玩法很简单，用户只需长按住屏幕中黑色的抽象小人，进行蓄力，蓄力越久就能跳得越远。只要小黑人不落到方格外，就能得分。一旦跳出方格外，游戏就算结束。这款游戏即点即玩，无需下载安装，玩家可以在微信内和好友一起玩。
  &emsp;&emsp;“今天你跳了吗？”这几天，微信朋友圈里“跳一跳”小游戏异常火热，其自带的得分排名功能，更是让很多人彻夜刷分。

但这一阵子网上也出现了很多的攻略：
![](https://images.gxuann.cn/archives/wechat-game-jump-1.png)
![](https://images.gxuann.cn/archives/wechat-game-jump-2.jpg)

---

  &emsp;&emsp;但既然是高分攻略，就肯定不能使用传统攻略的。
  &emsp;&emsp;这周做课设的时候，逛Github时，发现一位作者写了一段关于「用Python来玩跳一跳」的代码，阅读之后，我按照要求把这段代码跑起来了测试了一下，发现果然是高分神器！

---

下面来说说这个脚本：
![](https://images.gxuann.cn/archives/wechat-game-jump-3.png)
#### 原理
1.将手机界面停留在「跳一跳」界面
2.用 ADB 工具获取当前手机截图，并用 ADB 将截图 pull 上来
```bash
adb shell screencap -p /sdcard/autojump.png
adb pull /sdcard/autojump.png
```
3.计算按压时间
4.用 ADB 工具点击屏幕蓄力一跳
```bash
adb shell input swipe x y x y time(ms)
```

#### 操作步骤
##### 简要步骤：
首先搭建运行环境`ADB`和`Python`,然后将ADB添加到环境变量当中，最后就可以直接运行`.py`的脚本了。

##### 下面是详细步骤：
![](https://images.gxuann.cn/archives/wechat-game-jump-4.png)

#### 下载
大家可以去作者的repo页面查看更详细的内容以及下载这个脚本
>[Github:wangshub/wechat_jump_game](https://github.com/wangshub/wechat_jump_game)
>脚本由@wangshub提供

<br>
&&
end
