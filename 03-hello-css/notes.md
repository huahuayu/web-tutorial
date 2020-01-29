## CSS(Cascading Style Sheets)
css是和html完全独立的语言，html负责描述骨架，css负责描述样式。
![](https://cdn.liushiming.cn/img/20200121142503.png)
CSS提供的词汇表告诉web浏览器诸如“我希望我的标题非常大，我的边栏出现在正文的左边。”HTML没有做出这种布局决定的术语——它只能说，“那是一个标题，那是一个侧边栏。”

一个CSS“规则”总是以一个“选择器”开始，它定义了它所应用的HTML元素。在本例中，我们尝试设置<body>元素的样式。在选择器之后，我们在一些花括号里面有“声明块”。我们在这里设置的任何“属性”都会影响<body>元素。


color是CSS规范定义的一个内置属性，它决定所选择的HTML元素的文本颜色。它接受一个表示颜色的十六进制值。#FF0000表示鲜红色。

CSS属性有点像HTML属性，因为它们都处理键值对。但是，这里我们定义的是表示性信息，而不是底层内容的语义意义。

## css和html绑定
使用`<link>`标签来绑定css
``` html
<head>
  <meta charset='UTF-8'/>
  <title>Hello, CSS</title>
  <link rel='stylesheet' href='styles.css'/>
</head>
```
![](https://cdn.liushiming.cn/img/20200121143523.png)
## link和a的不同
1. link只能用在header中，a只能在body中。
1. link是用来关联项目中的其他文件的，一般是css文件。
1. a是在body中做超链接的（可以跳到另一个网页，也可以跳到本网页中的其他地方）

## css语法
``` css
body {
  color: #414141;               /* Dark gray */
  background-color: #EEEEEE;    /* Light gray */
}
```
![](https://cdn.liushiming.cn/img/20200121143015.png)

`color`:用来定义文字颜色  
`background-color`：定义背景色  
`/*  */` 定义注释。css的注释格式和html注释格式不同。 

## 度量单元
`px` - pixel像素  
`em` - 基于base像素点的相对倍数
![](https://cdn.liushiming.cn/img/20200121163557.png)

## 选中多个元素
错误示范：
``` css
h1 {
  font-family: "Helvetica", "Arial", sans-serif;
}

h2 {
  font-family: "Helvetica", "Arial", sans-serif;
}

h3 {
  font-family: "Helvetica", "Arial", sans-serif;
}
```
正确示范：
``` css
h1, h2, h3, h4, h5, h6 {
  font-family: "Helvetica", "Arial", sans-serif;
}
```

## 定义字体
`font-family` - 定义字符集。如果定义了多个，先从左边的字符集开始用，用户本地没有则用右边的，直至默认的sans-serif。
``` css
h1 {
  font-family: "Helvetica", "Arial", sans-serif;
}
```

![](https://cdn.liushiming.cn/img/20200121164846.png)

## 列表样式
``` css
ul {
  list-style-type: circle; /*无顺序列表，圆点*/
}

ol {
  list-style-type: lower-roman; /*有顺序列表，序号*/
}
```

## 全局css样式表
一份css样式表可以被多个html网页引用，
![](https://cdn.liushiming.cn/img/20200121170809.png)

## 更多的样式
### 文本修饰
``` css
a {
  text-decoration: none; /* 文本修饰none，作用在a标签下，超链接默认的下划线就没有了  */
}
```

### 文本对齐
``` css
p {
  text-align: left; /* right, center, or justify都可以 */
}
```

### 文字粗细
``` css
h1, h2, h3, h4, h5, h6 {
  font-family: "Helvetica", "Arial", sans-serif;
  font-weight: normal;      /* 正常粗细 */
}
```

## 叠层样式
叠层(cascading)样式

从上到下优先级升高: 
* 浏览器的默认样式表
* 用户定义的样式表
* 外部样式表
* 页面自定义样式
* 行内样式

![](https://cdn.liushiming.cn/img/20200121175117.png)

## 页面自定样式
`<link>` - 定义了外部样式表  
`<style>` - 定义了页面样式  
页面样式在同一属性上会覆盖外部样式
``` css
<head>
  <meta charset='UTF-8'/>
  <title>Dummy</title>
  <link rel='stylesheet' href='styles.css'/>
  <style>
    body {
      color: #0000FF;    /* Blue */
    }
  </style>
</head>
```
![](https://cdn.liushiming.cn/img/20200121175725.png)

在html文件中定义`style`只能做为临时使用，还是放在一个单独的文件中好维护。

## 行内样式
在一行内也可以用`style`定义样式，这将覆盖页面自定义样式。但是不推荐这么做。
``` css
<p>Want to try crossing out an <a href='nowhere.html'
   style='color: #990000; text-decoration: line-through;'>obsolete link</a>?
   This is your chance!</p>
```

## 多个样式组合使用
`styles.css`是共用的样式，`product`和`blog`页面各有独特的样式。且被后`link`的样式会覆盖先写的。
``` css
<!-- All product pages have this -->
<head>
  <link rel='stylesheet' href='styles.css'/>
  <link rel='stylesheet' href='product.css'/>
</head>
<!-- While all blog posts have this -->
<head>
  <link rel='stylesheet' href='styles.css'/>
  <link rel='stylesheet' href='blog.css'/>
</head>
```

## 跨平台样式
根据用户使用的不同终端使用不同的样式
![](https://cdn.liushiming.cn/img/20200121180449.png)