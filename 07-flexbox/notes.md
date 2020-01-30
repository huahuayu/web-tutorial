## 前言
“Flexible Box”或“Flexbox”布局模式为定义web页面的整体外观提供了浮动的另一种选择。浮动只允许我们水平地放置盒子，而flexbox让我们完全控制盒子的对齐、方向、顺序和大小。
![](https://cdn.liushiming.cn/img/20200129193805.png)

web目前正在经历一个重大的转变，因此有必要对行业的状态进行一些讨论。在过去十年左右的时间里，浮动是设计复杂网页的唯一选择。因此，即使在传统浏览器中，它们也得到了很好的支持，开发人员已经使用它们构建了数百万个web页面。这意味着在您的web开发生涯中，您将不可避免地遇到浮点数(因此前一章并不是完全的浪费)。

然而，浮动最初是为杂志风格的布局而设计的，我们用浮动表示内容。不管我们在上一章看到了什么，您可以用浮动创建的布局类型实际上是有一定限制的。即使是一个简单的侧边栏布局，从技术上讲，也有点不太好。Flexbox的发明就是为了打破这些限制。

我们终于到了一个关键时刻，浏览器支持已经达到临界量，开发人员可以开始用flexbox构建完整的网站。我们的建议是尽可能多地使用flexbox来布局你的web页面，当你需要文本在一个方框中流动时(例如，当你需要一个浮动文本时)保留浮动。或者当您需要支持遗留的web浏览器时。
![](https://cdn.liushiming.cn/img/20200129194029.png)

## flexbox概述
Flexbox使用了两种我们从未见过的盒子:“flex容器”和“flex项目”。flex容器的工作是将一组flex项组合在一起并定义它们的位置。  
![](https://cdn.liushiming.cn/img/20200129211940.png)

每个直接作为flex容器子元素的HTML元素都是一个“项”。Flex项可以单独操作，但在大多数情况下，由容器决定它们的布局。flex项目的主要目的是让它们的容器知道需要放置多少东西。

与基于float的布局一样，用flexbox定义复杂的web页面就是关于嵌套盒的。您将一组flex项目排列在一个容器中，然后，这些项目可以作为它们自己项目的flex容器。当您处理本章中的示例时，请记住布置页面的基本任务并没有改变:我们仍然只是移动一堆嵌套的框。

## flex container
使用flexbox的第一步是将一个HTML元素转换成一个flex容器。我们使用display属性来实现这一点，这应该是CSS框模型一章中熟悉的内容。通过给它一个flex值，我们告诉浏览器框中的所有东西都应该使用flexbox来呈现，而不是默认的框模型。

添加以下行到我们的.menu-container规则，将其转换为一个flex容器:
``` css
.menu-container {
  /* ... */
  display: flex;
}
```

这就支持了flexbox布局模式——没有它，浏览器就会忽略我们将要介绍的所有flexbox属性。显式定义flex容器意味着您可以将flexbox与其他布局模型(例如，浮动和我们将在高级定位中学习的所有内容)混合和匹配。

![](https://cdn.liushiming.cn/img/20200129212947.png)

## flex iterm
有了flex容器之后，接下来的工作是定义其项的水平对齐。这就是辩护内容属性的作用。我们可以使用它来居中我们的。menu，像这样:  

``` css
.menu-container {
  /* ... */
  display: flex;
  justify-content: center;    /* Add this */
}
```

这与向.menu元素添加`margin: 0 auto`声明具有相同的效果。但是，请注意我们是如何做到这一点的:将一个属性添加到父元素(flex容器)中，而不是直接添加到我们想要居中的元素(flex项目)中。在flexbox中，像这样通过容器来操作项目是一个常见的方式，这与我们到目前为止定位箱子的方式有点不同。

![](https://cdn.liushiming.cn/img/20200129230825.png)

## 多个flex iterm
将menu样式改为justify-content:space-between;
``` css
.menu {
  border: 1px solid #fff;
  width: 900px;
  display: flex;
  justify-content: space-between;
}
```
![](https://cdn.liushiming.cn/img/20200130151743.png)


## 组合flex iterm
![](https://cdn.liushiming.cn/img/20200130152918.png)
将sign up 和login放在一个新的div  
``` html
<div class='menu'>
  <div class='date'>Aug 14, 2016</div>
  <div class='links'>
    <div class='signup'>Sign Up</div>      <!-- This is nested now -->
    <div class='login'>Login</div>         <!-- This one too! -->
  </div>
</div>
```

现在sign up和login是在右边了但是是按照block的默认纵向排列的  
![](https://cdn.liushiming.cn/img/20200130153429.png)

解决办法是把.link也变成一个flexbox  
``` css
.links {
  border: 1px solid #fff;  /* For debugging */
  display: flex;
  justify-content: flex-end;
}

/* login he sign up之间留一点间隙 */
.login {
  margin-left: 20px;
}
```

最后再将用来debug的border移除  

效果  
![](https://cdn.liushiming.cn/img/20200130153923.png)

## 坐标轴调整
横坐标调整用`justify-content` 纵坐标调整用 `align-items`  
![](https://cdn.liushiming.cn/img/20200130160547.png)

`align-items`的对齐方式有  
- center
- flex-start   (top)
- flex-end     (bottom)
- stretch
- baseline

![](https://cdn.liushiming.cn/img/20200130162247.png)

## flex iterms换行
![](https://cdn.liushiming.cn/img/20200130163814.png)

新增5个格子  
``` html
<div class='photo-grid-container'>
  <div class='photo-grid'>
    <div class='photo-grid-item first-item'>
      <img src='images/one.svg'/>
    </div>
    <div class='photo-grid-item'>
      <img src='images/two.svg'/>
    </div>
    <div class='photo-grid-item'>
      <img src='images/three.svg'/>
    </div>
    <div class='photo-grid-item'>
      <img src='images/four.svg'/>
    </div>
    <div class='photo-grid-item'>
      <img src='images/five.svg'/>
    </div>
  </div>
</div>
```

css  
``` css
.photo-grid-container {
  display: flex;
  justify-content: center;
}

.photo-grid {
  width: 900px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.photo-grid-item {
  border: 1px solid #fff;
  width: 300px;
  height: 300px;
}
```

## flex container 方向
“方向”指的是容器是水平还是垂直呈现其项目。到目前为止，我们看到的所有容器都使用默认的水平方向，这意味着项目在同一行中一个接一个地绘制，然后在空间不够时向下一列。
![](https://cdn.liushiming.cn/img/20200130165618.png)

flexbox可以将网格纵向排列，大部分桌面web页面是横向排列，但是手机屏幕一般纵向排列，这在响应式布局里面有很实际的作用  

在.photo-grid里面加上flex-directions:column;即可  
``` css
.photo-grid {
  /* ... */
  flex-direction: column;
}
```

![](https://cdn.liushiming.cn/img/20200130165848.png)


## 校准注意事项
请注意，尽管我们使用了`justify-content:center`，但该列仍然紧紧拥抱其flex容器的左侧;声明。当您旋转容器的方向时，您也会旋转正当性内容属性的方向。它现在指的是容器的垂直对齐，而不是水平对齐。
![](https://cdn.liushiming.cn/img/20200130170110.png)

## flex container order
到目前为止，HTML元素的顺序与在web页面中呈现框的方式之间一直存在紧密的相关性。到目前为止，我们已经看到了浮动和flexbox技术，我们能使一个框在另一个框之前或之后出现的唯一方法是移动底层的HTML标记。这种情况即将改变。
![](https://cdn.liushiming.cn/img/20200130170525.png)


修改css  
``` css
.photo-grid {
  width: 900px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  flex-direction: row-reverse;  /* <--- Really freaking cool! */
  align-items: center;
}
```

这两行现在都呈现为从右到左而不是从左到右。但是，请注意这只是在每行的基础上交换顺序:第一行不是从5开始，而是从3开始。对于许多常见的设计模式来说，这是一种有用的行为(特别是专栏反转为移动布局打开了许多大门)。在下一节中，我们将学习如何变得更细粒度。

![](https://cdn.liushiming.cn/img/20200130170706.png)

从样式表内部重新排序元素是一件大事。在使用flexbox之前，web开发人员不得不求助于JavaScript技巧来完成这类事情。然而，不要滥用你新发现的能力。正如我们在本教程的第一章中所讨论的，您应该始终将内容与表示分开。像这样改变顺序纯粹是为了呈现—如果不应用这些样式，您的HTML仍然是有意义的。  

## flex item 对齐
垂直对齐也是一样的。如果我们想要订阅链接和那些社交图标放在页眉的底部而不是中间呢?使他们单独对齐!这就是align-self属性的用武之地。将其添加到flex项目会覆盖其容器中的align-items值:

``` css
.social,
.subscribe {
  align-self: flex-end;
  margin-bottom: 20px;
}
```

subscribe按钮和社交账号按钮就移下来了  
![](https://cdn.liushiming.cn/img/20200130172011.png)

