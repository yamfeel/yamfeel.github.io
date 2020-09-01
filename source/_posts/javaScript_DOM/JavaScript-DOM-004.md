---
title: JavaScript 最佳实践
date: 2018-01-12 10:32
tags: 
- JavaScript
categories: 
- JavaScript DOM
typora-root-url: ..\..
---

| **平稳退化：确保网页在没有Javascript 的情况下也能正常工作。** |
| ------------------------------------------------------------ |
| **分离Javascript ：把网页的结构和内容与Javascript 脚本动作行为分开。** |
| **向后兼容性：确保老版本的浏览器不会因为你的Javascript 脚本而死掉。** |
| **性能考虑：确定脚本执行的性能最优。**                       |

1.平稳退化

　　平稳退化编程属于保守派的编程思想，对于公司而言，公司更喜欢这种开发思想，因为用户至上嘛。假设：一款3D游戏的添加了光晕滤镜特殊处理效果，用户要是没有安装该技术库支持，就不给进入游戏or游戏进入就崩溃吧？怎么可能，这对于公司来说流失了多少用户。

```javascript
//如你想为用户创建一个简洁新窗口，使用window 对象的open() 方法来创建新的浏览器窗口。
window.open( url, name, features );
//url:打开的网页的URL地址。 name：则是新窗口的名字。 features：新窗口的各种属性，属性间逗号间隔。

//这个函数是创建一个宽300像素，高500像素的新窗口“popup”。
function popUp(winURL){
    window.open( winURL,"popup","width = 300,height = 500" );
}
//下面用如何的方式来调用这条函数？
```

"Javascript:"伪协议

　　真协议就是用来传输网络数据包,如HTTP协议（http://）、FTP协议（ftp://）等，伪协议只是让我们通过链接来调用Javascript函数。具体用法```<a href = "javascript: function();"></a>```

```html
<!--我们可以用伪协议调用popup 或者 用onclick 属性来调用。-->
<a href = "javascript: popup('http://baidu.com');">new</a>
<a href = "#" onclick = "popup('http://baidu.com'); return false;">new</a>
```

​		如上这样调用的代码很糟糕，如果用户禁止掉Javascript 脚本 或者 浏览器太老，将无法打开如上链接。“平稳退化”思想就是让我们的代码预留后路，让访问者即使没有Javascript的支持也能将操作进行下去。

 2.分离Javascript

　　随着技术的飞跃发展，更新迭代，技术的分工越来越明确、精细。大项目里不可能一人独揽所有开发，大家都是分工明确的，你做你的UI，我做我的脚本。

　　那么如何将上面Javascript 内嵌的事件处理函数分离？

```javascript
//可以在外部Javascript 文件里把一个事件添加到HTML 文档中的某个元素上
//element.event = action... 如:getElementsById(id).onclick = function()
//分离Javascript 如下
//首先我们要给a 标签加个class ，class = "popup";
window.onload = prepareLinks;
function prepareLinks(){
    var links = document.getElementsByTag('a');
    for( var i = 0; i < links.length; i++ ){
        if( links[ i ].getAttribute("class") == "popup" ){
            links[ i ].onlick = function{
                popUp( this.href );
                return false;
            }
        }
    }
}
```

3.向后兼容

　　有时候遇到一些比较老版本的Javascript DOM的js库不是很丰富，出现无法理解DOM 提供的方法和属性。这时候可能你的Javascript 脚本也不一定能运行。不止是在Javascript这方面，这是在开发时也经常出现的问题，当加载某些类库时，有时我们无法判断这个类库是否有没这个封装方法 or 有没开启这个配置项，就像那些做外包小项目的，做好随手一丢，在你的机子上测试没问题，在客户手上就不一定了。

```javascript
window.onload = prepareLinks;
function prepareLinks(){
//当js 库没有这个方法时，则中途离开
    if( !document.getElementsByTag ) return false;
    var links = document.getElementsByTag('a');
    for( var i = 0; i < links.length; i++ ){
        if( links[ i ].getAttribute("class") == "popup" ){
            links[ i ].onlick = function{
                popUp( this.href );
                return false;
            }
        }
    }
}
```

4.性能考虑 

　　尽量少访问 DOM，尽量减少标签（过多不必要的标签会增加DOM 树的规模，进而增加遍历元素时间）。

```javascript
//这段代码用了两次方法去执行相同的操作，浪费了一次搜索。
if( document.getElementsByTag("a").length > 0 ){
    var links = document.getElementsByTag("a");
    for( var i = 0; i < links.length; i++ ){
        //对每一个链接对象做处理
    }
}
//正确做法
var links = document.getElementsByTag("a");
if( links.length > 0 ){
    for( var i = 0; i < links.length; i++ ){
        //对每一个链接对象做处理
    }
}
```

​		合并和放置脚本，例如：A.js、B.js、C.js、D.js等导入js文件，不是框架的尽量合并放在一起，减少请求数量通常都是在性能优化时首先要考虑的。页面的初次加载时间也有很大影响，传统我们都把加载项放在<head>区域上，为了让用户得到最佳的阅览体验，可以将较大的js放到</body>之前，可以让页面变的更快。

　　压缩代码，是指把代码中不必要的字节，如空格和注释，统统删除，从而达到压缩文件的目地。