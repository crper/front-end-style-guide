#XHTML

####<i class="fa fa-check-square"></i>**XHTML 1.0 的三种 XML 文档类型**
- XHTML 1.0 Strict

```html
<!--在此情况下使用：需要干净的标记，避免表现上的混乱。请与层叠样式表配合使用。-->

<!DOCTYPE html
PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

```
- XHTML 1.0 Transitional

```html
<!--在此情况下使用：当需要利用 HTML 在表现上的特性时，并且当需要为那些不支持层叠样式表的浏览器编写 XHTML 时。-->

<!DOCTYPE html
PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```
- XHTML 1.0 Frameset

```html
<!--在此的情况下使用：需要使用HTML框架将浏览器窗口分割为两部分或更多框架时。-->

<!DOCTYPE html
PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

<br>

####<i class="fa fa-check-square"></i>**所有的XML标记都必须合理嵌套（合理不是强制，虽然奇葩的写法，浏览器有些也能解析！！）**

```html
<!--推荐-->
<div>
    <h1></h1>
    <p>
        <span></span>
    </p>
</div>

<!--不推荐-->
<div>
    <h1></h1>
    <span>
        <p></p>
    </span>
</div>

```
<br>
####<i class="fa fa-check-square"></i>**所有的标记都必须要有一个相应的结束标记**

```html
<!--推荐写法-->
<!--表单控件也需要用反斜杆闭合标签，还有一些单闭合标签`<br/>`,<hr/>`-->
<div class="wrapper">
    <form action="1_submit" method="get" accept-charset="utf-8">
        <input type="text" />
    </form>
</div>

```
<br>
#####<i class="fa fa-check-square"></i>**所有标签的元素和属性的名字都必须使用小写**
>XHTML中对大小写敏感，`<p>`和`<P>`,`<BODY>`和`<body>`是完全不同的标签！！！

<br>
####<i class="fa fa-check-square"></i>**属性必须赋值且带上双引号**
>XHTML规定所有属性都必须有一个值，没有值的就重复本身。

```html
<!--推荐-->
<div class="wrapper">
    <form action="1_submit" method="get" accept-charset="utf-8">
        <input type="text" checked="checked" name="username" />
    </form>
</div>

<!--不推荐 --- H5中可以这样写-->
<div class="wrapper">
    <form action="1_submit" method="get" accept-charset="utf-8">
        <input type="text" name=""  checked>
    </form>
</div>


```
<br>
####<i class="fa fa-check-square"></i>**不要在注释内容中使`--`**

```html
  “--”只能发生在XHTML注释的开头和结束，也就是说，在内容中它们不再有效。例如下面的代码是无效的:     

 <!--这里是注释-----------这里是注释--> 
  用等号或者空格替换内部的虚线。  


 <!--这里是注释============这里是注释--> 
```

<br>
####<i class="fa fa-check-square"></i>**对于图片需添加alt属性**

```html
<!--推荐-->
<img src="" alt="">

<!--不推荐-->
<img src="" >
```
<br>

####<i class="fa fa-check-square"></i>**冲突符号用HTML实体表示**
>比如：
>- `>` 用 `&gt;`
>- `<` 用 `&lt;`
>- `x` 用 `&times;`
>- `&` 用 `&amp;` <br>
>HTML实体很多，这里就不一一列举了，有兴趣的引擎一搜就一堆了
