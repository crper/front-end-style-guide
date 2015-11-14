<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css">

# HTML5

####<i class="fa fa-check-square"></i>**文档类型必须指明**
```html
<!--不写这个，浏览器无法识别html5的标签-->

<!DOCTYPE html>
```
<br>
####<i class="fa fa-check-square"></i>**字符编码设置**
```html
<!--保证各种浏览器下正常展示-->

<meta charset="UTF-8">
```
<br>

####<i class="fa fa-check-square"></i>**要顾及移动设备**
```html
<!--调用IE的最新内核而非兼容模式，chrome调用最新内核-->
<!--网站通过viewport缩放到设备宽高展示-->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

####<i class="fa fa-check-square"></i>**不要再DIV全家桶了**
```html
<!--
    传统的布局，都是DIV全家桶，各种DIV模拟和嵌套；
    H5带来更多的标签，在某些区域可以使用这些标签表示；
    让代码结构更加语义化
-->

<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="//xxx.com/default.css">
</head>

<body>
    <header id="header" class="">
        <nav>
            <ul>
                <li><a href="" title=""></a></li>
            </ul>
        </nav><!--可以用于导航包裹层-->
    </header><!--可以用来表示网站的头部 -->
    <section>

    </section><!--可以用来写段落，区域块-->
    <article>

    </article><!--用来写文章居多-->
    <footer>

    </footer><!--可以用来表示网站的尾部-->
</body>
</html>

```

<br>

####<i class="fa fa-check-square"></i>**多用表单控件内置属性**
>若是针对的用户群是追新一族（最新浏览器，或者移动端（非android4.4以下或者IOS9以下的）），
>可以任性的使用这些h5的新特性；大大减少了对JS的依赖（比如一些功能需要用js实现的，表单验证！！
>，取色器,日期等==）

```html
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="//xxx.com/default.css">
</head>

<body>
    <form action="1_submit" method="get" accept-charset="utf-8">
        <!--原生验证，必填项 required -->
        <input type="text" required>

        <!--原生验证，正则匹配 pattern ,这里匹配手机号码-->
        <input type="text" pattern="^1[34578][0-9]\d{8}" title="请输入您的手机号码！">

        <!--原生验证，范围输入 range 和number很类似 -->
        <input type="range" min="0" max="100" step="5">

        <!--原生验证，邮箱验证 ,会判断是否有@，和域名后缀 -->
        <input type="email">

        <!--url 原生支持，不用通过js判断了-->
        <input type="url">

        <!--原生日期支持，可以减少JS的依赖了；年月日都支持，具体可以搜索相关资料，就是浏览器支持的不多-->
        <input type="date">
        <input type="time">
        <input type="datetime">
        <input type="month">
        <input type="week">
        <input type="datetime-local">

        <!--还有取色器，及提到另外表单===-->
        更多的可以看下我的两篇简述的博文
        <a href="http://blog.csdn.net/crper/article/details/47925843">HTML5基础知识汇总_(1)标签结构上的整改</a>
        <a href="http://blog.csdn.net/crper/article/details/47971225">HTML5基础知识汇总_(2)自定义属性及表单新特性</a>
    </form>
</body>

</html>

```
