# [](#css盒子模型)css盒子模型

*   盒子模型是CSS的基石之一，布局最重要的概念，它指定元素如何呈现在页面当中。网页就是由许多个盒子通过不同的排列方式（纵向排列，横向排列，嵌套排列）堆积而成。
*   页面上的每个元素都被浏览器看成是一个矩形的盒子，这个盒子由元素的内容、填充、边框和边界组成。
*   默认情况下盒子的边框是无，背景色是透明，所以我们在默认情况下看不到盒子

## [](#盒子的相关概念和属性)盒子的相关概念和属性

*   内容
    *   盒子里面所包含的元素和内容
*   填充(内边距) (padding)
    *   盒子里面的内容到盒子的边框之间的距离. padding-left、 padding-right、 padding-top、padding-bottom
*   边框(border)
    *   盒子本身有边框(border) border-left、 border-right、 border-top、 border-bottom
*   外边距(magin)
    *   边框外和其它盒子之间 margin-left、 margin-right、 margin-top、margin-bottom
*   盒子实例图示
    ![盒子实例图示](amWiki/images/2016-12-13_010759.png)
*   盒子示意图示
    ![盒子实例图示](amWiki/images/2016-12-13_011313.png)

## [](#设置盒子padding和margin的方式)设置盒子padding和margin的方式

| 设定值的个数 | 写法 | 描述 |
| --- | --- | --- |
| 1个属性值 | padding:40px;margin:40px; | 表示上下左右的值都是该值 |
| 2个属性值 | padding:10px 10px; | 前者表示上下的值，后者表示左右的值 |
| 3个属性值 | padding:10px 20px 10px; | 前者表示上边的值，中间的数值表示左右的值，后者表示下边的值 |
| 4个属性值 | padding:10px 20px 10px 10px; | 依次表示上、右、下、左的值，即顺时针排序 |
| 单独设定属性值 | padding-left、 padding-right、 padding-top、padding-bottom |

## [](#盒子的宽高属性)盒子的宽高属性

| 盒子所占大小 | 计算方式 |
| --- | --- |
| 盒子所占宽度 | width + padding-left + padding-right + border-left + border-right 设定宽度+左右内边距+左右边框 |
| 盒子所占高度 | height + padding-top + padding-bottom + border-top + border-bottom 设定高度+上下内边距+上下边框 |
| width | 宽度设定的具体值 |
| height | 高度设定的具体值 |
| width auto | 一般会是父元素的宽度 |
| height auto | 一般会是内容的高度 |

### [](#边框)边框

| 类型 | 设置方式 |
| --- | --- |
| border-width | border-top-width、border-right-width、border-bottom-width、border-left-width对某一面的边框宽度单独设置 |
| border-color | 设置四个方面的边框颜色，可以通过设置border-top-color、border-right-color、border-bottom-color、border-left-color对某一面的边框颜色单独设置 |
| border-style | 设置四个方面的边框样式，可以通过设置border-top-style、border-right-style、border-bottom-style、border-left-style对某一面的边框样式进行单独设置. |

*   border常见的样式
    *   none：无样式
    *   dotted：点线
    *   dashed：虚线
    *   solid：实线
    *   double：双线
    *   groove：槽线
    *   ridge：脊线
    *   inset：内凹
    *   outset：外凸
*   实例

    ```
    .sample-border1{
    border-top-width:1px;
    border-top-style:dotted;
    border-top-color:#cccccc;
    }
    .sample-border2{
    border-top:1px solid #cccccc;
    border-left:1px solid #cccccc;
    border-right:1px soli #cccccc;
    border-bottom:1px solid #cccccc;
    }
    // 缩写后
    .sample-border1{
    border-top:1px dashed #ccc;
    }
    .sample-border2{
     border:1px solid #ccc;
    }

    ```

## [](#关于填充和边距的常见问题)关于填充和边距的常见问题

*   大部分html元素的盒子属性(margin, padding)默认值都为0，有少数html元素的(margin, padding)浏览器默认值不为0，例如：body，p，ul，li，form标记等，因此我们有时有必要先设置它们的这些属性为0。
*   相邻两个兄弟元素的外边距会发生合并，一般布局我们都会设定他们的外边距
*   如果没有设置父级元素的内边距或边框那么他的子元素的边界会和其合并
*   margin-top bug的问题:当两个容器嵌套时,如果外层容器和内层容器之间没有别的元素,并且外层容器没有边框和padding值的时候，部分浏览器会把内层元素的margin-top作用与父元素
*   设定一个块元素居 中 `margin:0 auto;`
*   margin可以设置负值，padding不可以
*   行内元素的margin值，只有左右，没有上下的值

## [](#标签分类)标签分类

| 分类 | 特性 | 代表元素 |
| --- | --- | --- |
| 块标签 | 有宽、高属性，同时块标签会独占一行 | H1～H6、P、li、div |
| 行标签 | 不具有宽、高特性，mrgin属性的值，只有左右没有上下。也不会占一行 | 字体标签、span |
| 行内块标签 | 既有行元素的属性即:不会独占一行又有块元素的属性即：可以设置宽高 | img 、表单元素 |

## [](#display)display

> 元素的在页面中的存在形式

| 值 | 特性 |
| --- | --- |
| `display: none;` | 可以让元素隐藏起来并且不占用页面空间,浏览器会完全忽略掉这个元素，该元素将不会被显示，也不会占据文档中的位置 |
| `display:block;` | 可以让元素具有块特性将块级元素 |
| `display:inline;` | 可以让块级元素变为行内元素 |
| `display:inline-block;` | 指定元素兼有块级和行级元素的特性，即在行内显示但是可以设定宽高 |

*   元素的相互转化

| 类型 | 方式 |
| --- | --- |
| 其它元素转化为块元素 | `display:block` |
| 其它元素转化为行元素 | `display:inline` |
| 其它元素转化为行内块元素 | `display:inline-block` |

> 在IE6中当行内元素转换为块元素时，高度会比原有的高度大，所以要设置overflow:hidden,来做兼容。
