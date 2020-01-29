## 概述
css选择器可以用来关联特定的html元素，实现对特定元素的样式指定  
![](https://cdn.liushiming.cn/img/20200127175324.png)

到目前为止，我们看到的惟一CSS选择器称为“类型选择器”，它的目标是页面上所有匹配的元素。在本章中，我们将探索使用类选择器、后代选择器、伪类和ID选择器来设计web页面样式的更细粒度的方法。
## class属性
`class`属性可以用在任何html标签上  
``` html
<p class='synopsis'>CSS selectors let you <em>select</em> individual HTML
   elements in an HTML document. This is <strong>super</strong> useful.</p>
```
## 类选择器
类选择使用点号(.)作为前缀  
``` css
.synopsis {
  color: #7E8184;        /* Light gray */
  font-style: italic;
}
```
![](https://cdn.liushiming.cn/img/20200127182409.png)

![](https://cdn.liushiming.cn/img/20200127190716.png)

## div容器
`div`可以在不改变html语义的情况下将布局划分为块状，方便应用不同的样式  
![](https://cdn.liushiming.cn/img/20200127203504.png)

如：将`body`用`div`包起来，指定其class为page，然后对.page应用css样式，指定宽度并居中    
``` html
<body>
  <div class='page'>  <!-- Add this -->
    <h1>CSS Selectors</h1>

    <p  class='synopsis'>CSS selectors let you <em>select</em> individual HTML
    elements in an HTML document. This is <strong>super</strong> useful.</p>

    <p>Classes are ridiculously important, since they allow you to select
    arbitrary boxes in your web pages.</p>

    <p>We’ll also be talking about links in this example, so here’s
    <a href='https://internetingishard.com'>Interneting Is Hard</a> for us to
    style.</p>

    <div class='button'>Button One</div>
  </div>  <!-- And this -->
</body>
```

style.css增加： 
``` css
.page {
  width: 600px;
  margin: 0 auto;
}
```
![](https://cdn.liushiming.cn/img/20200127210709.png)

## 重用class
只要使用同样的class，就可以使用同样的样式  
``` html
<div class='button'>Button One</div>
<div class='button'>Button Two</div>
```
![](https://cdn.liushiming.cn/img/20200127210912.png)

如果希望第二个button和第一个稍微有区别，可以给第二个button加上一个新的class，用空格隔开
``` html
<div class='button call-to-action'>Button Two</div>
```
对应的css为新的class指定样式  
``` css
.call-to-action {
  font-style: italic;
  background-color: #EEB75A;    /* Yellow */
}
```
![](https://cdn.liushiming.cn/img/20200127211036.png)

## class的先后顺序
因为`call-to-action`在`button`后面所以`call-to-action`的样式将覆盖`button`的样式  
``` html
<div class='button call-to-action'>Button Two</div>
```

## 后代选择器
因为.synopsis样式为斜体，`em`默认样式也是斜体，所以`<em>select</em>`显示不出特殊性  
``` html

        <p class='synopsis'>CSS selectors let you <em>select</em> individual HTML
            elements in an HTML document. This is <strong>super</strong> useful.</p>
```

如果想单独改变这个段落里的`em`的样式，可以为它加一个class，但是没必要这么做，可以使用后代选择器  
``` css
.synopsis em {
  font-style: normal;
}
```

![](https://cdn.liushiming.cn/img/20200127212600.png)  

## 不要嵌套太多层
后代选择器不宜嵌套太多层，因为可重用性和可维护性都不好  
``` css
/* Try to avoid this */
.article h2 .subheading em {
  /* Special styles */
}
```

## 伪类选择器
伪类选择器可以指定用户行为带来的样式变化  
![](https://cdn.liushiming.cn/img/20200127214545.png)

最常见的伪类是链接的悬停、点击状态  
- :link – 未被访问
- :visited – 被访问过
- :hover – 鼠标悬停
- :active – 点击


``` css
a:link {
  color: blue;
  text-decoration: none;
}
a:visited {
  color: purple;
}
a:hover {
  color: aqua;
  text-decoration: underline;
}
a:active {
  color: red;
}
```

## 已访问悬停状态
可以为已访问的链接单独设置悬停样式  
``` css
a:visited:hover {
  color: orange;
}
```

如此，已访问的链接悬停会变为橙色。但是会引发一个问题`a:active`的样式会失效  

为了解决这个问题，可以设置已访问点击样式  
``` css
a:visited:active {
  color: red;
}
```

## 按钮伪类选择器
伪类选择器不只是为超链接服务的，它可以用在任何选择器上  

举例，用在`.button`类上

首先需要将按钮的`div`标签改为`<a href>`标签  
``` html
<a class='button' href='nowhere.html'>Button One</a>
<a class='button call-to-action' href='nowhere.html'>Button Two</a>
```

改完后会发现，按钮的某些样式失效了  
![](https://cdn.liushiming.cn/img/20200127221328.png)

因为`<a>`是行级元素并且有默认的`color`样式。我们需要将它改为块级元素并移除掉一些默认的超链接的样式，将之前的button样式改为  
``` css
.button:link,                 /* Change this */
.button:visited {             /* Change this */
  display: block;             /* Add this */
  text-decoration: none;      /* Add this */
  color: #FFF
}
```  

注意选择器中新的:link和:visited伪类。没有它，我们的`color`将不会覆盖浏览器的默认a:链接样式。

## id选择器
只要html中给标签写上id属性，css就可以选中标签设定样式  
``` html
<a id='button-2' class='button' href='nowhere.html'>Button Two</a>
```

id选择器使用`#`号  
``` css
#button-2 {
  color: #5D6063;  /* Dark gray */
}
```

因为id选择器可复用性不好，所以尽量少用  

## url片段
网页中的超链接可以跳转到外部也可以跳转到同一页面的片段上，url片段参数用`#`号和`path`区分，放在最后  
![](https://cdn.liushiming.cn/img/20200127231254.png)

html超链接写法  
``` html
<!-- From the same page -->
<a href='#button-2'>Go to Button Two</a>

<!-- From a different page -->
<a href='selectors.html#button-2'>Go to Button Two</a>
```

因为`id`属性被同时用在url跳转和css样式上，所以如果为了修改跳转链接而修改了id，css样式没有跟着改，网站就会被搞乱。因此，不建议使用id选择器。  
![](https://cdn.liushiming.cn/img/20200127231832.png)

## css的特异性
id选择器的优先级大于类选择器  
如果都是类选择，按顺序，后面覆盖前面的
![](https://cdn.liushiming.cn/img/20200127235038.png)

如果中间有id选择器，则id选择器之后的类选择器不生效  
![](https://cdn.liushiming.cn/img/20200127235052.png)

