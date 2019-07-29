# CSS布局

tags： CSS 布局

[TOC]
***
##介绍 CSS 布局

###正常布局流
:    浏览器默认的HTML布局方式。
###浮动
主要用途是布置出多个列并且浮动文字以环绕图片。float 属性有四个可能的值：

> - left — 将元素浮动到左侧。
> - right — 将元素浮动到右侧。
> - none — 默认值, 不浮动。
> - inherit — 继承父元素的浮动属性。

###定位技术
四种主要的定位类型：

> - **静态定位(Static positioning)是每个元素默认**的属性。
- **相对定位(Relative positioning)**
- **绝对定位(Absolute positioning)元素从正常布局流移出，相对于页面的 <html> 元素边缘固定，或者相对于离元素最近的被定位的祖先元素(ancestor element)。**
- **固定定位(Fixed positioning)相对浏览器视口固定。

>这里我们给中间段落一个position relative值——这属性本身不做任何事情，所以我们还添加了top和left属性。这些可以将受影响的元素向下向右移——这可能看起来和你所期待的相反，但你需要把它***看成是左边和顶部的元素被“推开”一定距离***，这就导致了它的向下向右移动。

*******

###CSS 表格
``` HTML
<form> 
<p>First of all, tell us your name and age.</p>
<div>
<label for="fname">First name:</label>
<input type="text" id="fname"> </div> 
<div>
<label for="lname">Last name:</label> 
<input type="text" id="lname"> </div>
<div> 
<label for="age">Age:</label>
<input type="text" id="age">
</div> 
</form>
```
``` CSS
html { 
       font-family: sans-serif;
}
form { 
       display: table;
       margin: 0 auto; 
       }
form div { 
       display: table-row; 
       } 
form label, form input { 
       display: table-cell; 
       margin-bottom: 10px; 
       }
form label  {
       width: 200px; 
       padding-right: 5%;
       text-align: right;
       }
form input {
       width: 300px;
       } 
form p { 
       display: table-caption;
       caption-side: bottom;
       width: 300px;
       color: #999; 
       font-style: italic; 
       }
```
###弹性盒子
###网格布局

***
##正常布局流

***
##弹性盒子flex
优势：

> - 垂直居中
> - 高度宽度等分
> - 每列相同高度

###flex模型
> - 主轴（main axis）是沿着 flex 元素放置的方向延伸的轴（比如页面上的横向的行、纵向的列）。该轴的开始和结束被称为 main start 和 main end。
- 交叉轴（cross axis）是垂直于 flex 元素放置方向的轴。该轴的开始和结束被称为 cross start 和 cross end。
- 设置了 `display: flex`的父元素（在本例中是 <section>）被称之为 flex 容器（flex container）。
- 在 flex 容器中表现为柔性的盒子的元素被称之为 flex 项（`flex item`）（本例中是 <article> 元素。


###列还是行? flex-direction 
默认值是 row,换成列 

    flex-direction: column;
###换行
    flex-wrap: wrap;
    flex: 200px;

###flex 项的动态尺寸`flex: 1`
    article { flex: 1; }

每个元素占用空间都是相等.
   
    article:nth-of-type(3) { flex: 2; }
占两份宽度。

    article { flex: 1 200px; } 
    article:nth-of-type(3) { flex: 2 200px; }
表示“每个flex 项将首先给出200px的可用空间，然后，剩余的可用空间将根据分配的比例共享“。

###flex: 缩写与全写
不推荐缩写
###水平和垂直对齐`align-items: center`
``` CSS
div {                display: flex; 
               align-items: center;
        justify-content: space-around; }
```
`align-items` 控制 flex 项在***交叉轴***上的位置。值：

> - stretch **拉伸**
- center **居中**
- `flex-start `或` flex-end `控制**开始**或**结束**处对齐所有的值。

其他值：
``` CSS
/* Basic keywords */ 
align-items: normal; 
align-items: stretch; 
/* Positional alignment */
 align-items: center; 
/* Pack items around the center */
 align-items: start; 
/* Pack items from the start */ 
align-items: end; 
/* Pack items from the end */
 align-items: flex-start; 
/* Pack flex items from the start */
 align-items: flex-end; 
/* Pack flex items from the end */
 align-items: self-start; 
align-items: self-end; 
/* Baseline alignment */ 
align-items: baseline; 
align-items: first baseline;
 align-items: last baseline;
 /* Overflow alignment (for positional alignment only) */ 
align-items: safe center;
 align-items: unsafe center; 
/* Global values */
 align-items: inherit; 
align-items: initial; 
align-items: unset;
```

 `align-self` 控制单个 `align-items `的行为。
    
    button:first-child { align-self: flex-end; }
    
    
`justify-content` 控制 flex **主轴**上的位置。

> - flex-start
- flex-end 
- center
- space-around 均匀分布，两端有空间。
- space-between 均匀分布，两端无空间。

###flex 项排序`order: 1`

    button:first-child { order: 1; }
:**值小排前**，所有值默认为0

###flex 嵌套
:  *设置一个元素为flex项目，那么他同样成为一个 flex 容器，它的直接子节点也表现为 flexible box 。*
***
##网格grid
###一个简单的浮动定宽网格
``` CSS
* { box-sizing: border-box; }
.row { clear: both; }
.col { float: left;
        margin-left: 20px;
         width: 60px;
         background: rgb(255, 150, 150); }

```

