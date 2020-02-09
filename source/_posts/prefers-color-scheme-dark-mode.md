---
title: 给网站加上自适应的深色模式
date: 2020-02-01 22:13:25
tags:
    - public
    - tutorials
---

![dark_mode](https://cdn.gxuann.cn/mweb/2020/02/01/dark_mode.png)

之前在浏览 sspai 的网站时，发现了一个细节，那就是他们的网站会随着我手机或者是电脑的主题模式来变换配色，也就是说当我的设备主题是深色模式时，网站会自动变成深色模式，如果我的设备主题是浅色是，网站也会相应的变成浅色。
在我看来网站的「深色模式」对于提升用户体验来说是至关重要的，因为大多数的用户可能会打开手机内或者电脑内的自动外观模式，就我自己来说，我一般是设定一个区间，晚 11 点至早 7 点，这样在夜间整个手机的配色都会暗下来，在夜间也是保护视力的一种方式呢。
自 Apple 在 2019 年发布的 iOS13 中配有「深色模式」之后，现在越来越多的 APP 和网站都会适配上「深色模式」，都 0202 年了，如果到现在还是没有「深色模式」的 APP 或者网站，在我看来就会显得格格不入呢（指绿色聊天应用）

## 初次尝试
那么对于我这个小破站来说，最早是在 2019 年 11 月首次适配了「深色模式」，那时候我想到的方法是利用 js 来判定然后重新加载 css。

首先是在前端页面创建了一个用于切换浅色/深色模式的 icon，然后在 js 里创建一个监听这个 icon 点击事件的函数，点击后，如果本地缓存变量 `dark_mode` 的值为 `light` 则从远端 CDN 服务器中加载一个「深色模式」的 CSS 来覆盖现有的样式并将变量缓存的值修改为 `dark`；反之，如果则会移除这个「深色模式」的样式。
```
$("#dark-btn,#dark-mobile").click(function() {
    if (localStorage.getItem("dark_mode") === 'dark'){
      removeCss('https://cdn.gxuann.cn/blog-css-dark.css');
      $("#dark-btn").attr("class","fa fa-moon");
      localStorage.setItem("dark_mode", 'light');
    } else {
      loadCss('https://cdn.gxuann.cn/blog-css-dark.css');
      $("#dark-btn").attr("class","fa fa-sun");
      localStorage.setItem("dark_mode", 'dark');
    }
  })
```
为了保证在页面加载的时候存在`dark_mode` 这个变量，我在页面的`head`中加入了一段 js 用于写入这个变量。
```
<script>
    "dark" === localStorage.getItem("dark_mode") ? document.write('<link rel="stylesheet" href="https://cdn.gxuann.cn/blog-css-dark.css"></span>') : ""
</script>
```

这么做我觉得还存在一些问题，优点是：用户在访问到页面的时候可以自主选择切换浅色/深色模式；缺点是：首次从远端 CDN 服务器加载 CSS 样式文件的时候会视网络状况有延迟，毕竟在页面渲染好之后重新加载一次 CSS 的用户体验并不是很好。

## 通过 CSS 的媒体查询来实现
在 CSS 的规范中，存在一个[五级媒体查询](https://drafts.csswg.org/mediaqueries-5/#mf-user-preferences) 规范。
```
@media (prefers-color-scheme: light | dark) 
{ ... }
```
通过这个查询可以检测出用户的系统主题是浅色或者深色。

> 但目前，这个媒体查询在部分浏览器中不被支持：（附浏览器兼容性表）

![](https://cdn.gxuann.cn/mweb/2020/02/02/15806584382257.jpg)

- 部分代码
1. **HTML**
```
<body>
  <header id="header">...</header>
  <section id="about">...</section>
  <section id="writing">...</section>
  <footer id="footer">...</footer>
</body>
```
2. **CSS**
```
body {
  ...
  margin: 0;
  height: 100%;
  color: #22272a;
  background-color: #fafafa;
  ...
}

@media (prefers-color-scheme: dark ) {
  body {
    ...
    background-color: #1d1f21;
    color: #c9cacc;
    ...
  }
}
```

通过在 CSS 样式文件中添加 `@media (prefers-color-scheme)` 媒体查询，并在里面写入新的颜色样式，就可以实现浏览器根据用户设备的系统样式来自适应选择浅色/深色模式了。


## 相关资料
- [prefers-color-scheme-MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)
- [Redesigning your product and website for dark mode](https://stuffandnonsense.co.uk/blog/redesigning-your-product-and-website-for-dark-mode)


&&
end





 

