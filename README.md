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

但是由于需要支持换肤，所以选中态的文字颜色值和边框颜色值都不能写死，然后再用指定的换肤类名来控制颜色：

``` css
.current { border-bottom: solid 2px; }
/* 文字颜色 */
.c_txt3 { color: #31c27c; }
/* 边框颜色 */
.c_bor2 { border-color: #31c27c; }
```

有趣的是，由于一时疏忽忘记加上 `c_bor2` 来控制边框颜色，**但当我修改选中态文字颜色值的时候，边框的颜色也随之改变**。并且如果边框是由伪元素 `::after` 来模拟，同样也会有这种情况。

开始时百思不得其解，在查阅了大量国外网站之后，发现 `border` 默认的颜色就是当前的文字颜色，因此就很好的解释了：在不定义 `border` 颜色值的情况下，边框的颜色为什么随文字颜色改变而变化。

随着更进一步的研究，发现 **当前文字颜色** 还有一个专业的称谓 — currentColor，它是CSS3里一个强大的关键字，如果解释为变量的话，估计大家会更好理解。



> `currentColor` 表示当前元素被应用上的 `color` 颜色值。 使用它可以将当前这个颜色值应用到其他属性上，或者嵌套元素的其他属性上。

我们再看看currentColor的特征：

1. 1
2. 2
3. ​

``` css
border: solid 1px currentColor;
box-shadow: inset 2px 2px 3px currentColor;
background-color: currentColor;
background-image: linear-gradient(transparent, currentColor);
fill: currentColor; 
```



## 应用

1. **精简代码**
   
   例如我们在编写一个空心按钮时，
   
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





## 扩展阅读​

[The First CSS Variable: currentColor]: http://demosthenes.info/blog/908/The-First-CSS-Variable-currentColor	"The First CSS Variable: currentColor"



