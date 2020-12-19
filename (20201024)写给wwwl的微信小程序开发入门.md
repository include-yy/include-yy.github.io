这篇介绍是写给 WWWL 四个人的，主要目的是介绍一些和微信小程序开发相关的基本知识，以应对《软件工程导论》随后的编码环节。如果您不是本文的受众而且也不愿意浪费上十几分钟的宝贵光阴，可以 `Alt+F4` 了。如果您对微信小程序感兴趣且刚开始学习的话，看看也无妨。

如果发现了任何的错误，请联系我，我会迅速改正。

# 0X00 写在前面

本文的目的，其一是介绍一些编程的常识性知识，使得整个团队在编程术语的使用上，以及编程知识的了解上有一个最基本的共识，这样更有利于团队之间的沟通。其二是介绍微信小程序的基本知识，即程序的组织结构与组成、使用的程序语言等。其三是介绍微信小程序开发的环境，即**微信开发工具**的基本操作方法，来帮助熟悉开发工具。

看完了本文，能够有什么收获呢？

- 了解基本的编程/电脑知识（一点点）

- 了解微信开发的语言，微信程序的项目组织结构，以及如何查阅文档

- 了解微信开发工具的基本使用方式

如您所见，我使用的是“了解”而不是“学会”，如果看完了本文能对整个开发过程以及开发方法有了一个基本的了解的话，那么我的目的就达到了。能写一个 Hello World 出来就说明你会了。

你可能会问，微信的官方文档这么全，为什么不直接去看？官方文档虽全，但是针对性比较差，这里讲到的都是一些最简单的东西，目的就是能够写个程序出来，而不是淹没在文档的大海中。

闲话少说，让我们开始吧。

# 0X01 基本的编程/计算机知识

这部分的内容包括：

- 什么是文件后缀

- 什么是语言的强弱/动静类型

- 什么是前后端

- 什么是 Javascript，CSS，HTML

这部分的东西了解一下就行，没必要一定弄的清清楚楚，毕竟我们到时候编码时会写就行。

如果您已经了解过了，可以直接从 0X02 开始看。

## 1.文件类型与文件后缀

这里直接参考百度百科：文件后缀名也叫文件扩展名，用来表示某种文件格式。文件扩展名是加在主文件后面的，用”.“分隔。

常见的文件后缀有 .txt（文本文件），.pptx（ppt 文件），.pdf（ptf 文件），.rar（rar 格式压缩文件）等等。我们学过的 C 语言的源文件的文件后缀就是 .c。

文件后缀的意义是帮助辨识文件的类型，在 Windows 系统上，对每种后缀的文件，都有一个对应的默认打开软件。如果某个文件没有后缀的话，当你双击它时，系统会弹出这样的窗口，来提示你选择一个打开它的应用程序：

<img title="" src="file:///C:/Users/yy/Desktop/img/1.PNG" alt="avater" width="257" data-align="center">

如果你使用过百度网盘的手机 APP 的话，你应该知道，凡是以 .rar 作为后缀的文件，在下载之后是只能在线解压的，不能把文件放到其他应用中的（也许只有 ios 是这样），没有会员的话，解压包不能解压，相当于白下了一次。要解决这个问题，你可以在下载之前将文件后缀删除或改为任意的其他后缀，这样百度网盘下载完成后识别不了文件类型，你就可以随意处理文件了。

扯远了。如果你在你的电脑上像这样看不到文件后缀的话：

![avater](C:\Users\yy\Desktop\img\2.PNG)

你可以勾选这里的”文件扩展名“：

![avater](C:\Users\yy\Desktop\img\3.PNG)

关于文件后缀名的知识就到这里。接下来我们会提到几种文件格式，它们是 .json，.html 和 .css。

## 2.编程语言的静态/动态类型，强/弱类型

为什么要提到这个问题？这是因为我们即将使用的 javascript 与我们学过的 C 是一种截然不同的语言，C 语言是静态类型，强（也许吧，不过网上貌似认为它是弱类型）类型，而 javascript 是动态类型、弱类型。如果让静态/动态和强/弱四种属性两两组合成一张 2 乘 2 的表的话，那么 C 和 javascript 的位置在对角线上。

|      | 强类型     | 弱类型                |
| ---- | ------- | ------------------ |
| 动态类型 | 强，动态    | 弱，动态（javascript）   |
| 静态类型 | 强，静态（C） | 弱，静态（C，maybe here） |

简单理解一下的话（不一定完全正确），语言中的类型是对值的一个约束，有助于检查错误。

那么什么是静态和动态类型呢？静态类型语言在编译期间检查类型，而动态类型语言在执行期间检查类型。

强类型和弱类型又是什么呢？强类型偏向于不容忍隐式类型转换，比如 Python 中字符串和数字相加是会报错的。弱类型偏向于容忍隐式类型转换，在 javascript 中，你可以试试 1 + "1"，看看能够得到什么结果。

