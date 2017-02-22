# [](#svg)svg

## [](#SVG 简介)SVG 简介

*   可缩放矢量图形（Scalable Vector Graphics，SVG）是基于可扩展标记语言（XML），用于描述二维矢量图形的一种图形格式。SVG由W3C制定，是一个开放标准。SVG是一种矢量图格式。
*   在 2003 年1月，SVG 1.1 被确立为 W3C 标准。参与定义 SVG 的组织有：Adobe、苹果、Auto Desk、Bit Flash、Corel、惠普、IBM、ILOG、INSO、Macromedia、微软、Netscape、OASIS、Open Text、Quark、RAL(CCLRC)、Sun、Visio、施乐等，所以SVG不是一个私有格式，而是一个开放的标准。也就是说，它并不属于任何个体的专利，而是一个通过协作、共同开发的工业标准。正是因为这点，才使得SVG能够得到更迅速的开发和应用。

## [](#优势)优势

*   SVG 可被非常多的工具读取和修改（比如记事本），支持多种滤镜和特殊效果，在不改变图像内容的前提下可以实现位图格式中类似文字阴影的效果，易于修改和编辑。
*   SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。
*   SVG 是可伸缩的
*   SVG 图像可在任何的分辨率下被高质量地打印
*   SVG 可在图像质量不下降的情况下被放大
*   SVG可以方便的建立文字索引，从而实现基于内容的图像搜索，图像中的文本是可选的，同时也是可搜索的（很适合制作地图）。
*   SVG 可与现有技术可以互动融合。例如，SVG技术本身的动态部分（包括时序控制和动画）就是基于SMIL标准。另
*   SVG文件还可嵌入JavaScript（严格的说应该是ECMA Script)脚本来控制SVG对象，还可以与 Java 技术一起运行
*   SVG 文件是纯粹的 XML。
*   SVG 图形格式可以用来动态生成图形。例如，可用SVG动态生成具有交互功能的地图，嵌入网页中，并显示给终端用户

SVG的出现带来了一次技术革命。利用SVG能够创建更加丰富多彩的信息可视化和交互性的应用，尤其是可以创建具有动态的、数据驱动的、交互式图形、图像。另外，由于是纯文本格式的．SVG比传统的图形、图像格式如GIF和JPEG占用更少的空间。因此，SVG更加适合有线带宽，并可提高下载速度。SVG和XML的开放式标准特性使其成为国际性语言。SVG标准得到了IBM、Adobe、Microsoft、Corel等几十家大公司的支持，其最新的版本是SVG 1.2。 总之，SVG技术的出现，变革了在Web上图文传递信息的方式，并将产生一种更适于Web信息发布的工作流模式，其中包括Web信息显示和印刷出版的组织方式。

## [](#SVG 实例)SVG 实例

```
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">
<circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red"/>
</svg>

```

> *   第一行包含了 XML 声明。请注意 standalone 属性！该属性规定此 SVG 文件是否是“独立的”，或含有对外部文件的引用。standalone="no" 意味着 SVG 文档会引用一个外部文件 - 在这里，是 DTD 文件。
> *   第二和第三行引用了这个外部的 SVG DTD。该 DTD 于"[http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"该](http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"该) DTD 位于 W3C,含有所有允许的 SVG 元素。SVG 代码以 `<svg>` 元素开始，包括开启标签 `<svg>` 和关闭标签 `</svg>` 。这是根元素。
> *   width 和 height 属性可设置此 SVG 文档的宽度和高度。version 属性可定义所使用的 SVG 版本，xmlns 属性可定义 SVG 命名空间。
> *   SVG 的 `<circle>` 用来创建一个圆。cx 和 cy 属性定义圆中心的 x 和 y 坐标。如果忽略这两个属性，那么圆点会被设置为 (0, 0)。r 属性定义圆的半径。
> *   stroke 和 stroke-width 属性控制如何显示形状的轮廓。我们把圆的轮廓设置为 2px 宽，黑边框。
> *   fill 属性设置形状内的颜色。我们把填充颜色设置为红色。
> *   关闭标签的作用是关闭 SVG 元素和文档本身。

## [](#HTML引入SVG的方式)HTML引入SVG的方式

*   使用 `<embed>` 标签

    ```
    <embed src="rect.svg" width="300" height="100"
    type="image/svg+xml"
    pluginspage="http://www.adobe.com/svg/viewer/install/" />

    ```

*   使用 `<object>` 标签

    ```
    <object data="rect.svg" width="300" height="100"
    type="image/svg+xml"
    codebase="http://www.adobe.com/svg/viewer/install/" />

    ```

*   使用 `<iframe>`标签

    ```
    <iframe src="rect.svg" width="300" height="100">
    </iframe>
    `<iframe>` 标签可工作在大部分的浏览器中。

    ```

## [](#H5的引入方式)H5的引入方式

*   把 SVG 直接嵌入 HTML 页面

    ```
    <svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190">
    <polygon points="100,10 40,180 190,60 10,60 160,180"
    style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;" />
    </svg>

    ```

## [](#svg 的形状)svg 的形状

*   SVG 有一些预定义的形状元素，可被开发者使用和操作
*   矩形 `<rect>`
*   圆形 `<circle>`
*   椭圆 `<ellipse>`
*   线 `<line>`
*   折线 `<polyline>`
*   多边形 `<polygon>`
*   路径 `<path>`

## [](#SVG的样式)SVG的样式

> 主要是给svg定义的形状添加样式。 | 样式和属性 | 含义 | 可能的值 | | :------------- | :------------- |:------| | 样式和属性 | 含义 | 可能的值 | | fill| 填充 | 颜色值| | stroke| 描边 | 颜色值 | | stroke-width | 描边宽度 | 数字（通常以像素为单位）| | opacity | 不透明度 | 0.0（完全透明）和1.0（完全不透明）之间的数值| | font-family | 字体 | text标签特有，CSS字体| | font-size | 字体大小 | text标签特有，数字| | text-anchor | 对齐方式 | text标签特有，left/center/right|

## [](#形状实例)形状实例

*   矩形

    > x和y的指定左上角的坐标，width和height指定矩形的尺寸。

    ```
    <rect x="20" y="20" width="250" height="250"
    style="fill:blue;stroke:pink;stroke-width:5;
    fill-opacity:0.1;stroke-opacity:0.9"/>

    ```

*   圆形

    > cx和cy指定圆心的坐标，ŗ表示半径大小

    ```
    <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red"/>

    ```

*   椭圆

    > cx和cy指定圆心坐标，rx和ry分别指定横半轴纵半轴长度

    ```
    <ellipse cx="250" cy="25" rx="100" ry="25"/>

    ```

*   线条

    > 用x1和Y1到指定线的一端的坐标，x2和y2指定的另一端的坐标。stroke指定描边让线是可见的

    ```
    <line x1="0" y1="0" x2="300" y2="300" style="stroke:rgb(99,99,99);stroke-width:2"/>

    ```

*   多边形

    > points 表示多边形的每一个点

    ```
    <polygon points="220,100 ,300,210 ,170,250" style="fill:#cccccc;stroke:#000000;stroke-width:1"/>

    ```

*   文本

    > x和y指定文本的位置。

    ```
    <text x="250" y="25">Easy-peasy</text>

    ```
