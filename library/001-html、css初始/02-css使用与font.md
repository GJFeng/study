# [](#CSS)CSS

## [](#名词解释)名词解释

### [](#网页标准布局：div+css网页标准布局方式)网页标准布局：div+css网页标准布局方式

#### div

> 全称 division 意为"区块、分割"div标签是一个无意义的容器标签，用于将页面划分出不同的区域。 通过div将复杂的页面进行细分块，可以将问题细分一个一个解决，所以通过div将页面分块是一个关键的工作，也是决定最终效果与质量的前提。

#### css（Cascading Style Sheet）

> 中文翻译为层叠样式表，是用于控制网页样式并允许将样式信息与网页内容分离的一种标记性语言。

div承载的是内容，css承载的是样式。

### [](#div+css布局优点)div+css布局优点

*   div+css是web标准，顺应潮流。
*   弥补html标签的功能缺陷。
*   加快页面加载的速度，降低流量费用。
*   对搜索引擎更加友好，更有利于收录和抓取您的页面。
*   使页面的内容和表现分离，便于维护和管理，节省大量的人力和成本。

### [](#div+css布局缺点)div+css布局缺点

*   使用相对复杂相对html中的table布局来说，div+css布局相对要复杂些，需要掌握的知识更多些
*   css网站设计的浏览器兼容性问题比较突出，各个浏览器对CSS的支持略有不同，但这些细小的不同也会使网站在各个浏览器中有较大的显示差异，甚至是面目全非。

## [](#CSS 的引入方式)CSS 的引入方式

要利用div+css的布局方式，那么首先我们来看如何引入css。

### [](#行内样式表)行内样式表

> 顾名思义，我们要修饰哪个元素我们就将css写在哪个标签上。

```
  <div style='属性:值;属性:值……'></div>

```

```
  <div style='width:200px;height:200px;background:red'> </div>

```

### [](#嵌入样式表)嵌入样式表

> css样式表是写在html文件中的，因此我们称之为嵌入样式表。

```
  <style> 选择器{属性：值;属性：值;……}</style>

```

```
 <head>
   <style>
      div{
        width:200px;
        height:200px;
        background:red;
      }
   </style>
 </head>

```

### [](#外部样式表)外部样式表

> 该方法是需要我们引入一个外部的css样式表。

*   新建css样式表
*   引入 `<link rel='stylesheet' type='text/css' href='地址'>`

```
<link rel='stylesheet' type='text/css' href='uek.css'>

```

### [](#导入样式表)导入样式表

> 该方法是将一个css样式表导入到另一个css样式表中。

*   `@import` url(外部样式表位置)

```
 @import url('index.css');

```

## [](#优先级)优先级

现在我们可以有4中方式将css引入到我们的页面当中。那么当一个html文件中利用多种方式引入css，哪种方式会作用到页面元素呢？因此我们需要引入优先级。优先级也就是说哪种样式会优先作用到元素。

*   行内样式最高
*   其他的样式表，优先级一样，按照导入的顺序来确定他们是否起作用。

## [](#选择器)选择器

当我们定义一条样式规则时候，这条样式规则会作用于网页当中的某些元素，而我们的规定的这些元素的规则就叫做选择器。

> 在此处我们需要注意，css既然是用来修饰页面中元素样式的，那么页面中必须存在该元素。

| 选择器 | 格式 | 作用范围 |
| --- | --- | --- |
| id选择器 | #id | 选择页面中指定id名的元素，id是唯一的 |
| 类名选择器 | .classname | 选择页面中指定类名的元素集合 |
| 标签选择器 | tagname | 选择页面中所有指定标签元素集合 |
| 交叉选择器 | tagname.classname | 选择页面中同时符合俩个条件元素集合 |
| 群组选择器 | 多个选择器用‘，’隔开 | 选择多个选择器指定元素 |
| 后代选择器 | 父级 空格 子级 | 选择某父元素下面的子元素 |
| 通用选择器 | * | 选择页面中所有的元素 |

## [](#伪类选择器)伪类选择器

同一个html元素在不同状态下的不同样式

| 选择器 | 描述 |
| --- | --- |
| :link | 未访问的链接 |
| :active | 选定的链接 |
| :hover | 鼠标移动到链接上 |
| :visited | 已访问的链接 |
| :first-letter | 选择段落中的第一个字母或中文字符 |
| :first-line | 选择文本中的首行 |

## [](#CSS的继承性和叠加性)CSS的继承性和叠加性

### [](#继承性)继承性

> 后代元素会继承前辈元素的一些属性和样式。

### [](#叠加性)叠加性

> 同一个元素，被多个样式规则指定。

因为有了继承性和叠加性，就有了css的优先级。

## [](#选择器的优先级)选择器的优先级

所谓的优先级，指的就是哪条样式规则会最作用于指定的元素
![选择器优先级](amWiki/images/001-yxj.png);

## [](#CSS注释)CSS注释

`/* css code */`

## [](#文字属性)文字属性

| 属性 | 描述 | 值 |
| --- | --- | --- |
| font-size | 文字大小 | px、em |
| font-family | 文字字体 | 微软雅黑、宋体 |
| font-weight | 文字粗细 | bold（加粗）normal（正常）100~900（9级加粗） |
| font-style | 文字风格 | normal（默认值标准样式）italic （斜体）oblique（倾斜）inherit |
| color | 文字颜色 | rgb、#ffffff、red |

`字体缩写 font: bold 12px/20px "宋体" ; 如果缩写至少要定义 font-size 和font-family两个属性`

## [](#文本段落)文本段落

| 属性 | 描述 | 值 |
| --- | --- | --- |
| text-align | 设置文本水平对齐方式 | left左对齐，right右对齐，center居中对齐，justify两端对齐 |
| vertical-align | 设置元素垂直对齐方式 | super上标，sub下标，top与行中最高元素顶端对齐，middle父元素的中间位置，bottom与行中最低元素底端对齐.常用来对齐表单元素和图片，在块元素内不起作用，在行内元素中起作用。 |
| line-height | 设置元素的行高字体行高，单行文字一般用来设置居中， | 常用单位em |
| text-indent | 设置首行的缩进方式 | 常用单位em |
| word-break | 自动换行 | break-all |
| text-transform | 设置文本的大小写 | none（无转换） capitalize（将每个单词的第一个字母转换成大写）
uppercase（将每个单词转换成大写）lowercase（将每个单词转换成小写） |
| letter-spacing | 设置字间距 | normal、length、percentage（css3） |
| text-indent | 设置首行缩进 | length、percentage |
| text-size-adjust | 设置移动端页面中对象文本大小 | （auto）文本大小根据设备尺寸进行调整。（none）文本大小不会根据设备尺寸进行调整。（percentage）用百分比来指定文本大小在设备尺寸不同的情况下如何调整。 |

```
<style media="screen">
   .fontcap{
     text-transform: capitalize;
   }
   .fontup{
     text-transform: uppercase;
   }
   .fontlow{
     text-transform: lowercase;
   }
</style>
<span class="fontcap">web ui php</span>
<span class="fontup">web ui php</span>
<span class="fontlow">WEB UI PHP</span>

```
