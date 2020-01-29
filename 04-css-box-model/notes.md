## css box model
“CSS框模型”是一组定义如何呈现Internet上的每个web页面的规则。CSS将HTML文档中的每个元素视为一个“框”，其中包含许多不同的属性，这些属性决定了元素在页面中的位置。到目前为止，我们所有的web页面都只是一个接一个呈现的元素。box模型是我们定制这个默认布局方案的工具包。
![](https://cdn.liushiming.cn/img/20200122175240.png)

屏幕上呈现的每个HTML元素都是一个框，它们有两种样式:“块”框和“内联”框。  

![](https://cdn.liushiming.cn/img/20200122180821.png)

## display属性
`display: none;` - 不展示
`display: inline;` - 该元素生成一个或多个行内框
`display: block;` - 块展示（独占一行）
`display: inline-block;` - 该元素生成一个块级别框，但是整个框的行为就像是一个内联元素。 

### inline 和 inline-box的区别
#### margin与padding
inline元素只能设定左右margin、padding，上下的是不起作用的
inline-block的上下左右都可以设定margin和padding
#### width与height
inline元素不能设定width与height
inline-block元素可以设定width和height
#### 换行
如下图，改变窗口大小会发现，inline-block的元素在剩余空间不够一个块的宽度时就会换行，而inline则会断行显示。

![](https://cdn.liushiming.cn/img/20200122212930.png)

## 箱模型
“CSS框模型”是一组确定网页中每个元素大小的规则。它给每个框(内联和块)四个属性:

Content(内容)——元素中的文本、图像或其他媒体内容。
Padding(填充)——方框内容和边框之间的空间。
Border(边框)-方框的边距和边距之间的线。
Margin(边距)-方框与周围方框之间的空间。
![](https://cdn.liushiming.cn/img/20200122213441.png)

## padding
``` css
h1 {
  padding: 50px;
}
```

``` css
p {
  padding-top: 20px;
  padding-bottom: 20px;
  padding-left: 10px;
  padding-right: 10px;
}
```
以下和上面等价
``` css
p {
  padding: 20px 10px;  /* Vertical  Horizontal */
}
```
![](https://cdn.liushiming.cn/img/20200122214637.png)

``` css
p {
  padding: 20px 0 20px 10px;  /* Top  Right  Bottom  Left */
}
```
![](https://cdn.liushiming.cn/img/20200122215226.png)

## border
``` css
h1 {
  border: 1px solid #5D6063;
}
```
![](https://cdn.liushiming.cn/img/20200122221159.png)

``` css
border-bottom: 1px solid #5D6063;
```

## margin
边距定义元素边框外的空间。或者更确切地说，一个盒子和它周围的盒子之间的空间。让我们添加一些空间到每个<p>元素的底部:  
在很多情况下，边距和填充可以完成相同的事情，这使得很难确定哪一个是“正确的”选择。最常见的原因是:
* 盒子的填充有背景，而边距总是透明的。
* 元素的单击区域包含padding，而不包含margin。
* padding垂直折叠，而margin填充不会。

## margin垂直重叠
![](https://cdn.liushiming.cn/img/20200122222551.png)
如果不想两个box的margin重叠可以这么做：  
``` html
<p>Paragraphs are blocks, too. <em>However</em>, &lt;em&gt; and &lt;strong&gt;
elements are not. They are <strong>inline</strong> elements.</p>

<div style='padding-top: 1px'></div>  <!-- Add this -->

<p>Block elements define the flow of the HTML document, while inline elements
do not.</p>
```
![](https://cdn.liushiming.cn/img/20200122222751.png)

## content boxes
`width` 和 `height`属性只作用于`content`，想象一下，用三个宽度都是200px的盒子来填充一个600px的容器，但它们都不合适，因为它们都有1px的边框(实际宽度是202px)。
![](https://cdn.liushiming.cn/img/20200127171549.png)

幸运的是，CSS允许通过`box-sizing: border-box`属性将边框包含在内，`content`会变为动态长度:
``` css
div {
  color: #FFF;
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;
  
  width: 200px;
  box-sizing: border-box;  /* Add this */
}
```
![](https://cdn.liushiming.cn/img/20200127172121.png)

## div居中对齐
块级元素的水平margin设为auto的时候，块级元素会居中(下面css最后一句)  
``` css
div {
  color: #FFF;
  background-color: #4A90E2;
  font-weight: bold;
  padding: 20px;
  text-align: center;

  width: 200px;
  box-sizing: border-box;
  margin: 20px auto; /* Vertical  Horizontal */
}
```

注意，这只适用于具有显式宽度定义的块。`width: 200px`，按钮将是整个浏览器的宽度，使“居中对齐”毫无意义。

## 修改默认样式
浏览器会给box加上默认的margin/padding,不同的浏览器会有不同的默认值。最好去掉这些默认值，让页面变得确定。这是一个最佳实践。
``` css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

![](https://cdn.liushiming.cn/img/20200127173757.png)

## span和div的区别
SPAN 和 DIV 的区别在于，DIV(division)是一个块级元素，可以包含段落、标题、表格，乃至诸如章节、摘要和备注等。而SPAN 是行内元素，SPAN 的前后是不会换行的，它没有结构的意义，纯粹是应用样式，当其他行内元素都不合适时，可以使用SPAN。

## 小结
当我们深入到构建复杂的web页面时，我们将学习更多关于CSS框模型的实际应用。现在，把它看作是CSS工具箱中的一个新工具。有了本章的一些关键概念，你会觉得更有能力把设计模型转换成现实的网页:

所有东西都是一个盒子。
盒子可以是内联的，也可以是块级的。
盒子包含内容、填充、边框和边距。
它们在如何交互方面有看似随意的规则。
掌握CSS框模型意味着你可以布局大部分网页。
和上一章一样，我们刚刚提到的CSS属性看起来可能很简单，但它们确实很简单。但是，通过CSS框模型的镜头来观察你访问的网站，你会发现这些东西到处都是。