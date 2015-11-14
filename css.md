# CSS

####<i class="fa fa-check-square"></i>**语法**
- 用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
- 为选择器分组时，将单独的选择器单独放在一行。
- 为了代码的易读性，在每个声明块的左花括号前添加一个空格。
- 声明块的右花括号应当单独成行。
- 每条声明语句的 : 后应该插入一个空格。
- 为了获得更准确的错误报告，每条声明都应该独占一行。
- 所有声明语句都应当以分号结尾。最后一条声明语句后面的分号是可选的，但是，如果省略这个分号，你的代码可能更易出错。
- 对于以逗号分隔的属性值，每个逗号后面都应该插入一个空格（例如，`box-shadow`）。
- 不要在 `rgb()`、`rgba()`、`hsl()`、`hsla()` 或 `rect()` 值的内部的逗号后面插入空格。这样利于从多个属性值（既加逗号也加空格）中区分多个颜色值（只加逗号，不加空格）。
- 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，`.5` 代替 `0.5`；`-.5px` 代替 `-0.5px`）。
- 十六进制值应该全部小写，例如，#fff。在扫描文档时，小写字符易于分辨，因为他们的形式更易于区分。
- 尽量使用简写形式的十六进制值，例如，用 `#fff` 代替 `#ffffff`。
- 为选择器中的属性添加双引号，例如，`input[type="text"]`。只有在某些情况下是可选的，但是，为了代码的一致性，建议都加上**双引号**。
- 避免为 0 值指定单位，例如，用 `margin: 0`; 代替 `margin: 0px`;。
- 使用**分号结束**单个属性的定义；

>```css
/* 不推荐的写法 */
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin-bottom: 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}
>
/* 推荐的写法 */
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin:0 0 0 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
>}
>```

<br>
####<i class="fa fa-check-square"></i>**声明顺序**
1. Positioning
2. Box model
3. Typographic
4. Visual

>由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

>其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

>```css
declaration-order {
  /* 位置偏移先写 */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;
>
  /* 盒子模型第二 */
  display: block;
  float: right;
  width: 100px;
  height: 100px;
>
  /* 文本样式第三 */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
>
  /* 可视化属性第四 */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;
>
  /* 透明度最后 */
  opacity: 1;
>}
>
>/*也有人不是根据类型来写的,按字母排序的;看习惯了,个人感觉这种比较好阅读*/
>```

<br>
####<i class="fa fa-check-square"></i>**不要使用 `@import`**
>与`<link>`标签相比，@import >指令要慢很多，不光增加了额外的请求次数，还会导致不可预料的问题。替代办法>有以下几种：

>使用多个 `<link>` 元素
>通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件
>通过 Rails、Jekyll 或其他系统中提供过 CSS 文件合并功能
>请参考 Steve Souders 的文章了解更多知识。


>```css
<!-- 推荐使用链接引入css -->
<link rel="stylesheet" href="core.css">
>
<!-- import的性能太低,不如link!不推荐 -->
<style>
  @import url("more.css");
</style>
>```

<br>
####<i class="fa fa-check-square"></i>**媒体查询（Media query）的位置**
>将媒体查询放在尽可能相关规则的附近。不要将他们打包放在一个单一样式文件中或者放在文档底部。如果你把他们分开了，将来只会被大家遗忘。下面给出一个典型的实例。

>```css
element { ... }
.element-avatar { ... }
.element-selected { ... }
>
@media (min-width: 480px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
>```

