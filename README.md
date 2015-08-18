# 鲜为人知的currentColor

最近在做一个换肤项目的时候，发现了一个蛮有意思的特性 — currentColor。

先说说是怎样发现的，下面是一个普通的响应式导航：

 ![nav](https://raw.githubusercontent.com/ImBryanZhang/currentColor/master/img/nav.jpg)

每个item的颜色值应该就是这样：

``` css
.item { color: #000; }
```

而选中态：

``` css
.current { color: #31c27c; border-bottom: solid 2px #31c27c; }
```

但是由于需要支持换肤，所以选中态的文字颜色值和边框颜色值都不能写死，然后再用指定的换肤类名来控制颜色。

HTML：

``` html
<ul class="nav">
  <li class="current c_txt3 c_bor2">全部</li>
  <li>内地</li>
  <li>港台</li>
  <li>欧美</li>
  <li>日韩</li>
</ul>
```

CSS：

``` css
.current { border-bottom: solid 2px; }
/* 文字颜色 */
.c_txt3 { color: #31c27c; }
/* 边框颜色 */
.c_bor2 { border-color: #31c27c; }
```

有趣的是，由于一时疏忽忘记加上 `c_bor2` 来控制边框颜色，**但当我修改选中态文字颜色值的时候，边框的颜色也随之改变**。并且如果边框是由伪元素 `::after` 来模拟，同样也会有这种情况。

开始时百思不得其解，在查阅了W3C网站之后，发现CSS1和CSS2中 `border-color` 属性的默认值就是 `color` 属性的值，因此就很好的解释了：在不指定 `border-color` 的值的情况下，边框的颜色为什么随文字颜色改变而变化。

随着更进一步的研究，发现 **当前文字颜色** 还有一个专业的称谓 — currentColor，它是CSS3里一个强大的关键字，如果解释为变量的话，估计大家会更好理解。

引用[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#currentColor_keyword)中的描述：

> The currentColor keyword represents the calculated value of the element’s color property. It allows to make the color properties inherited by properties or child’s element properties that do not inherit it by default.
> 
> It can also be used on properties that inherit the calculated value of the element’s color property and will be equivalent to the inherit keyword on these elements, if any.

我们再看看currentColor的特征：

1. 1
2. 2
3. 用于所有接受颜色的属性上。

``` css
border: solid 1px currentColor;
box-shadow: inset 2px 2px 3px currentColor;
background-color: currentColor;
background-image: linear-gradient(transparent, currentColor);
fill: currentColor; 
```



## 应用

1. **精简代码**
   
   例如我们编写一个空心按钮，并且为按钮的各个状态（ `:hover` ,  `:active` , disabled ）设置了不同的样式：
   
   ``` css
   /* before */
   .btn { color: #000; border: solid 1px #000; }
   .btn:hover { color: #333; border-color: #333; }
   .btn:active { color: #666; border-color: #666; }
   .btn.disabled { color: #ccc; border-color: #ccc; }
   
   /* now */
   .btn { color: #000; border: solid 1px currentColor; }
   .btn:hover { color: #333; }
   .btn:active { color: #666; }
   .btn.disabled { color: #ccc; }
   ```
   
2. **换肤**

	

## 浏览器支持

![browser support](https://raw.githubusercontent.com/ImBryanZhang/currentColor/master/img/browser_support.jpg)

从[Can I use](http://caniuse.com/#feat=currentcolor)的数据可以看出IE9+及现代浏览器都支持，并且移动端上也支持良好。



## 扩展阅读​​

[The First CSS Variable: currentColor](http://demosthenes.info/blog/908/The-First-CSS-Variable-currentColor)



[Extending the Color Cascade with the CSScurrentColor Variable](http://blogs.adobe.com/dreamweaver/2015/02/extending-the-color-cascade-with-the-css-currentcolor-variable.html)

翻译版本：[使用CSS的currentColor变量扩展颜色级联](http://www.w3cplus.com/css3/extending-the-color-cascade-with-the-css-currentcolor-variable.html)



[Keeping CSS short with currentColor](http://osvaldas.info/keeping-css-short-with-currentcolor)

翻译版本：[currentColor让CSS更简短](http://www.w3cplus.com/css3/keeping-css-short-with-currentcolor.html)



[currentColor-CSS3超高校级好用CSS关键字](http://www.zhangxinxu.com/wordpress/2014/10/currentcolor-css3-powerful-css-keyword/)

