---
title: JavaScript 获取元素、设置属性
date: 2018-01-03 11:44
tags: 
- JavaScript
categories: 
- JavaScript DOM
typora-root-url: ..\..
---

有3种DOM方法可获取元素节点，分别通过ID、标签名、类名来获取。

1.getElementsById

　　通过id来访问元素，注意开头字母不是写成大写，如果把它写错成“GetElementById”，是无效的。

　　document.getElementsById( id )　　这个id值必须写在单引号或者双引号里面

 

2.getElementsByTagName

　　getElementsByTagName 通过标签名来访问元素，方法返回一个对象数组，每个对象分别对应着文档里有着给定标签的一个元素。

　　document.getElementsByTagName( Tag )

 

3.getElementsByClassName　

　　getElementsByClassName 通过类名来访问元素，与TagName类似，都是返回一个数组，它还可以查找带有多个类名的元素。

　　getElementsByClassName( class )

　　注意是访问带有多个类名的元素，不是可以访问多个类名。

```html
document.getElementsByClassName("a b");
//只能访问
<div class="a b"></div>
//不可访问
<div class="a"></div>
<div class="b"></div>
```


获取和设置属性

1.getAttribute

　　这个方法用来获取节点的各个属性值，但不属于 document 对象，所以不能通过document 对象调用。

```javascript
//用法
<p title="hello">Yes!</p>
<p>Yes!</p>
var paras = document.getElementsByTagName("p");
for ( var i = 0; i < paras.length; i++ ){
    title_text =  paras[ i ].getAttribute("title");
    if ( title_text != null){//等价( title_text )
        alert( title_text );
    }
}
```

2.setAttribute

　　setAttribute()用来设置节点的各个属性值。

```javascript
//用法
<p title="hello">Yes!</p>
var paras = document.getElementsByTagName("p");
for ( var i = 0; i < paras.length; i++ ){
    var title_text = paras[ i ].getAttribute("title");
    if ( title_text ){
        paras[ i ].setAttribute("title","hey");
        alert( paras[ i ].getAttribute("title") );
    }
}
```

这5个方法是编写许多DOM 脚本的基础！