本小节可以说是简单介绍了一下编程语言的类型分类，但主要目的是提醒注意 javascript 的类型问题，到时候遇到了玄学问题可以往类型这个方向想一想。在你的浏览器中按下 `F12` 并在浏览器控制台中输入 1 + "1" 和 1 - "1" 试试，结果一定很有趣。

## 3.什么是前端和后端

参考资料【1】中这样写道：

> **Front-end developers work on what the user can see while back-end developers build the infrastructure that supports it.**

翻译过来的意思是：前端开发者负责用户看得到的部分，而后端开发者负责构建支持前端功能的部分。

前端指软件的用户界面部分，而后端指工作在幕后的服务器，应用和数据库，它们向用户传递信息。前端和后端合在一起，就是全栈，也就是什么都会做的意思。

我们的编程主要任务是完成前端的工作，用用第三方的后端就行，毕竟我们也不会（笑）。

## 4.什么是 javascrpit，html 与 CSS

javascrpit（以下简称 JS），html 和 CSS 并称“前端三大件”。

HTML是网页内容的载体，内容就是网页制作者放在页面上想让用户浏览的信息，比如文字，图片，视屏等等，就是定义网页内容。
CSS 是网页样式的表现，可以想象成网页的衣服，比如标题的变化，背景图片以及边框等等，就是定义我这个网页的布局是什么样的。
JavaScript 是用来实现网页上的动态效果，控制网页行为，比如有什么样的动作，弹出消息之类的。

接下来，我对它们 3 个分别做一个简单的介绍。

### 4.1.什么是 HTML

HTML 的英文全名是 Hyper Text Markup Language，即“超文本标记语言”，它并不是一种编程语言，而是一种标记语言。它的文件后缀名是 .html。

至于什么是标记语言（ML），它是一种将文本以及文本相关的其他信息结合起来，展现出关于文档结构和数据处理细节的计算机文字编码。与文本相关的其他消息使用标记来进行标识。

最简单的例子，例如下面的纯文本：

```
Hello
World
```

使用 HTML 的话，要想得到上面的效果，应该这样写：

```html
<p> Hello </p> <p> World </p>
```

其中的 \<p\> 和 \</p\> 就是标记。

