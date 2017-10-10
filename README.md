# html+css基础知识

## html

dl 就是definition list， 定义列表；
dt 就是definition title，定义标题；
dd 就是definition description，定义描述

```html
<dl>
  <dt>标题</dt>
  <dd>内容</dd>
</dl>
```

- \&lt; < 
- \&gt; >
- \&copy; © 
- \&nbsp; " "空格

### 文档流

> 宏观的讲，我们的web页面和photoshop等设计软件有本质的区别：web页面的制作，是个“流”，必须从上而下，像“织毛衣”。
> 而设计软件，想往哪里画个东西，都能画。

- 1） 空白折叠现象：
- 2） 高矮不齐，底边对齐：
- 3） 自动换行，一行写不满，换行写。

### 浏览器兼容

- 儿子选择器 “>” IE7开始兼容，IE6不兼容。
- 序选择器 IE8开始兼容；IE6、7都不兼容

```css
ul li:first-child{color:red;}
```

- 下列都是IE6兼容的选择器：

p
#box,
.spec,
div.box,
div .box,
div , .box
*

- 下列都是IE7开始兼容：

div>p,
div+p

- 下列都是IE8开始兼容：

div p:first-child,
div p:last-child



## css

### CSS的继承性

有一些属性，当给自己设置的时候，自己的后代都继承上了，这个就是继承性。

> color、 text-开头的、line-开头的、font-开头的。
> 这些关于文字样式的，都能够继承； 所有关于盒子的、定位的、布局的属性都不能继承。

### CSS的权重

important是英语里面的“重要的”的意思。我们可以通过语法：

`font-size:60px !important;`

`1font-size:60px; !important;`     → 不能把!important写在外面

`font-size:60px important;`      →  不能忘记感叹号

来给一个属性提高权重。这个属性的权重就是无穷大。

### 盒模型

- width是“宽度”的意思，CSS中width指的是内容的宽度，而不是盒子的宽度。
- height是“高度”的意思，CSS中height指的是内容的高度，而不是盒子的高度
- padding是“内边距”的意思
- border是“边框”
- margin是“外边距”

### 脱离文档流

css中一共有三种手段，使一个元素脱离标准文档流：

- 1） 浮动
- 2） 绝对定位
- 3） 固定定位

1)浮动：两个元素并排了，并且两个元素都能够设置宽度、高度了（这在刚才的标准流中，不能实现）。浮动想学好，一定要知道三个性质。

```css
.box1{
  float: left;
  width: 300px;
  height: 400px;
  background-color: yellowgreen;
}
.box2{
  float: left;
  width: 400px;
  height: 400px;
  background-color: skyblue;
}
```

**一个span标签不需要转成块级元素，就能够设置宽度、高度了。所以能够证明一件事儿，就是所有标签已经不区分行内、块了。**
也就是说，一旦一个元素浮动了，那么，将能够并排了，并且能够设置宽高了。无论它原来是个div还是个span。

```css
span{
  float: left;
  width: 200px;
  height: 200px;
  background-color: orange;
}
```

**浮动的元素互相贴靠**

**永远不是一个东西单独浮动，浮动都是一起浮动，要浮动，大家都浮动。**

**浮动宏观的看，就是做“并排”的。有几个性质：脱标、贴边、字围、收缩。**

- 收缩：一个浮动的元素，如果没有设置width，那么将自动收缩为文字的宽度（这点非常像行内元素）。

**浮动的清除:**

- 1：给浮动的元素的祖先元素加高度。

- 2：clear:both;

- 3：隔墙法

```html
<div class="box1">
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JS</li>
  <li>HTML5</li>
  <li>设计模式</li>
</ul>
</div>

<div class="cl h16"></div>

<div class="box2">
<ul>
  <li>学习方法</li>
  <li>英语水平</li>
  <li>面试技巧</li>
</ul>
</div>
  <!--
  我们发现，隔墙法好用，但是第一个div，还是没有高度。如果我们现在想让第一个div，自动的根据自己的儿子，撑出高度，我们就要想一些“小伎俩”，“奇淫技巧”。
  -->
  
<div>
  <p></p>
  <p></p>
  <p></p>
  <div class="cl h10"></div>
</div>

<div>
  <p></p>
  <p></p>
  <p></p>
</div>

<!--
内墙法的优点就是，不仅仅能够让后部分的p不去追前部分的p了，并且能把第一个div撑出高度。这样，这个div的背景、边框就能够根据p的高度来撑开了。
-->
  ```
  
  
  - 4：overflow:hidden;
  
### margin

1）margin的塌陷现象

- 标准文档流中，竖直方向的margin不叠加，以较大的为准。
- 如果不在标准流，比如盒子都浮动了，那么两个盒子之间是没有塌陷现象的。

2）盒子居中margin:0 auto;

- 使用margin:0 auto; 的盒子，必须有width，有明确的width。

- 只有标准流的盒子，才能使用margin:0 auto; 居中。也就是说，当一个盒子浮动了、绝对定位了、固定定位了，都不能使用margin:0 auto;

- margin:0 auto;是在居中盒子，不是居中文本。文本的居中，要使用`text-align:center;`

3)善于使用父亲的padding，而不是儿子的margin

- 如果父亲没有border，那么儿子的margin实际上踹的是“流”，踹的是这“行”。所以，**父亲整体也掉下来了**

- margin这个属性，本质上**描述的是兄弟和兄弟之间的距离**； 最好**不要用这个marign表达父子之间的距离**。所以，我们一定要善于使用父亲的padding，而不是儿子的margin。

### margin的IE6兼容问题

1)IE6双倍margin bug

- 当出现连续浮动的元素，携带和浮动方向相同的margin时，队首的元素，会双倍marign。

解决方案：

使浮动的方向和margin的方向，相反。

```css
float: left;
margin-right: 40px;
```

2)IE6的3px bug

解决办法：

不用管，因为根本就不允许用儿子踹父亲。所以，如果你出现了3px bug，说明你的代码不标准。

### 行高和字号

1)行高

- CSS中，所有的行，都有行高。盒模型的padding，绝对不是直接作用在文字上的，而是作用在“行”上的。
- 为了严格保证字在行里面居中，我们的工程师有一个约定： 行高、字号，一般都是偶数。这样，它们的差，就是偶数，就能够被2整除。

2）单行文本垂直居中

- 行高=盒子高。  只适用于单行文本垂直居中！！不适用于多行。

- 如果想让多行文本垂直居中，需要设置盒子的padding：

3）font属性

- 使用font属性，能够将字号、行高、字体，能够一起设置。

- `font: 14px/24px "Comic Sans MS";`

```css
font-size:14px;
line-height:24px;
font-family:"Comic Sans MS";
```

- 行高可以用百分比，表示字号的百分之多少。一般来说，都是大于100%的，因为行高一定要大于字号。

```css
font:12px/200% "宋体";
font:12px/24px "宋体";
```

4)color

- #000   黑
- #fff   白
- #f00   红
- #333   灰
- #222   深灰
- #ccc   浅灰

5）`background-attachment:fixed;`背景就会被固定住，不会被滚动条滚走。







