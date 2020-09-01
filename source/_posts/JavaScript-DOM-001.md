---
title: JavaScript 常见错误及用法习惯（新手入门）
date: 2017-12-29 15:53
tags: 
- JavaScript
categories: 
- JavaScript DOM
typora-root-url: ..
---

数据类型

1.字符串

　　如果想用双引号来包住一个本身就包含双引号的字符串，就必须用反斜杠对字符串中的双引号进行转义：

```javascript
var height = "about 5' 10\" tall";
值得注意的是反斜杠并不是字符串的一部分。您可以去验证一下：
alert(height);
```

![img](/images/JavaScript-DOM-001/1195417-20171228101154113-1163045201.png)

2.数组与对象

　　新手可能会用到关联数组，这种用法不是一个好习惯。这时应该使用通用的对象（Object）

　　什么是关联数组？

```javascript
var a = array(3);
a[0]="my";
a[1]=1995;
a[2]=false;　　//这种是典型的Beatles数组。

var a = array(3);
a[name]="my";
a[age]=1995;
a[live]=false;　　//用字符串代替数字值，这种就叫做关联数组，提高可读性。
```

既然都是为了可读性创建对象，何必加多一步数组来创建，不妨我们直接用对象（Object）来创建。

```javascript
var a = Object(); //或者 var a = {};
a.name = "my";
a.age = 1995;
a.live = false;
//还有一种更简洁的写法,也是最常用的写法
var a = {
    name:"my",
    age:1995,
    live:false
};
```

3.操作

　　算术操作法要养成好习惯，把多种操作组合在一起时，要用括号把操作分隔，避免歧义。

　　1+4*5 -> (1+4)*5 ->1+(4*5)

　　有时也常把自加写反（新手）再次提醒：“+=”。

4.条件语句

　　在判断语句if中，习惯性我们都会用｛｝。如果是语句很少时，可以写在同一行上。

```javascript
if ( 1 > 2 ) alert("hello world!");
```

​		在接下来的H5中的判断操作符，“比较操作符”需要更严谨的写法，尽量写“===”、“!==”。

　　还有我们常见的逻辑操作符 && 和 || 外，还要注意这种“逻辑非”的操作符 如：“!( num > 10 || num < 5 )”。

5.循环语句

　　与 if 相似的 while 多了循环，条件成立时就一直循环。还有一种 do{}while()，不管条件是否成立第一次都会执行。

　　for 循环最常用的就是遍历对象长度（Object.lenght）

```javascript
var beatles = Array("john","Paul","George","Ringo");
for ( var count = 0; count < beatles.length; count++ ){
    alert(beatles[count]);
}
```

6.函数与变量的作用域

　　理解函数，不如来理解它的意图。让函数体现得更有价值，如我们把它当作一种数据类型来使用：

```javascript
function convertToUSD( CNY ){
    var result = CNY * 6.5;
    return result;
}
var CNY = 99;
var USD = convertToUSD( CNY );
alert( USD );
//输出结果就是把人民币转换成美元。
```

　　值得注意的是1行convertToUSD( CNY )不等于6行convertToUSD( CNY )，CNY 是形参 CNY 是实参

　　function fn( CNY ) -> 封装函数括号内的是形参，也是唯一的。可以理解为函数 function( var CNY ) 给自己定义用的变量。

 

　　变量的作用域，我们在函数中声明的变量是局部变量，它只存在于这个函数的上下文。让新手混淆的是全局与局部问题：

```javascript
function square( num ) {
    total = num * num;
    return total;
}
var total = 50;
var number = square( 20 );
alert( total );
//要想使得全局 total 不受影响，可以写成如下所示
function square( num ) {
    var total = num * num;
    return total;
}
//这里替换上面，全局和局部就同名了，且局部影响不了全局变量
```

7.New 与 构造函数

　　构造函数可以初始化一个实例对象，对象的prototype属性是继承一个实例对象。这里就不细说，主要讲下新手常用方式。

　　当我们加new的时候是 构造对象，不加new 则是普通函数的调用。

```javascript
//当想声明几个任务对象时,可能你会一个一个去声明
var num1 = { name:Tim, age:20, ... };
var num2 = { name:May, age:19, ... };
var num3 = { name:Ken, age:26, ... };
... ...
//一一个声明时数量多，会很繁琐，难维护。
//这时我们就得写个函数去构造，也就是new
function Person( name,age ) {
   this.name = name;
   this.age = age;
   ... ...
}
var num1 = new Person( "Tim",20 );
var num2 = new Person( "May",19 );
var num3 = new Person( "Ken",26 );
... ...

//如果你只是想写一个方法调用，则不用new它。
//如之前的转换美元convertToUSD()只是个方法，没有必要生成对象。
```

