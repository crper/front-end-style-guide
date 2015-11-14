# jQuery编码规范及优化

####<i class="fa fa-check-square"></i>**关于变量及选择器**
1. 关于变量,使用jquery选择器赋值的变量应该加上`$`前缀; eg:`var $_t = $(this)`

2. 尽量`ID`选择器。实际运用的是js的`document.getElementById()`，所以速度较其他选择器快。

3. 使用类选择器时表指定元素的类型。请看[性能比较](http://jsperf.com/jqeury-selector-test)
>```js
var $products = $("div.products"); // 慢
var $products = $(".products"); // 快
```

4. ID父亲容器下面查找子元素请用`.find()`方法。这样做快的原因是通过id选择元素不会使用Sizzle引擎。[详情看这里](http://learn.jquery.com/performance/optimize-selectors/)
>```js
>// BAD, a nested query for Sizzle selector engine
>var $productIds = $("#products div.id");
>
>// GOOD, #products is already selected by document.getElementById() so >only div.id needs to go through Sizzle selector engine
>var $productIds = $("#products").find("div.id");
```

5. 多级查找中，右边尽量指定得详细点而左边则尽量简单点。[了解更多](http://learn.jquery.com/performance/optimize-selectors/)
>```js
// 丑陋
>$("div.data .gonzalez");
>
>// 优化后
>$(".data td.gonzalez");
```

6. 避免冗余。详情或者查看[性能比较](http://jsperf.com/avoid-excessive-specificity)
>```js
>$(".data table.attendees td.gonzalez");
>
>// 好的方式：去掉了中间的冗余
>$(".data td.gonzalez");
```

7. 指定选择的上下文。
>```js
>
>// 劣质的代码：因为需要遍历整个DOM来找到.class
>$('.class');
>
>// 高品代码：因为只需在指定容器范围内进行查找
>$('.class', '#class-container');
```

8. 避免使用万能选择器。查看[具体阐释](http://learn.jquery.com/performance/optimize-selectors/)
>```js
>$('div.container > *'); // 差
>$('div.container').children(); // 棒
```

9. 警惕隐式的万能选择器。省略的情况下其实使用的就是`*`号通配符。更多信息
>```js
>$('div.someclass :radio'); // 差
>$('div.someclass input:radio'); // 棒
```
10. ID已经表示唯一了，背后使用的是`document.getElementById()`，所以不要和其他选择器混淆了。
>```js
>$('#outer #inner'); // 脏
>$('div#inner'); // 乱
>$('.outer-container #inner'); // 差
>$('#inner'); // 干净利落，后台只需调用document.getElementById()
```

<br>
####<i class="fa fa-check-square"></i>**DOM操作**

1. 操作任何元素前先将其从文档卸载，然后再贴回去。[请看](http://learn.jquery.com/performance/detach-elements-before-work-with-them/)
>```js
>var $myList = $("#list-container > ul").detach();
>//...a lot of complicated things on $myList
>$myList.appendTo("#list-container");
```

2. 使用连接字符串或数组join()，然后再append()。请看
>性能比较: http://jsperf.com/jquery-append-vs-string-concat
>```js
>// 不好
>var $myList = $("#list");
>for(var i = 0; i < 10000; i++){
>    $myList.append("<li>"+i+"</li>");
>}
>
>// GOOD
>var $myList = $("#list");
>for(var i = 0; i < 10000; i++){
>    list += "<li>"+i+"</li>";
>}
>$myList.html(list);
>
>// EVEN FASTER
>var array = []; 
>for(var i = 0; i < 10000; i++){
>    array[i] = "<li>"+i+"</li>"; 
>}
>$myList.html(array.join(''));
```

3. 不要用缺失的元素，[具体请看](http://learn.jquery.com/performance/dont-act-on-absent-elements/)
>```js
>// BAD: This runs three functions before it realizes there's nothing in >the selection
>$("#nosuchthing").slideUp();
>
>// GOOD
>var $mySelection = $("#nosuchthing");
>if ($mySelection.length) {
>    $mySelection.slideUp();
>}
```

<br>
####<i class="fa fa-check-square"></i>**事件**

1. 一个页面只写一个文档ready事件的处理程序。这样代码既清晰好调试，又容易跟踪代码的进程。

2. 不要用匿名函数来做事件的回调。匿名函数不易调试维护测试和复用。
>```js
>$("#myLink").on("click", function(){...}); // 不要这样
>
>
>
>// 这样
>function myLinkClickHandler(){...}
>$("#myLink").on("click", myLinkClickHandler);
```

3. 处理文档`ready事件`的回调也表用匿名函数，匿名函数不易调试维护测试和复用
>```js
>$(function(){ ... }); // 糟糕的做法：无法利用此函数也无法为其写测试用例
>
>// 好的做法
>$(initPage); // 抑或 $(document).ready(initPage);
>function initPage(){
>    // 这里你可以进行程序的初始化了
>}
```

4. 进一步，最好也将ready事件的处理程序放到外部文件中引入到页面，而页面中内嵌的代码只需调用即可。
>```js
><script src="my-document-ready.js"></script>
><script>
>    // 初始化一些必要的全局变量
>    $(document).ready(initPage); // 抑或 $(initPage);
></script>
```

5. 千万表写内联到HTML的JS代码，这是调试的噩梦！应该总是用jQuery来绑定事件自带程序，这样也方便随时动态地取消绑定。
>```js
><a id="myLink" href="#" onclick="myEventHandler();">my link</a> <!--不好 >-->
>
>$("#myLink").on("click", myEventHandler); // GOOD
```
6. 如果可能尽量在绑定事件处理程序时使用一个命名空间，这样可以方便地取消绑定而不会影响其他绑定。
>```js
$("#myLink").on("click.mySpecialClick", myEventHandler); // 不错
// 之后，让我们优雅地解除绑定
$("#myLink").unbind("click.mySpecialClick");
```

7. 当选择某个元素的子元素的时候，尽量在后面选择，不要在前面选择其中选择。如下：
>```js
$("#list a").on("click", myClickHandler); // BAD, you are attaching an event to all the links under the list.
$("#list").on("click", "a", myClickHandler); // GOOD, only one event handler is attached to the parent.
```


####<i class="fa fa-check-square"></i>**Ajax异步操作**

1. 不要用`.getJson()`或`.get()`,直接用直接用`$.ajax()` ，因为jQuery内部还是将前者转化为`$.ajax()`

2. 表对HTTPS站点使用HTTP去发起请求，最好干脆就表指定（将HTTP或者HTTPS从你的URL中移除）

3. 表在链接里面嵌参数，请使用专门的参数设置来传递
>```js
>// 不易阅读的代码...
>$.ajax({
>    url: "something.php?param1=test1&param2=test2",
>    ....
>});
>
>// 更易阅读...
>$.ajax({
>    url: "something.php",
>    data: { param1: test1, param2: test2 }
>});
```

4. 尽量指明数据类型以便你自己清楚要处理什么样的数据（见下方会提到的Ajax模板）

5. 对于异步动态加载的内容，最好使用代理来绑定事件处理程序。这样的好处是对于之后动态加载的元素事件同样有效。[了解更多](http://api.jquery.com/on/#direct-and-delegated-events)
>```js
$("#parent-container").on("click", "a", delegatedClickHandlerForAjax);
```

6. 使用Promise模式。[更多例子](http://www.htmlgoodies.com/beyond/javascript/making-promises-with-jquery-deferred.html)
>```js
$.ajax({ ... }).then(successHandler, failureHandler);
>
>
>
>// 抑或
var jqxhr = $.ajax({ ... });
jqxhr.done(successHandler);
jqxhr.fail(failureHandler);
```

7. 标准的Ajax模板如下，查看[官方案例](https://api.jquery.com/jQuery.ajax/)
>```js
var jqxhr = $.ajax({
    url: url,
    type: "GET", // 默认为GET,你可以根据需要更改
    cache: true, // 默认为true,但对于script,jsonp类型为false,可以自行设置
    data: {}, // 将请求参数放这里.
    dataType: "json", // 指定想要的数据类型
    jsonp: "callback", // 指定回调处理JSONP类型的请求
    statusCode: { // 如果你想处理各状态的错误的话
        404: handler404,
        500: handler500
    }
});
jqxhr.done(successHandler);
jqxhr.fail(failureHandler);
```

<br>
####<i class="fa fa-check-square"></i>**动画与特效**

>**对于当前来说,不建议使用jquery的`animate`,因为很慢,移动端更严重,<br>可以考虑使用`velocity.js`来替换jquery `animate`的实现**

1. 保持一个始终如一风格统一的动画实现

2. 紧遵用户体验，不要滥用动画特效

使用简洁的显示隐藏，状态切换，滑入滑出等效果来展示元素
使用预设值来设置动画的速度'fast'，'slow'，或者400（中等速度）

####<i class="fa fa-check-square"></i>**插件相关**

1. 始终选择一个有良好支持，文档完善，全面测试过并且社区活跃的插件

2. 注意所用插件与当前使用的jQuery版本是否兼容

3. 一些常用功能应该写成jQuery插件。jQuery插件的编写模板


####<i class="fa fa-check-square"></i>**链式结构**

1. 除了用变量将jQuery选择器返回的结果保存，还可以**利用好链式**调用。
>```js 
$("#myDiv")
    .addClass("error")
    .show();
```

2. 当链式调用多达3次以上或代码因绑定回调略显复杂时，使用换行和适当的缩进来提高代码的可读性。
>```js
$("#myLink")
    .addClass("bold")
    .on("click", myClickHandler)
    .on("mouseover", myMouseOverHandler)
    .show();
//推荐这种链式写法,这是在<<编写可维护的JS>>的书籍上看到的写法,感觉很不错 
```

3. 对于特别长的调用最好还是用变量保存下中间结果来简化代码。

####<i class="fa fa-check-square"></i>**其他案例**

1. 使用对象来传递参数
>```js
$myLink.attr("href", "#").attr("title", "my link").attr("rel", "external"); // 糟糕：调用了三次attr
// 不错，只调用了一次attr
$myLink.attr({
    href: "#",
    title: "my link",
    rel: "external"
});
```

2. 不要将CSS与jQuery杂揉
>```js
$("#mydiv").css({'color':red, 'font-weight':'bold'}); // 不好
.error {/* 不错 */
    color: red;
    font-weight: bold;
}
$("#mydiv").addClass("error"); 
```

3. 时刻关注官方Changelog，不要使用摒弃了的方法。[点此查看所有废弃的方法](http://api.jquery.com/category/deprecated/)

4. 适时地使用原生JavaScript。原生的性能肯定相当好一些，查[性能比较](http://jsperf.com/document-getelementbyid-vs-jquery/3)
>```js
$("#myId"); //jquery只是为了方便实现JS想要实现的功能,至于效率 
document.getElementById("myId");
//原生JS是吊打JQ的,,这是个不争的事实
```