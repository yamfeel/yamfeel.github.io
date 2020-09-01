---
title: Servirce Workers 网站加速和离线缓存
date: 2020-08-03 11:36:35
tags: Blog 日志
---

s最近sw.js 这个东西，啊这2016年的，时刻提醒我是个废物。Service Workers 是用来缓存网站静态与动态资源，截取用户的所有网络请求，根据缓存配置来决定是从缓存还是网络获取相应资源，这样就可以极大提升网站加载速度啦。
优点：可定制、无需服务端、效果显著。
缺点：只支持HTTPS，因为截取请求必须要一个安全的环境。

- 首先在主页添加注册代码

```javascript
<script>
if ('serviceWorker' in navigator) {
 navigator.serviceWorker.register('/sw.js');
}
</script>
```

将https://alphayang.github.io/sw.js保存到你的网站根目录下

- 修改不缓存的域名及离线状态页面

在你的sw.js中修改

```javascript
const ignoreFetch = [
  /https?:\/\/cdn.bootcss.com\//,
  /https?:\/\/static.duoshuo.com\//,
  /https?:\/\/www.google-analytics.com\//,
  /https?:\/\/dn-lbstatics.qbox.me\//,
];
```

打开`Chrome Dev Tools->Source`，看看自己的blog都引用了哪些第三方资源，逐个加到忽略列表里。

在根目录下添加offline.html、offline.svg，在没有网络且缓存中也没有时使用。