有关 HTML 的学习资料有很多，比如 W3C 的 [HTML 教程](https://www.w3school.com.cn/html/index.asp) 

### 4.2.什么是 CSS

CSS 的英文全名是 Cascading Style Sheets，即“层叠样式表”。HTML 负责确定网页中的内容，而 CSS 负责确定如何显示（大小，粗细，颜色，对其和位置）这些内容。

CSS 可以将文件的内容与它的外观分割开来，以此简化 HTML 的内容（即不需要在 HTML 中列出外观的信息）。

在上面的例子中，我们分行显示了“Hello World”，现在我们可以使用 CSS 为它加上各种样式。html 引用 css 有多种方法，它可以内联，可以使用内部样式表，也可以使用外部样式表。这里直接使用内部样式表。

```html
<style>
pe
{
    color:red;
    text-align:center;
}
</style>
<pe> <p> Hello </p> </pe>
<pe> <p> World </p> </pe>
```

这样，你打开这个 html 文件时，你会看到居中的，红色的 "Hello World"。

使用外部样式表就是引用 .css 文件，这里把样式定义部分移到 1.css 中

```css
pe
{
    color:red;
    text-align:center;
}
```

然后编写这样的 html 文件：

```html
<head>
 <link rel="stylesheet" type="text/css" href="1.css">  
<pe> <p> Hello </p> </pe>
<pe> <p> World </p> </pe>
</head>
```

在浏览器中打开的效果应该和内部样式表相同。

有关 CSS 的学习资料也不少，比如 菜鸟的 的 [CSS 教程 | 菜鸟教程](https://www.runoob.com/css/css-tutorial.html)

### 4.3.什么是 javascript

javascript 自然是一门编程语言，虽然它的名字里面有“java”，但是它和 java 没有半毛钱的关系，就像“雷锋”和“雷锋塔”一样。

以下内容引自维基百科：

> javascript 是一种高级的解释性语言，它支持面向对象程序设计，命令式编程和函数式编程。它提供语法来操控文本，数组，日期以及正则表达式等。
> 
> javascript 与 java 在名字或语法上有很多相似性，但这两门语言从设计之初就有很大的不同，javascript 的语言设计主要受到了 Self 和 Scheme 的影响。在语法结构上它又与 C 语言有很多相似之处。

据说现在 JS 是最快的解释性语言，不过我也只是随便看网页时看到的，这句话的真实性也待考证。

就像维基上说的，JS 与 C 的语法是很相似的，比如以下的计算阶乘的代码：

```javascript
var i;
var n = 1;
for (i = 1; i <= 10; i++) {
    n = n * i;
}
console.log(n);
```

除了变量定义和输出与 C 不同之外，for 循环的结构与 C 简直一模一样。这样的相似之处还有不少，我们已经学过了 C，想要快速入门 JS 应该不会很难。需要注意的是，JS 也有它自己的很多特性，在某些情况下不要套用原先的经验。

JS 可以写到 html 中，实现一些功能，比如以下的代码实现了 Hello World 的输出。：

```html
<body>

<script>
document.write("<h1>Hello World!</h1>");
</script>

</body>
```

这里提一下 JSON，JSON 的全称是 JavaScrpit Object Notation，即 JavaScript 对象标记。它是一种基于纯文本的数据格式。它的基本数据类型有

- 数值

- 字符串

- 布尔值 true 和 false

- 数组（列表）

- 对象

- 空类型，写作 null

下面是一个 JSON 的例子：

```json
{
  "name": "example",
  "description": "A really long description that needs multiple lines.\nThis is a sample project to illustrate why JSON is not a good configuration format. This description is pretty long, but it doesn't have any way to go onto multiple lines.",
  "version": "0.0.1",
  "main": "index.js",
  "//": "This is as close to a comment as you are going to get",
  "keywords": ["example", "config"],
  "scripts": {
  "test": "./test.sh",
  "do_stuff": "./do_stuff.sh"
  }
}
```

JS 的教程也有很多，比如 [JavaScript 教程 | 菜鸟教程](https://www.runoob.com/js/js-tutorial.html)

## 总结

本小节提到了四个话题，前三个仅仅需要了解一下，但是前端三大件是我们在开发过程中不得不用到的东西，需要一定的学习。对于 HTML 和 CSS，我们不一定要写的很顺畅，但是至少需要了解组成它们的基本元素，以及最基本的语法。我们在设计和实现 UI 时一定会用到它们。

对于 javascript，我们应该学会它的基本使用方法。随便找一个教程，然后在浏览器的控制台上对着教程敲上一些代码是必要的工作。除了菜鸟教程外，这本书也还不错：[Eloquent JavaScript](https://eloquentjavascript.net/)。

对编程语言的学习，这里简单提一点：

- 对编程语言基本组成元素的学习

- 对基本语法的学习

- 对语言提供的抽象手段的学习

- 对语言提供的库的学习

- （optional）学习语言的高级特性

基本元素就是指基本的数据类型，变量定义等。基本语法指分支和循环语句。抽象手段指语言提供的结构体和类之类的东西。库就是语言标准库，提供了一些基础的功能。

当然了，所谓”实践是检验真理的唯一标准“，能写就行，不会的话读文档，边读边写。

在微信中，HTML 成了 WXML，CSS 成了 WXSS。它们有相应的文档来供我们学习。

[WXML | 微信开放文档](https://developers.weixin.qq.com/miniprogram/dev/reference/wxml/)

[WXSS | 微信开放文档](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html) 

# 0X02 微信小程序开发的知识

有了上面讲的东西（不看也行），现在我们可以正式开始介绍微信开发的相关知识了。

首先需要说明的是，微信小程序的官方文档在我看来已经做到了相当程度的通俗易懂，这一小节主要是介绍一些最基本的内容，几乎就是告诉你怎么看文档，以及部分文档内容的搬运。

这部分参考的内容主要是微信的官方文档 [小程序简介 | 微信开放文档](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/) ，考虑到这文档内容可能会时间变化而与我这里的描述不符，这里我记一下参考时间：2020 年 10 月 24 日（真巧啊，所谓的程序员节，2020 - 1024 = 996）。

## 1.微信小程序是什么

顾名思义，微信小程序就是运行在微信上的程序。微信的官方文档这样写道：小程序是一种全新的连接用户和服务的方式，它可以在微信内被便捷地获取和传播。

就像网页技术是跨平台一样，小程序也是跨平台的，编写小程序不必为 ios 或 Android 分别开发。

微信小程序的优点有：

- 快速加载

- 开发简单

- 不用专门安装和卸载

- 容易通过微信群和朋友圈进行扩散传播

## 2.渲染层与逻辑层



## 3.一个项目的组织结构和文件组成

# 0x10 更多

微信公众平台 —— 账号登入地点： https://mp.weixin.qq.com

微信开发工具下载地址： [稳定版 Stable Build | 微信开放文档](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)，选择稳定版 Windows 64。

微信小程序官方文档（reference） —— 指南：[小程序简介 | 微信开放文档](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/)

微信小程序开发指南（toturial）：[教程 | 《小程序开发指南》](https://developers.weixin.qq.com/ebook?action=get_post_info&docid=0008aeea9a8978ab0086a685851c0a)

# 0x100 参考资料

【1】[What Is the Difference Between Front-End and Back-End Development?](https://www.conceptatech.com/blog/difference-front-end-back-end-development)
