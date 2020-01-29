## basic web pages
``` html
<!DOCTYPE html>
<html>
  <head>
    <title>Interneting Is Easy!</title>
    <meta charset='UTF-8'/>
    <!-- Metadata goes here -->
  </head>
  <body>
    <h1>Interneting Is Easy!</h1>
    <p>First, we need to learn some basic HTML.</p>
    <!-- Content goes here -->
    <h2>Headings</h2>
    <p>Headings define the outline of your site. There are six levels of headings.</p>
    <p>This is what an unordered list looks like:</p>
    <ul>
      <li>Add a "ul" element (it stands for unordered list)</li>
      <li>Add each item in its own "li" element</li>
      <li>They don't need to be in any particular order</li>
    </ul>
    
    <p>This is what an ordered list looks like:</p>
    <ol>
      <li>Notice the new "ol" element wrapping everything</li>
      <li>But, the list item elements are the same</li>
      <li>Also note how the numbers increment on their own</li>
      <li>You should be noticing things is this precise order, because this is an ordered list</li>
    </ol>
    <h2>Inline Elements</h2>
    <p><em>Sometimes</em>, you need to draw attention to a particular word or phrase.</p>
    <p>Other times you need to <strong>strong</strong>ly emphasize the importance of a word or phrase.</p>
  </body>
    <p><em><strong>And sometimes you need to shout!</strong></em></p>
    <h2>Empty Elements</h2>

    <p>Thanks for reading! Interneting should be getting easier now.</p>

    <p>Regards,
    The Authors</p>
    <p>Regards,<br/>
        The Authors</p>
    <hr/>

    <p>P.S. This page might look like crap, but we'll fix that with some CSS
    soon.</p>
</html>
```
`<!DOCTYPE html>` - 告诉浏览器这是一个html5的页面
`<html>` - 整个浏览器被html标签包裹，<html>是一个open tag
`</html>` - <html>标签的close tag
`<head>` - 一个web页面的头部包含它的所有元数据，比如页面标题、CSS样式表以及呈现页面所需的其他内容，但是您不一定希望用户看到这些内容。
`<meta>` - 元数据, charset属性描述网页的字符集。
`<body>` - 网页中可见的部分
`<!--  -->` - 注释
`<title>` - 网页标题（将显示到浏览器tab页上）
`<p>` - 正文中的段落
`<h1>` - 一号标题
`<h2>` - 二号标题，诸如此类一共有6号标题
`<ul>` - unordered list，无顺序列表
`<li>` - list item，列表内容
`<ol>` - ordered list，有顺序列表
`<em>` - 斜体字，`em` tag包围的文字将斜体展示，表示强调，em stands for emphasis。
`<strong>` - 加粗，`strong` tag包围的文字将加粗显示，表示比`em`更强一级的强调。
`<em><strong>` - 加斜并加粗，表示最强的强调。
>为什么使用`emphasis`和`strong`而不是`italic`和`bold`，因为html只负责网页的骨架，网页的显示样式由css决定。
>![](https://cdn.liushiming.cn/img/20200119134721.png)

`<br/>` - 换行符。`br`是空html元素。如果不加换行符，在`p`tag中敲enter换行是行不通的，html解析的时候会将这样的换行解析为空格。
`<hr/>` - 水平线。`hr` stands for horizontal rule。

不要滥用`<br/>`,`<hr/>`，它们必须有含义。如果加一条分割线只是因为美学原因，可以用css的`border`属性来实现。
`<br/>`,`<hr/>`与`<br>`,`<hr>`是等效的，但是为自己方便，最好始终选择一种写法。




