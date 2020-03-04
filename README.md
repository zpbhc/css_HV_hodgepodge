# css垂直水平居中杂烩
罗列了一些水平垂直居中的方法 这些方法足够应对我们布局中的90%以上的情况
> 在实际开发中，居中的情况非常常见，几乎存在于每天的开发中，所以借助这篇文章来总结一下水平垂直的方法，希望对大家有所帮助。

**首先约定一下DOM结构：**

```html
<div class="parent-dom">
	<span class="child-dom">e1e211</span>
</div>	
```

假定父级的CSS如下：

```css
.parent-dom{
	position: absolute;
	background: rgb(239, 52, 115);
	width: 100vW;
	height: 100vH;
	left: 0;
	top: 0;
	z-index: 999;
}

```

**说明：**

默认父级相对body绝对定位，并且宽高为屏幕的宽高，这样做的目的：1、让父级元素有宽高，否则无高度无法看出宽高居中效果；2、但是父级宽高未知，毕竟开发中不都是定宽定高的；

好了，预备工作做完了，开始吧

### 1、使用绝对定位方式

**css代码**

```css
.child-dom{
    position: absolute;
    width: 50%;
    height: 50%;
    background: #fff;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
}
```

**说明：**

首先让其相对其父级绝对定位，假定宽为50%，高为50%；这样宽高也是未知，符合我们前面的初衷，宽高未知的情况下去设定水平垂直居中；

然后结合：left、right、top、bottom都设定为0，margin设为auto；这样便达到了水平垂直居中

------

### 2、利用transform

```css
.child-dom{
    position: relative;
    width: 50%;
    height: 50%;
    background: #fff;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
}
```

**说明：**
首先这里一定要给定一个position值，最好为relative或者absolute,否则浏览器无法计算left,top值；

然后left,top值都设定为50%，偏移量translate的X轴和Y轴都设为-50%，同样可以水平垂直居中

---

### 3、flex布局

```css
.parent-dom{
	position: absolute;
	display: flex; /*固定值*/ 
	background: rgb(239, 52, 115);
	width: 100vW;
	height: 100vH;
	left: 0;
	top: 0;
	align-items: center; /*固定值*/ 
	justify-content: center; /*固定值*/ 
	z-index: 999;
}
.child-dom{
    position: relative;
    width: 50%;
    height: 50%;
    background: #fff;
}
```

**说明：**

首先这里主要是靠父级元素来控制，设定父级元素display为flex；algin-items设为center(垂直居中);justify-content设为center(水平居中)

其次子元素，可设flex值或者不设置都可以， 水平垂直居中目的完成

---

### 4、利用inline-block方式

```css
.parent-dom{
	position: absolute;
	background: rgb(239, 52, 115);
	width: 100vW;
	height: 100vH;
	left: 0;
	top: 0;
	font-size: 0; /*建议设为0*/
	z-index: 999;
}
.parent-dom:before{
    content: '';
    display: inline-block;
    vertical-align: middle;
    height: 100%;
    width: 0;
}
.child-dom{
    position: relative;
    background: #fff;
    width: 50%;
    height: 50%;
    display: inline-block;
    vertical-align: middle;
}
```

**说明：**

首先设定父级元素text-algin为center(水平居中)；**建议这里font-size为0；**

然后给父级元素一个伪类after；设定display为inline-block;height为100%；width为0；居中元素display设为inline-block;然后伪类和居中元素vertical-algin都设为middle，即可达到垂直居中的目的，**然后这里font-size重新设置一下**

---

### 5、利用table-cell

```css
.parent-dom{
    display: table-cell;
	width: 100vW;
	height: 100vH;
	background: rgb(239, 52, 115);
	text-align: center; 
	vertical-align: middle;
}
.child-dom{
    background: #fff;
	width: 50%;
	height: 25%;
	display: block;
	margin: 0 auto;
}
```

**说明：**

首先父级display设为table-cell;text-algin为center(如果子元素display为block可以不设置此值)；vertical-align设为middle;达到垂直上居中

其次子元素，建议设置一个display，如果为block，则要加上margin: 0 auto;达到水平上居中

---

### 总结

第二种方法和第三种方法适合做移动端开发或者兼容性要求不高的开发中，当然，方法肯定还有很多，一搜各式各样的居中法，什么6种终极居中法，7种最适合你的居中法，8种绝世居中法，毕竟这是一盘炒剩的菜，大家都有不同的见解，如果大家都不发表意见去总结，那前端还有什么活力？所以，前端的活力还是存在的，知识就是这样，大家一起参与，才会发展的更好，这门技术才能有活下去的潜力；

---

想要了解更多的前端方面相关的知识， *****请搜索关注微信公众号【大前端js】*****，了解更多前端的硬技术

好了，感谢大家的阅读，同时这篇文章起到抛砖引玉的作用，大家一起来讨论自己的水平居中方法，当然，前提是宽高未知哦，再一次感谢大家

> **原创不易，转载请注明出处，铭感五内**