<br>
####<i class="fa fa-check-square"></i>**属性前缀**
>虽说W3C带头,但是大多浏览器都推出了一些属性的私有特性;
>可以去查询手册,看看哪些需要带前缀的
>这里推荐用[`autoprefixer`](https://github.com/postcss/autoprefixer)来解决


<br>
####<i class="fa fa-check-square"></i>**简写形式的属性声明**
>在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

>- `padding`
>- `margin`
>- `font`
>- `background`
>- `border`
>- `border-radius`
>大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

>MDN（Mozilla Developer Network）上一片非常好的关于[**shorthand properties**](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) 的文章，对于不太熟悉简写属性声明及其行为的用户很有用。


>```css
/* 不推荐的写法 */
>.element {
>  margin: 0 0 10px;
>  background: red;
>  background: url("image.jpg");
>  border-radius: 3px 3px 0 0;
>}
>
/* 推荐的写法 */
>.element {
>  margin-bottom: 10px;
>  background-color: red;
>  background-image: url("image.jpg");
>  border-top-left-radius: 3px;
>  border-top-right-radius: 3px;
>}
>
>/*
就我个人而言,我觉得简写的好处多于分离的
- 减少了执行的条数(因为css是自上而下加载的);
- 减少了代码量,阅读起来方便
>
阅读及书写顺序:
- border,padding,margin是顺时针,上右下左!(这里是指四个参数的时候,三个参数也就是对角作用了,区别不是很大)
- background: 背景色 背景图片 背景是否重复 背景图片位置;
- font: italic(是否斜体)  bold(是否加粗) .8em/1.2(字体大小及行高) Arial, sans-serif(字体种类);
- border-radius 也是顺时针,但是稍微有点差异化,是自左上角到左下角
>
>
>*/
>```

####<i class="fa fa-check-square"></i>**单行规则声明**
>对于只包含一条声明的样式，为了易读性和便于快速编辑，建议将语句放在同一行。对于带有多条声明的样式，还是应当将声明分为多行。
>
>这样做的关键因素是为了错误检测 -- 例如，CSS 校验器指出在 183 >行有语法错误。如果是单行单条声明，你就不会忽略这个错误；如果是单行多条声>明的话，你就要仔细分析避免漏掉错误了。
>
>```css
/* 一条声明的样式单独放在一起 */
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }
>
/* 多条声明的样式应该每条独占一行 */
.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url(../img/sprite.png);
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
>```

<br>
####<i class="fa fa-check-square"></i>**class 命名**
- `class` 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class 的命名（类似于命名空间）（例如，`.btn` 和 `.btn-danger`）。
- 避免过度任意的简写。`.btn` 代表 button，但是 `.s` 不能表达任何意思。
- class 名称应当尽可能短，并且意义明确。
- 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式（presentational）的名称。
- 基于最近的父 `class` 或基本`（base） class` 作为新 class 的前缀。
- 使用 .js-* class 来标识行为（与样式相对），并且不要将这些 class 包含到 CSS 文件中。

>```css
/* 不推荐的写法 */
.t { ... }
.red { ... }
.header { ... }
>
/* 推荐的写法--可以参考bootstrap的命名 */
.btn{ ... }
.btn-sm{ ... }
.btn-danger{ ... }
.tweet { ... }
.important { ... }
.tweet-header { ... }
>```

####<i class="fa fa-check-square"></i>**选择器**
- 对于通用元素使用 `class` ，这样利于渲染性能的优化。
- 对于经常出现的组件，避免使用属性选择器（例如，`[class^="..."]`）。浏览器的性能会受到这些因素的影响。
- 选择器要尽可能短，并且尽量限制组成选择器的元素个数，建议不要超过 3 。
- 只有在必要的时候才将 `class -` 限制在最近的父元素内（也就是后代选择器）（例如，不使用带前缀的 class 时 -- 前缀类似于命名空间）。
- 尽量少使用**后代选择器**和**ID选择器不应该带上关联标签**,会浪费很多资源;
- 命名需要考虑可读性

>```html
> <style type="text/css" media="screen">
>    /*推荐写法*/
>     #container {}
>        .box {}
>
>            .box-tile>h3 {}
>
>            .box-innercontent {}
>
>                .box-innercontent>span {}
>
>    /*不推荐的写法*/
>    div#container {}
>        .box {}
>
>            .box .box-tilte {}
>
>            .box .box-content span {}
>    </style>
>
>    <div id="container">
>        <div class="box">
>        <div class="box-title">
>            <h3></h3>
>        </div>
>        <div class="box-content">
>            <p class="box-innercontent">
>               <span></span>
>               <span></span>
>                <span></span>
>            </p>
>        </div>
>    </div>
>    </div>
>
>```

<br>
####<i class="fa fa-check-square"></i>**尽可能的不用引号，迫不得已时使用单引号.**

>```css
/* 不推荐 */
@import url("//www.google.com/css/maia.css");
>
html {
  font-family: "open sans", arial, sans-serif;
}
>
/* 推荐 */
@import url(//www.google.com/css/maia.css);
>
html {
  font-family: 'open sans', arial, sans-serif;
}
>```

<br>
####<i class="fa fa-check-square"></i>**避免css hack,考虑使用特定浏览器前缀表示；**

>```css
.compact-ie6 p {
    margin: 0;
    *z-index:1;
}
.compact-ie8 .hedaer{};
>```