####自适应
#####百分比
    target / context = result
    60 / 960 = 0.0625
    
#####使用calc() 函数计算
跨越网格的多个列的任何列具有***6.25％***的总宽度***乘以***跨越的***列数*** ***加上2.08333333％乘以槽的数量（其将总是列数减去1）***。该calc()函数允许我们在宽度值内部执行此计算，因此对于跨4列的任何项目，我们可以执行此操作，例如：
   
    .col.span4 { width: calc((6.25%*4) + (2.08333333%*3)); }
###什么是语义与“非语义”网格系统？？？？？
###网格容器偏移
    .offset-by-one { margin-left: calc(6.25% + (2.08333333%*2)); }
    or
    .offset-by-one { margin-left: 10.41666666%; }
##Flexbox 网格
**flexbox从来没有被设计为网格系统。**
``` CSS
body {
      width: 90%;
      max-width: 980px; 
      margin: 0 auto;
      } 
.wrapper {
           padding-right: 2.08333333%; 
} 
.row { display: flex; } 
.col { 
       margin-left: 2.08333333%; 
       margin-bottom: 1em;
       width: 6.25%; 
       flex: 1 1 auto; 
       background: rgb(255,150,150); 
       }
```
***Flexbox是一维设计***。它处理单个维度，即***行或列***。不能为列和行创建严格的网格，这意味着如果我们要为网格使用flexbox，我们仍然需要为浮动布局计算百分比。

***
##浮动`float`
:    float 属性最初只用于在成块的文本内浮动图像，但是现在它已成为在网页上创建多列布局的最常用工具之一。
###多列浮动布局
####两列布局
``` CSS
body { width: 90%; max-width: 900px; margin: 0 auto; }
div:nth-of-type(1) { width: 48%; }
 div:nth-of-type(2) { width: 48%; }
div:nth-of-type(1) { width: 48%; float: left; }
 div:nth-of-type(2) { width: 48%; float: right; }


```
####三列布局
``` CSS
body { width: 90%; max-width: 900px; margin: 0 auto; } 
div:nth-of-type(1) { width: 36%; float: left; } 
div:nth-of-type(2) { width: 30%; float: left; margin-left: 4%; }
 div:nth-of-type(3) { width: 26%; float: right; }
```

###清除浮动
    footer { clear: both; }
clear 可以取三个值：

> - left：停止任何活动的左浮动
- right：停止任何活动的右浮动
- both：停止任何活动的左右浮动
###浮动问题

整个宽度可能难以计算
布局损坏 —— 由于内边距和边界引入的额外宽度，一行容纳不下三列了，因此第三列下降到另外两列之下。
有两个方法可以解决问题，最好的方法是给你的html加上下面的css。
    
    * { box-sizing: border-box; }
所以，让我们解决这个！ 首先，在HTML的代码里添加新的<div> 元素，位于在<footer>标签的上方：
    
    <div class="clearfix"></div>
如果您没有一个可用的元素来清除您的浮动(比如我们的页脚)，在您想要清除的浮动之后添加一个看不见的“clearfix div”是非常有用的，但是在这里页脚也要用到。接下来我们要做的是，移除页脚样式规则中的 clear: both; 声明，取而代之将其放在clearfix div中：
    
    .clearfix { clear: both; }
我们的页脚现在有一个很好的顶部外边距，但也有另一个问题——clearfix div 背景、内边距和边界与我们的列和页脚相同！为了解决这个问题，让我们先给每个列块一个类（ class ）column：


    <div class="column"> ... </div>
 现在让我们改变应用盒子样式的规则到这些块和页脚，这样只有列块被样式化：


    .column, footer { padding: 1%; border: 2px solid black; background-color: red; }
至此，修复问题大概就那样。
***
##定位`position`
###文档流
###静态定位`static`
###相对定位`relative`
:  相对定位工作的方式——你需要考虑一个看不见的力，推动定位的盒子的一侧，***移动它的相反方向。*** 所以例如，如果你指定 top: 30px;一个力推动框的顶部，使它向下移动30px。
###绝对定位`absolute`
:  ***绝对定位的元素不再存在于正常文档布局流中。被放在<html>元素的外面，相对与窗口。***
###定位上下文（定位父子元素）
**目的：**让绝对定位的元素回 **body**以内。利于布局。
**做法：**将它的父元素设置为相对定位`position:relative`。

###z-index
:  当元素开始重叠，什么决定哪些元素出现在其他元素的顶部？
   
>    “z-index”是对z轴的参考。
      z-index只接受无单位索引值。
      z-index: 1;
### 固定定位
:  与绝对定位的工作方式完全相同，只有一个主要区别：绝对定位固定元素是相对于 **html** 元素或其最近的定位祖先，而固定定位固定元素则是***相对于浏览器窗口***本身。

###`position: sticky`
:  是一个比其他属性要新一些的属性。这基本上是相对位置和固定位置之间的混合，其***允许定位的元件像它被相对定位一样动作，直到其滚动到某一阈值点（例如，从视口顶部10像素），之后它变得固定。***阅读我们的position:sticky 引用入口 查看详情和例子。
