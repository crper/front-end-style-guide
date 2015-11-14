- 统一字符编码 : ```charset 'utf-8' ```;
- 两个空格取代tab键盘;很多语言都这样协定,挺好;
- 代码需要断行,且必须带上分号;
>```css
.test {
    property1: attr;
    property2: attr;
    property3: attr;
}
>```
----
- 字符串和超链接使用单引号包裹,内部出现其他冲突符号建议使用转义字符
- 数字为0的不建议带单位,很多IDE都推荐干掉;
- 运算上,使用通用计算思维考虑,最高级别的用小括号包裹
- 颜色上,十六进制的颜色推荐`#fff`(小写且尽可能的缩写),RGBA`(0,0,0,.5)`[逗号之间不带空格]
- 变量上,有可能复用的引用,应该赋值给变量;对于偶尔使用的,推荐使用`%placeholder`占位符变量;
- map上,推荐json的写法;
>```css
'name': 'CRPER', //冒号后空格再写值,逗号结尾
'mage': 22,  //每个值对独占一行
>```
- 嵌套中,不仅仅考虑使用CSS的写法,跟应该使用新属性`&`来减少变量名的书写,方便阅读和引用正确
>```css
a{
    &:link,
    &:visited{
        color:#000;
}
    &:hover{
            color:#000;
    }
}
>```
------
- 嵌套中,属性根据类型进行排序`（position, display, colors, font, miscellaneous…）`,类型之间隔行
>```css
.container{
    /*定位*/
    position:absolute;
    left:50%;
    top:50%;
   transform:translate(-50%,-50%);
>   
   /*盒子类型*/
   display:block;
>
  /*颜色控制*/
   color:#000;
   background-color:#f00;
   border-color:#ff0;
>
  /*字体设置*/
  font-family:"微软雅黑";
  font-size:15px;
  font-weight:700;
  line-height:30px;
  text-decoration:none;
  work-break:break-all;
>
  /*阴影设置*/
  text-shadow: 1px 1px 1px rgba(0,0,0,.5);
  box-shadow: 1px 1px 1px rgba(0,0,0,.5);
>  
>}
>```
------
- 命名规范,推荐和CSS统一,小写加小横杆`wrapper-inbox`
- 注释上,推荐和JS一样,有函数,写明类型,结果;可以参考`Docblock`
- 目录层次上,相同文件夹的import不换行,不同文件夹的导入要换行(建议参考bootstrap的sass写法)
- 混合宏(mixin),在传入CSS3阴影这类多参数的值时,应该使用`$var...`
>```css
@mixin shadows($shadows...) {
>
}
>```
----
-  循环条件判断可以参考JS的规范写法
>```css
@if (true){
} @else (){
}
>```

---

- `@extend`在前,`@include`其次,常规样式在后,伪类在最后
>```css3
.test {
  @extend %module; 
  @include transition(all 0.3s ease-out);
  background: #000;
    &:hover {
    background: DarkCyan;
  }
  &::before {
    content: "";
    display: block;
  }
  ...
}
>```


---

- 嵌套最好不过三,有利于阅读,也有利于维护
>```css
.outer {
  .inner {
    innercontent {
      // no more!
    }
  }
}
>```

---

- 通用样式必须注明作用
>```css
.overlay {
  // modals are 6000, saving messages are 5500, header is 2000
  z-index: 5000; 
}
>```

---

- 建议使用模块化写法,每个组件单独写个`scss`文件,通过`@import`来汇总成一个主scss文件,这样非常有利于维护;
- 模块内部的样式,建议在一百条内

