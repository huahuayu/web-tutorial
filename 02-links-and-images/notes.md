## links
- Links are created with the <a> element, which stands for “anchor”.

## 链接类型
### 绝对路径链接
``` html
<li>Absolute links, like to
    <a href='https://developer.mozilla.org/en-US/docs/Web/HTML'>Mozilla
    Developer Network</a>, which is a very good resource for web
    developers.
</li>
![](https://cdn.liushiming.cn/img/20200119171201.png)
```
### 相对路径
``` html
<li>Relative links, like to our <a href='misc/extras.html'>extras
    page</a>.
</li>
```
![](https://cdn.liushiming.cn/img/20200119171212.png)

### 上一层级路径
``` html
<p>This page is about miscellaneous HTML things, but you may also be
   interested in <a href='../links.html'>links</a> or <a
   href='../images.html'>images</a>.</p>
```
![](https://cdn.liushiming.cn/img/20200119171134.png)

### 回到首页
``` html
<li>Root-relative links, like to the <a href='/'>home page</a> of our website,
    but those aren't useful to us right now.</li>
```

## 命名方式
html文件的名字中不要带有空格(CSS files, JavaScript files, and images都一样)，`spaces are bad.html` 带有空格的文件，空格将以`%20`代替，`links-and-images/spaces%20are%20bad.html`

## 图片
使用`img`tag定义图片，`src`属性定义图片的地址，`width`定义宽度，`height`定义高度。
如果只定义宽度或高度，图片会按比例放大缩小，同时定义宽度和高度会按定义的展示。高度和宽度后面不用加单位，默认是`px`.
`alt`定义图片描述，这对搜索引擎和text-only浏览器会有用，alt stands for alternate text。
``` html
    <img src='images/mochi.png'  width='75' height="75"  alt='A mochi ball'/>
```

## html保留字
单引号、双引号、左尖括号、右尖括号、&符号在html中都需要转义
&lt; - less then, <
&gt; - great then, >
&amp; - ampersand symbols, &
&ldquo; - left double quote
&rdquo; - right double quote
&lsquo; - left single quote
&rsquo; - right single quote

转义字符对照表：https://tool.oschina.net/commons?type=2