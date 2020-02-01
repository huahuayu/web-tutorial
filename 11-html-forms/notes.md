## 概述
HTML表单元素让您收集来自网站访问者的输入。邮件列表、联系表单和博客文章评论是小型网站的常见例子，但在依靠网站获得收入的组织中，表单是非常重要的。  
![](https://cdn.liushiming.cn/img/20200131175330.png)  

表单是“赚钱的页面”。它们是电子商务网站销售产品的方式，SaaS公司收取服务费用的方式，以及非盈利组织在网上筹集资金的方式。许多公司通过表单的有效性来衡量网站的成功，因为他们会回答这样的问题:“我们的网站给我们的销售团队送了多少条线索?”和“上周有多少人注册了我们的产品?”这通常意味着表单要经受无休止的A/B测试和优化。

![](https://cdn.liushiming.cn/img/20200131175449.png)

一个功能性的HTML表单有两个方面:前端用户界面和后端服务器。前者是表单的外观(由HTML和CSS定义)，而后者是处理表单的代码(在数据库中存储数据、发送电子邮件等)。我们将完全集中在这一章的前端，而把后端表单处理留到以后的教程中讨论。

## 要实现的表单
![](https://cdn.liushiming.cn/img/20200131175612.png)

html  
``` html
<!DOCTYPE html>
<html lang='en'>
  <head>
    <meta charset='UTF-8'/>
    <title>Speaker Submission</title>
    <link rel='stylesheet' href='styles.css'/>
  </head>
  <body>
    <header class='speaker-form-header'>
      <h1>Speaker Submission</h1>
      <p><em>Want to speak at our fake conference? Fill out
        this form.</em></p>
    </header>
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

body {
  color: #5D6063;
  background-color: #EAEDF0;
  font-family: "Helvetica", "Arial", sans-serif;
  font-size: 16px;
  line-height: 1.3;

  display: flex;
  flex-direction: column;
  align-items: center;
}

.speaker-form-header {
  text-align: center;
  background-color: #F6F7F8;
  border: 1px solid #D6D9DC;
  border-radius: 3px;
  
  width: 80%;
  margin: 40px 0;
  padding: 50px;
}

.speaker-form-header h1 {
  font-size: 30px;
  margin-bottom: 20px;
}
```

## html forms
每个HTML表单都以`form`元素开始。它接受许多属性，但最重要的是`action`和`method`  
``` html
<form action='' method='get' class='speaker-form'>
</form>
```

action属性定义了处理表单的URL。当用户单击Submit按钮时，表单收集的输入将发送到这里。这通常是web服务器定义的一个特殊URL，它知道如何处理数据。  
![](https://cdn.liushiming.cn/img/20200201161408.png)

方法属性可以是post或get，两者都定义了如何将表单提交到后端服务器。这在很大程度上取决于web服务器处理表单的方式，但是一般的经验法则是在服务器上更改数据时使用post，而在只获取数据时保留get。

通过将action属性留空，我们告诉表单提交到相同的URL。结合get方法，我们将检查表单的内容。

## form格式化
``` css
.speaker-form {
  background-color: #F6F7F8;
  border: 1px solid #D6D9DC;
  border-radius: 3px;
  
  width: 80%;
  padding: 50px;
  margin: 0 0 40px 0;
}
```

## text input

``` html
        <form action='' method='get' class='speaker-form'>
            <div class='form-row'>
                <label for='full-name'>Name</label>
                <input id='full-name' name='full-name' type='text' value='Shiming' />
            </div>
        </form>
```

![](https://cdn.liushiming.cn/img/20200201161950.png)

![](https://cdn.liushiming.cn/img/20200201162009.png)

## 格式化text input字段
``` css
.form-row {
  margin-bottom: 40px;
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
  flex-wrap: wrap;
}

.form-row input[type='text'] {
  background-color: #FFFFFF;
  border: 1px solid #D6D9DC;
  border-radius: 3px;
  width: 100%;
  padding: 7px;
  font-size: 14px;
}

.form-row label {
  margin-bottom: 15px;
}
```

其中`input[type='text'] `是属性选择器，只选择`<input/>`标签且有一个`type`为text的元素  
``` css
.form-row input[type='text'] {
  background-color: #FFFFFF;
  border: 1px solid #D6D9DC;
  border-radius: 3px;
  width: 100%;
  padding: 7px;
  font-size: 14px;
}
```

## 响应式css
desktop样式  
``` css
@media only screen and (min-width: 700px) {
  .speaker-form-header,
  .speaker-form {
    width: 600px;
  }
  .form-row {
    flex-direction: row;
    align-items: flex-start; /* To avoid stretching */
    margin-bottom: 20px;
  }
  .form-row input[type='text'] {
    width: 250px;
    height: initial;
  }
  .form-row label {
    text-align: right;
    width: 120px;
    margin-top: 7px;
    padding-right: 20px;
  }
}
```

## email input fields
html  
``` html
<div class='form-row'>
  <label for='email'>Email</label>
  <input id='email'
         name='email'
         type='email'
         placeholder='joe@example.com'/>
</div>
```

css  
``` css
.form-row input[type='text'],
.form-row input[type='email'] {
  background-color: #FFFFFF;
  /* ... */
}

@media only screen and (min-width: 700px) {
  /* ... */
  .form-row input[type='text'],
  .form-row input[type='email'],    /* Add */
  .form-row select,                 /* These */
  .form-row textarea {              /* Selectors */
    width: 250px;
    height: initial;
  }
  /* ... */
}

.form-row input[type='text']:invalid,
.form-row input[type='email']:invalid {
  border: 1px solid #D55C5F;
  color: #D55C5F;
  box-shadow: none; /* Remove default red glow in Firefox */
}
```

校验效果  
![](https://cdn.liushiming.cn/img/20200201174057.png)

## 单选按钮
![](https://cdn.liushiming.cn/img/20200201174118.png)  

html  
``` html
<fieldset class='legacy-form-row'>
  <legend>Type of Talk</legend>
  <input id='talk-type-1'
         name='talk-type'
         type='radio'
         value='main-stage' />
  <label for='talk-type-1' class='radio-label'>Main Stage</label>
  <input id='talk-type-2'
         name='talk-type'
         type='radio'
         value='workshop'
         checked />
  <label for='talk-type-2' class='radio-label'>Workshop</label>
</fieldset>
```

响应式样式  
![](https://cdn.liushiming.cn/img/20200201174255.png)


## 下拉选单
``` html
<div class='form-row'>
  <label for='t-shirt'>T-Shirt Size</label>
  <select id='t-shirt' name='t-shirt'>
    <option value='xs'>Extra Small</option>
    <option value='s'>Small</option>
    <option value='m'>Medium</option>
    <option value='l'>Large</option>
  </select>
</div>
```