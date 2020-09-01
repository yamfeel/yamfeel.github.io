---
title: Hexo 提交百度引擎收录
date: 2020-08-03 11:58:45
tags: Blog 日志
typora-root-url: ..
---

- ## 查看网站是否被收录
首先我们可以输入 site:域名 来查看域名是否被搜索引擎收录，如下图所示，表示没有收录：

![image-20200803120344302](/images/blog-log-2/image-20200803120344302.png)

- ## 百度资源平台添加网站

访问[百度搜索资源平台](https://ziyuan.baidu.com/)，依次选择 `用户中心` - `站点管理`，添加网站时尽量添加https，会省去不少麻烦。添加方式推荐 CNAME 验证。

百度提供了自动提交和手动提交两种方式，其中自动提交又分为主动推送、自动推送和 sitemap 三种方式，以下是官方给出的解释：

- 主动推送：最为快速的提交方式，推荐您将站点当天新产出链接立即通过此方式推送给百度，以保证新链接可以及时被百度收录
- 自动推送：是轻量级链接提交组件，将自动推送的 JS 代码放置在站点每一个页面源代码中，当页面被访问时，页面链接会自动推送给百度，有利于新页面更快被百度发现

- sitemap：您可以定期将网站链接放到sitemap中，然后将sitemap提交给百度。百度会周期性的抓取检查您提交的sitemap，对其中的链接进行处理，但收录速度慢于主动推送

- 手动提交：如果您不想通过程序提交，那么可以采用此种方式，手动将链接提交给百度

<center>
    四种提交方式对比
</center>

| 方式                     | 主动推送 | 自动推送 | Sitemap | 手动提交 |
| ------------------------ | -------- | -------- | ------- | -------- |
| 速度                     | 最快     | ——       | ——      | ——       |
| 开发成本                 | 高       | 低       | 中      | 不需开发 |
| 可提交量                 | 低       | 高       | 高      | 低       |
| 是否建议提交历史链接     | 否       | 是       | 是      | 是       |
| 和其他提交方式是否有冲突 | 无       | 无       | 无      | 无       |

我用的是 **主动推送** 和 `sitemap` 。

### 主动推送

  在博客根目录安装插件 `npm install hexo-baidu-url-submit --save`，然后在根目录 `_config.yml` 文件里写入以下配置：

```
baidu_url_submit:
  count: 1               # 提交最新的多少个链接
  host: blog.yamfeel.cn    # 在百度站长平台中添加的域名
  token: your_token      # 秘钥
  path: baidu_urls.txt   # 文本文档的地址， 新链接会保存在此文本文档里
```

其中的 `token` 可以在 **链接提交** - **自动提交** - **主动推送** 下面看到，接口调用地址最后面 `token=xxxxx` 即为你的 `token`

![image-20200803121712413](/images/blog-log-2/image-20200803121712413.png)

同样是在根目录的 `_config.yml` 文件，大约第 17 行处，url 要改为在百度站长平台添加的域名，也就是你网站的首页地址：

```
# URL
url: https://blog.yamfeel.cn
root: /
permalink: :year/:month/:day/:title/
```

最后，加入新的 deployer：

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
- type: git
  repository:
    github: git@github.com:XXXXX.github.io.git  # 这是原来的 github 配置
    coding: git@git.dev.tencent.com:XXXXX.git   # 这是原来的 coding 配置
  branch: master
- type: baidu_url_submitter                         # 这是新加的主动推送
```

最后执行 `hexo g -d` 部署一遍即可实现主动推送，推送成功的标志是：在执行部署命令最后会显示类似如下代码：

```
{"remain":4999953,"success":47}
INFO  Deploy done: baidu_url_submitter
```

这表示有 47 个页面已经主动推送成功，remain 的意思是当天剩余的可推送 url 条数。

主动推送相关原理介绍：

- 新链接的产生：hexo generate 会产生一个文本文件，里面包含最新的链接
- 新链接的提交：hexo deploy 会从上述文件中读取链接，提交至百度搜索引擎

该插件的 GitHub 地址：https://github.com/huiwang/hexo-baidu-url-submit

### sitemap

首先我们要使用以下命令生成一个网站地图：

```
复制npm install hexo-generator-sitemap --save     
npm install hexo-generator-baidu-sitemap --save
```

这里也注意一下，将根目录的 `_config.yml` 文件，大约第 17 行处，url 改为在百度站长平台添加的域名，也就是你网站的首页地址：

```
复制# URL
url: https://www.itrhx.com
root: /
permalink: :year/:month/:day/:title/
```

然后使用命令 `hexo g -d` 将网站部署上去，然后访问 `你的首页/sitemap.xml` 或者 `你的首页/baidusitemap.xml` 就可以看到网站地图了

比如我的是：https://blog.yamfeel.cn/baidusitemap.xml 或者 https://blog.yamfeel.cnsitemap.xml

其中 `sitemap.xml` 文件是搜索引擎通用的 sitemap 文件，`baidusitemap.xml` 是百度专用的 sitemap 文件

然后来到百度站长平台的 sitemap 提交页面，将你的 sitemap 地址提交即可，如果成功的话状态会显示为正常，初次提交要等几分钟，sitemap.xml 相比 baidusitemap.xml 来说等待时间也会更长，如果以后你博客有新的文章或其他页面，可以点击**手动更新文件**，更新一下新的 sitemap

![img](/images/blog-log-2/07.png)

> 致谢提供方法博主 **TRHX** 
> 博客链接：[https://www.itrhx.com/2019/09/17/A48-submit-search-engine-inclusion/](https://www.itrhx.com/2019/09/17/A48-submit-search-engine-inclusion/)