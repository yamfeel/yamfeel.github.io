---
title: 博客项目-1
date: 2019-03-08 07:31
tags: 杂物间
categories: 杂物间
typora-root-url: ..\..
---

### 目标

+ 开发一个博客系统，具体博客的基本功能
+ 只开放server 端，不关心前端



### 需求

+ 首页，作者主页，博客详情页

    > ## 作者主页
    >
    > #### 博客标题A
    >
    > 张三 2018-12-30
    >
    > #### 博客标题B
    >
    > 张三 2018-12-20

    

+ 登录页

    > #### 用户名 密码 登录
    
    
    
+ 管理中心，新建页，编辑页 

    > ## 管理中心
    >
    > #### 新建博客
    >
    > | 搜索：—————— |           |
    > | ------------ | --------: |
    > | 博客标题A    | 编辑 删除 |
    > | 博客标题B    | 编辑 删除 |
    >
    > ## 编辑博客
    >
    > #### 博客标题A
    >
    > > xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    > >
    > > xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    > >
    > > xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    >
    > `保存`
    
    

### 技术方案 

+ 数据如何存储

  + 博客

    + | id   | title | content | createtime | author |
      | ---- | ----- | ------- | ---------- | ------ |
      | 1    | 标题  | 内容    | 时间戳     | 张三   |
      | 2    | 标题  | 内容    | 时间戳     | 李四   |

  + 用户

    + | id   | username | password | realname |
      | ---- | -------- | -------- | -------- |
      | 1    | zhangsir | MD5      | 张三     |
      | 2    | lisi     | MD5      | 李四     |

    

+ 如何与前端对接，即接口设计

  + 接口设计

    | 描述             | 接口             | 方法 | url参数                       | 备注                           |
    | ---------------- | ---------------- | ---- | ----------------------------- | ------------------------------ |
    | 获取博客列表     | /api/blog/list   | get  | author作者，keyword搜索关键字 | 参数为空的话，则不进行查询过滤 |
    | 获取一篇博客内容 | /api/blog/detail | get  | id                            |                                |
    | 新增一篇博客     | /api/blog/new    | post |                               | post 中有新增的信息            |
    | 更新一篇博客     | /api/blog/update | post | id                            | postData中有更新的内容         |
    | 删除一篇博客     | /api/blog/del    | post | id                            |                                |
    | 登录             | /api/user/login  | post |                               | postData中有用户名和密码       |

  

### 总结

+ 需求一定要明确，需求指导开发
+ 不要纠结于简单的页面样式，并不影响server 端的复杂度



## 开发接口（不使用任何框架）

+ nodejs 处理 http 请求
  + http 请求概述
    + DNS 解析，建立TCP连接（三次握手），发送http请求
    + server 接收 http 请求，处理，并返回
    + 客户端接收到返回数据，处理数据（如渲染页面，执行js）
+ 搭建开发环境
+ 开发接口（暂不连接数据库，暂不考虑登录）



### nodejs 处理 http 请求 （演示）

+ get 请求和 querystring

  + get请求，即客户端要向server 端获取数据，如查询博客列表

  + 通过 querystring 来传递数据，如 a.html?a=100&b=200

  + 浏览器直接访问，就发送get请求

    ```javascript
    const http = require('http');
    const querystring = require('querystring'); //解析结构对象
    const server = http.createServer((req, res) => {
        console.log(req.method) // GET
        const url = req.url //获取请求的完整url
        // req.query添加自定义属性，不是本身自带
        req.query = querystring.parse(url.split('?')[1]) // 解析querystr ing 将这些query字符转化成对象
        res.end(JSON.stringify(req.query)); // 将querystring 返回
    });
    server.listen(8000);
    ```

    `Array.split(param)` 以param分割字符串为数组

+ post 请求 和 postData

  + post 请求，即客户端要服务端传递数据，如新建博客
  + 通过 postData 传递数据

  ```javascript
  const http = require('http')
  const server = http.createServer((req, res) => {
      if (req.method === 'POST') {
          //数据格式 
          console.log('content-type', req.headers['content-type'])
          //接收数据
          let postData = ""
          // 未接收完成时不断触发'data',chunk本身是二进制
          req.on('data', chunk => {
                  postData += chunk.toString()
              }) 
          //end完结束
          req.on('end', () => {
              console.log(postData)
              res.end('hello world') //在这里返回，因为是异步
          })
      }
  });
  server.listen(8000);
  ```

+ 路由

  + nodejs处理路由
    + https://github.com/
    + https://github.com/username
    + https://github.com/username/xxx 



### 开发接口

+ 初始化路由：根据之前技术方案的设计，做出路由
+ 返回假数据：将路由和数据处理分离，以符合设计原则



### 搭建开发环境

+ 从 0 开始搭建，不使用任何框架
+ 使用nodemon 检测文件变化，自动重启 node
+ 使用 cross-env 设置环境变量，兼容 mac linux 和 windows