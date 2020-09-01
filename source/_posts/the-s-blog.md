---
title: Vue & webpack -VScode in 2019.8
date: 2019-08-22 07:35
tags: 杂物间
categories: 杂物间
typora-root-url: ..
---

**配置版本过时，谨慎参考**

1.创建项目文件夹 用vscode打开。

2.ctrl+` 打开 vscode终端 用 npm 包管理命令 ：npm init -y 回车。

3.在项目文件夹根目录创建 src （项目源代码） 和 dist （项目打包输出文件）

4.创建项目src/index.html，src/main.js

5.用npm本地安装webpack生产环境 ：npm i webpack -d，别忘了还有npm i webpack-cli -d，请看手册https://www.webpackjs.com/guides/installation/。

　　测试node_modules\.bin\webpack .\src\main.js -o .\dist\bundle.js 看看是否能成功打包

6.本地安装自动打包生产工具：npm i webpack-dev-server -d。

7.在项目根目录新建一个webpack的配置文件 webpack.config.js

8.本地安装webpack自动缓存插件：npm i html-webpack-plugin -d。

```javascript
//由于 webpack 是基于Node进行构建的，所以，webpack的配置文件中，任何合法的Node代码都是支持的
var path = require('path');

// 在内存中，根据指定的模板页面，生成一份内存中的首页，同时自动把打包好的bundle注入到页面底部
// 如果要配置插件，需要在导出的对象中，挂载一个plugin 节点
var htmlWebpackPlugin = require('html-webpack-plugin');


// 当以命令行形式运行webpack（node_modules\.bin\webpack） 或者 webpack-dev-server 的时候，工具会发现，我们并没有提供 要打包的文件的 入口 和 出口文件，此时，他会检查项目根目录中的配置文件，并读取这个文件，就拿到了导出的这个配置对象，然后根据这个对象，进行打包构建。
module.exports = {
    entry: path.join(__dirname,'./src/main.js'),// 入口文件
    output: {
        path: path.join(__dirname,'./dist'),// 输出路径
        filename:'bundle.js'// 指定输出文件的名称
    },
    plugins:[//所有webpack 配置插件的节点
        new htmlWebpackPlugin({//创建一个在内存中生成 HTML 页面的插件
            template: path.join(__dirname,'./src/index.html'),//指定模板页面，将来会根据指定的页面路径，去生成内存中的页面
            filename:'index.html'// 设置生成的页面名称
        })
    ],
}
```

9.在package.json中添加脚本测试

```javascript
{
  "name": "04.webpack",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server --open --port 3000 --contentBase src --hot"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "html-webpack-plugin": "^3.2.0",
    "webpack": "^4.39.2",
    "webpack-cli": "^3.3.7",
    "webpack-dev-server": "^3.8.0"
  }
}
```

 在终端中 npm run dev 测试

10.引入样式

　　本地安装loader：npm i style-loader css-loader -d

　　按需求安装：npm i less-loader less -d，npm i sass-loader node-sass -d

```javascript
//由于 webpack 是基于Node进行构建的，所以，webpack的配置文件中，任何合法的Node代码都是支持的
var path = require('path');

// 在内存中，根据指定的模板页面，生成一份内存中的首页，同时自动把打包好的bundle注入到页面底部
// 如果要配置插件，需要在导出的对象中，挂载一个plugin 节点
var htmlWebpackPlugin = require('html-webpack-plugin');


// 当以命令行形式运行webpack（node_modules\.bin\webpack） 或者 webpack-dev-server 的时候，工具会发现，我们并没有提供 要打包的文件的 入口 和 出口文件，此时，他会检查项目根目录中的配置文件，并读取这个文件，就拿到了导出的这个配置对象，然后根据这个对象，进行打包构建。
module.exports = {
    entry: path.join(__dirname,'./src/main.js'),// 入口文件
    output: {
        path: path.join(__dirname,'./dist'),// 输出路径
        filename:'bundle.js'// 指定输出文件的名称
    },
    plugins:[//所有webpack 配置插件的节点
        new htmlWebpackPlugin({//创建一个在内存中生成 HTML 页面的插件
            template: path.join(__dirname,'./src/index.html'),//指定模板页面，将来会根据指定的页面路径，去生成内存中的页面
            filename:'index.html'// 设置生成的页面名称
        })
    ],
    module:{//这个节点，用于配置所有第三方模块加载器
        rules:[// 第三方模块的匹配规则
            {test:/\.css$/,use:['style-loader','css-loader']},//配置处理 .css 文件的第三方规则
            {test:/\.less$/,use:['style-loader','css-loader','less-loader']},
        ]
    }
}
```

11.引入url资源：npm i url-loader file-loader -D

```javascript
module:{//这个节点，用于配置所有第三方模块加载器
        rules:[// 第三方模块的匹配规则
            {test:/\.css$/,use:['style-loader','css-loader']},//配置处理 .css 文件的第三方规则
            {test:/\.less$/,use:['style-loader','css-loader','less-loader']},
            {test:/\.scss$/,use:['style-loader','css-loader','sass-loader']},
            {test:/\.(jpg|png|gif|bmp|jpeg)$/,use:'url-loader'},
        ]
    }
```

12.引入字体库

{test:/\.(ttf|eot|svg|woff|woff2)$/,use:'url-loader'},