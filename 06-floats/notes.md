## 默认垂直样式
html  
``` html
<!DOCTYPE html>
<html lang='en'>
  <head>
    <meta charset='UTF-8' />
    <title>Floats</title>
    <link rel='stylesheet' href='styles.css'/>
  </head>
  <body>
    <div class='page'>
      <div class='menu'>Menu</div>
      <div class='sidebar'>Sidebar</div>
      <div class='content'>Content</div>
      <div class='footer'>Footer</div>
    </div>
  </body>
</html>
```

css  
``` css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.menu {
  height: 100px;
  background-color: #B2D6FF;    /* Medium blue */
}

.sidebar {
  height: 300px;
  background-color: #F09A9D;    /* Red */
}

.content {
  height: 500px;
  background-color: #F5CF8E;    /* Yellow */
}

.footer {
  height: 200px;
  background-color: #D6E9FE;    /* Light blue */
}
```

效果  
![](https://cdn.liushiming.cn/img/20200128134235.png)

## 把sidebar放在侧边栏
想把sidebar放在侧边栏，缩小宽度是没用的，因为div是块级元素  
``` css
.sidebar {
  width: 200px;                 /* Add this */
  height: 300px;
  background-color: #F09A9D;
}
```

效果
![](https://cdn.liushiming.cn/img/20200128140043.png)

## 浮动元素
float属性可以使元素浮动，下面的元素就会往上移  
``` css
.sidebar {
  float: left;                  /* Add this */
  width: 200px;
  height: 300px;
  background-color: #F09A9D;
}
```

效果  
![](https://cdn.liushiming.cn/img/20200128170021.png)

常见的float属性值有以下这些  
``` css
float: right;
float: left;
float: none;
```

float的元素只能浮动在父元素的左边或右边，如果调整page dev的宽度为900px，sidebar就会离开页面边缘和page一起缩进    
``` css
.page {
  width: 900px;
  margin: 0 auto;
}
```

效果  
![](https://cdn.liushiming.cn/img/20200128223517.png)

## 多个浮动元素
将content也浮动
``` css
.content {
  float: left;                  /* Add this */
  width: 650px;
  height: 500px;
  background-color: #F5CF8E;
}
```


多个浮动元素会水平堆放  
![](https://cdn.liushiming.cn/img/20200129001041.png)

给page加一个边框会发现，边框只包含menu和footer，sidebar和content已经溢出边框外了    
``` css
.page {
  width: 900px;
  margin: 0 auto;
  border: 1px solid red;  /* Add this */
}
```

![](https://cdn.liushiming.cn/img/20200129001500.png)

## clear属性
解决以上问题的一个办法是使用`clear`属性，使用了`clear`属性后，footer会移到float的元素下面去。clear属性值有以下几种：
- clear:none; 
- clear:left; /* 以靠左的浮动元素为准 */
- clear:right; /* 以靠右的浮动元素为准 */
- clear:both; /* 靠左或者靠右，那边长就以那边为准 */

所以在footer的css加上`clear:both;`，footer就会移到下面去  
![](https://cdn.liushiming.cn/img/20200129002742.png)

## 优化
把`menu`和`footer`从`page`dev中移出  
``` html
<body>
  <div class='menu'>Menu</div>

  <div class='page'>
    <div class='sidebar'>Sidebar</div>
    <div class='content'>Content</div>
  </div>

  <div class='footer'>Footer</div>
</body>
```

menu和footer宽度占据了整个窗口，效果是我们想要的，但是整个page的边框重叠为一条线了，因为page中的元素都float了，不占高度    
![](https://cdn.liushiming.cn/img/20200129003141.png)

## hiding overflow
使用clear属性只适用于在page中至少有一个非float的元素。page中全部都是float的元素，clear:both的方法就失效了。  

可以使用另一个属性来解决这个问题，即在.page中加上`overflow: hidden;`
![](https://cdn.liushiming.cn/img/20200129003900.png)

在.page加上背景和`overflow`属性 
``` css 
.page {
  width: 900px;
  margin: 0 auto;
  overflow: hidden;             /* Add this */
  background-color: #EAEDF0;    /* Add this */
}
```

效果  
![](https://cdn.liushiming.cn/img/20200129004215.png)

## 全屏背景
现在背景不是全屏，要把背景调整到全屏，但是又要保持.page居中。这是一个矛盾。因为要居中就必须指定width。  

要背景颜色覆盖全屏可以在page外面加一层div，这为我们提供了三层嵌套`div`，`.container`封装全屏背景，固定宽度`.page`使所有元素居中，最后是`.page`中的`.sidebar`和`.content`块。这样的嵌套和对齐方式是大多数网站的典型布局。  
![](https://cdn.liushiming.cn/img/20200129142633.png)
## 等分footer
将`footer`分成三个`div`块  
``` html
<div class='footer'>
  <div class='column'></div>
  <div class='column'></div>
  <div class='column'></div>
</div>
```

指定column的样式(使用百分比宽度)  
``` css
.column {
  float: left;
  width: 31%;
  margin: 20px 1.15%;
  height: 160px;
  background-color: #B2D6FF;    /* Medium blue */
}
```
![](https://cdn.liushiming.cn/img/20200129153754.png)

## 网格
`flotat`也可以设置网格，把footer改为6个column  
``` css
<div class='footer'>
  <div class='column'></div>
  <div class='column'></div>
  <div class='column'></div>
  <div class='column'></div>
  <div class='column'></div>
  <div class='column'></div>
</div>
```

出现了一个问题，新增的一排格子撑破了footer，失去了背景颜色  
![](https://cdn.liushiming.cn/img/20200129155733.png)

这时只需要加上`overflow: hidden;`属性, 并将`height`属性去掉，因为高度需要变成动态  


## floats for content
为content增加一些文字和图片内容  
``` html
<div class='container'>
  <div class='page'>
    <div class='sidebar'></div>
    <div class='content'>
      
      <img src='?' class='article-image'/>

      <p>Ad netus sagittis velit orci est non ut urna taciti metus donec magnis
      hendrerit adipiscing mauris sit a proin ultrices nibh.</p>

      <p>Enim suspendisse ac scelerisque nascetur vestibulum parturient sed mi a
      dolor eu non adipiscing non neque scelerisque netus ullamcorper sed
      parturient integer.Eros dui risus non sodales ullamcorper libero a dis
      cubilia a orci iaculis cursus.</p>

      <p>Egestas at aliquam a egestas accumsan cum elementum consectetur conubia
      tristique eu et vitae condimentum in ante consectetur suscipit a a duis
      vestibulum gravida morbi sagittis.Parturient scelerisque facilisis
      ullamcorper a a pretium a nisl parturient semper senectus accumsan ipsum
      mus scelerisque eget ridiculus.Accumsan dolor a.</p>

      <p>Ligula taciti vel primis sit a tincidunt habitant parturient parturient
      in parturient ante nulla consectetur sem.Facilisis parturient litora.</p>

    </div>
  </div>
</div>
```

给content和image增加属性  
``` css
.content {
  padding: 20px;
}

.article-image {
  float: left;
  width: 300px;
  height: 200px;
  margin-right: 20px;
  margin-bottom: 20px;
}

p {
  margin-bottom: 20px;
}
```



  