# HTML通用规范


####<i class="fa fa-check-square"></i>**通用条例**
- <i class="fa fa-check-circle"></i>用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
- <i class="fa fa-check-circle"></i>嵌套元素应当缩进一次（即两个空格）。
- <i class="fa fa-check-circle"></i>对于属性的定义，确保全部使用双引号，绝不要使用单引号。
- <i class="fa fa-check-circle"></i>启用最新模式（IE和chrome）
- <i class="fa fa-check-circle"></i>减少标签的数量,任何时候都要尽量使用最少的标签并保持最小的复杂度。
- <i class="fa fa-check-circle"></i>考虑移动设备要添加`viewport`
- <i class="fa fa-check-circle"></i>设置默认的字符编码为`utf-8`,保证浏览器的解析正确
- <i class="fa fa-check-circle"></i>不使用**行内样式**，需要谨记样式，结构，行为分离为基础
- <i class="fa fa-check-circle"></i>**段落分隔符**要使用实际对应的`<p>`元素，而不是用多个`<br>`标签。
- <i class="fa fa-check-circle"></i>在合适的条件下，充分利用`<dl>`（定义列表）和`<blockquote>`标签。
- <i class="fa fa-check-circle"></i>列表中的条目必须总是放置于`<ul>`、`<ol>`或`<dl>`中，永远不要用一组`<div>`或`<p>`来表示。
- <i class="fa fa-check-circle"></i>注释要适当，不多不少，太多造成阅读障碍【模块或者一块区域推荐注释，一两行的不推荐】
- <i class="fa fa-check-circle"></i>对于引用库的，推荐使用CDN，但是需要考虑到区域（比如国内的CDN，国外访问不友好；反之也一样）
- <i class="fa fa-check-circle"></i>若是用户群比较广泛，考虑残疾人，应该使用`aria-`和`role`来帮助他们更好的理解网页
- <i class="fa fa-check-circle"></i>文档设置`lang`
  >有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等
- <i class="fa fa-check-circle"></i>属性顺序
 >- `class`
 >- `id`, `name`
 >- `data-*`
 >- `src`, `for`, `type`, `href`
 >- `title`, `alt`
 >- `aria-*`, `role`
- <i class="fa fa-check-circle"></i>引入文件推荐协议判断,会根据当前站点的协议来请求文件，可以避免[Mixed Content](https://developer.mozilla.org/en-US/docs/Web/CSS/@charset)问题
>```html
><!-- 不推荐 -->
><script src="http://xxx.com/xx.js"></script>
><!-- 推荐 -->
><script src="//xxx.com/xx.js"></script>
>
><!-- 不推荐 -->
><link rel="stylesheet" href="http://xxx.com/default.css" type="text/css">
>
><!-- 推荐: html4/xhtml需要带上`type="text/css"` -->
><link rel="stylesheet" href="//xxx.com/default.css">
>
>/* 不推荐 */
>.test {
>  background: url(http://xxx.com/xx.css);
>}
>/* 推荐 */
>.test {
>  background: url(//xxx.com/xx.css);
>}
>
>
>//已经问题，如果在**IE7**，**IE8**中使用`<link>`和 `@import` 引入 CSS >的时候，会下载两次 CSS 文件。
>```


<br>
####<i class="fa fa-check-square"></i>**标准demo-h5**
>```html
><!DOCTYPE html>
><html lang="zh-CN">
>
><head>
>    <meta charset="UTF-8">
>    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
>    <meta name="viewport" content="width=device-width, user-scalable=no, >initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
>    <title>Document</title>
>    <link rel="stylesheet" href="//xxx.com/default.css">
></head>
>
><body>
>    <!--
>    最小复杂度例子,就一个评论行
>    img可以通过浮动和margin拉出去到左边，h3和p各自独占一行，文字对齐即可
>    -->
>    <div class="comment">
>        <img src="text.png" alt="我的头像">
>        <h3>木木</h3>
>        <p>你必须非常努力，才能看起来毫不费力！！</p>
>    </div>
>    
>    
>    <!--
>    多余元素的例子
>    这里的思想就是两个DIV包裹，一个左浮动，一个右浮动；达到了上面同样的效>果；却增加了两个包裹块（多余）
>    -->
>    <div class="comment">
>        <div class="avator">
>            <img src="text.png" alt="我的头像">
>        </div>
>        <div class="descr">
>            <h3>木木</h3>
>            <p>你必须非常努力，才能看起来毫不费力！！</p>
>        </div>
>    </div>
>
>    <!--
>    元素顺序
>    XHTML需要单闭合标签，这里用HTML5
>    -->
>    <form action="1_submit" method="get" accept-charset="utf-8">
>        <input type="text" class="input-name" id="username" >name="username" data-value="mumu" aria-hidden="true"  >role="tooltip" >
>        <img src="//xxx.jpg"  alt="demo">
>    </form>
>
>    <script src="/javascripts/application.js" type="text/javascript" charset="utf-8" async defer></script>
></body>
></html>

>```
