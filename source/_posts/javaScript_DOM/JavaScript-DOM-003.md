---
title: Javascript 图片库 节点
date: 2018-01-05 12:18
tags: 
- JavaScript
categories: 
- JavaScript DOM
typora-root-url: ..\..
---

通过简单的JavaScript 图片库案例来讲解函数应用及扩展。（[源代码+素材](https://share.weiyun.com/23f43be4bb82593df1ae9430fd07fb78)）

这是一个图片库小页面，通过单击1、2、3、4在原来的页面变换图片和描述。

![img](/images/JavaScript-DOM-003/1195417-20180104092521424-68628374.png)

下面是HTML标签：

```html
<body>
<h1>Snapshots</h1>
<ul>
    <li><a href="images/1.jpg" onClick="showPic(this); return false;" title="one">1</a></li>

<!--这些都是接来下要通过Javascript调用的标签属性-->
    <li><a href="images/2.jpg" onClick="showPic(this); return false;" title="two">2</a></li>
    <li><a href="images/3.jpg" onClick="showPic(this); return false;" title="three">3</a></li>
    <li><a href="images/4.jpg" onClick="showPic(this); return false;" title="four">4</a></li>
    <img src="images/show.jpg" alt="my img gallery" id="placeholder">
</ul>
<p id="description">Choose an image.</p>
</body>
```

图片变换步骤：1.获取a对象并取得href参数-> 2.获取img 对象-> 3.将href 的参数赋值给img 的src属性。

```javascript
//getElementsByTag( a );可以来获取a的对象，但是局限性，但是获取哪个a标签？因为Tag返回的是一段数组。
//这里我们可以封装一个方法function()用标签属性onClick调用这个函数
//在调用这个函数时，用this 关键字传递参数，就可以简单的把该a对象传递过去了
//onClick="showPic(this); return false;"为什么，后面要返回false。不加则会跳到href指定页面，返回false可以使链接无效。

showPic(whichpic)
function showPic(whichpic){
//whichpic就是传递过来的相对getElementsByTag( a );
        var source = whichpic.getAttribute("href");
        var placeholder = document.getElementById("placeholder");
        placeholder.setAttribute("src",source);
        }
如此一来，就可以变换图片了
```

文本变换如上步骤差不多，但在此前，先了解一下节点

1.childNodes 属性

　　在一颗节点树上，childNodes属性可以用来获取任何一个元素的所有子元素，它是一个包含这个元素全部子元素的数组：

　　element.childNodes

```javascript
function counBodyChildren(){
    var body_element = document.getElementsByTagName("body")[0];
    alert( body_element.childNodes.length );
}//这个小函数可以显示出你body 元素的子元素的总个数。
```

　　或者你想更清楚的了解childNodes具体是查询了哪个节点，可以尝试一下代码：

```html
<!DOCTYPE html>
<html>
<body> <p id="demo">请点击按钮来获得 body 元素子节点的相关信息。</p>

<button onclick="myFunction()">试一下</button>

<script>
function myFunction()
{
var txt="";
var c=document.body.childNodes;
for (i=0; i<c.length; i++)
  {
  txt=txt + c[i].nodeName + "<br>";
  };
var x=document.getElementById("demo");
x.innerHTML=txt;
}
</script>

<p><b>注释：</b>元素中的空格被视为文本，而文本被视为节点。</p>

</body>
</html>
```

　　得到的结果如下：

![img](/images/JavaScript-DOM-003/1195417-20180105114106003-1760732260.png)

了解节点后继续完善图片库变( showPic(whichpic) )更图片时的描述：

```javascript
function showPic(whichpic){
        var source = whichpic.getAttribute("href");
        var placeholder = document.getElementById("placeholder");
        placeholder.setAttribute("src",source);
//我们已经传入了a=whichpic标签对象了
//再用getAttribute获取a对象的title属性值,再获取P对象传入text。
        var text = whichpic.getAttribute("title");
        var description = document.getElementById("description");
        description.firstChild.nodeValue = text;
        }
//node.firstChild 等价于node.childNodes[0]
//node.lastChild 等价于node.childNodes[node.childNodes.length-1]
//补充：childNodes里现在已经不包括属性节点了。
```

​		要分清元素的value属性和nodeValue 不一样，nodeValue适用于“文本节点”和“属性节点”；对应“文档节点”和“标签节点”不起作用。

　　whichpic.getAttribute("title"); 还有一种写法whichpic.title;

　　前者只能get 不能赋值，后者可以。whichpic.title = "可赋值";