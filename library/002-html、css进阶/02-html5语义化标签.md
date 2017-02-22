## [](#HTML5新增标签)HTML5新增标签

在HTML5中新添加了一系列语义化的标签，能够更恰当的描述你的内容是什么。布局时就更加的灵活和多变，使用语义化标签有利于浏览器的seo，更加有利于网站的检索。

## [](#为什么要使用语义化的标签？)为什么要使用语义化的标签？

*   可以更好地理解网页的框架。即使在没有CSS的情况下，HTML页面也能呈现出很好地内容结构、代码结构。
*   不同的语义化标签实际上为我们将网页划分了不同的模块，结构分明更利于分解模块，利于团队的合作和维护。
*   使用语义化标签有利于浏览器的seo，更加有利于网站的检索。

## [](#文档声明)文档声明

*   <!DOCTYPE> 声明必须位于 HTML5文档中的第一行，也就是位于`<html>` 标签之前。该标签告知浏览器文档所使用的HTML规范。

*   DOCTYPE 声明不属于 HTML 标签; 它是一条指令，告诉浏览器编写页面所用的标记的版本。 在所有 HTML文档中规定 DOCTYPE 是非常重要的，这样浏览器就能了解预期的文档类型。

*   HTML 4.01 中的 DOCTYPE 需要对 DTD 进行引用，因为 HTML4.01 基于 SGML（标准通用标记语言）。而 HTML 5 不基于 SGML，因此不需要对DTD （文档类型定义）进行引用，但是需要 DOCTYPE 来规范浏览器的行为（让浏览器按照它们应该的方式来运行。）

## [](#meta标签)meta标签

`<meta name ="viewport" content ="width=device-width,initial-scale=1, maximum-scale=1, minimum-scale=1,user-scalable=no">`

*   content 属性说明

| 属性值 | 说明 |
| --- | --- |
| width | viewport 宽度(数值/device-width) |
| height | viewport 高度(数值/device-height) |
| initial-scale | 初始缩放比例 |
| maximum-scale | 最大缩放比例 |
| minimum-scale | 最小缩放比例 |
| user-scalable | 是否允许用户缩放(yes/no) |

## [](#结构性标签)结构性标签

结构性标签（construct tag）主要负责Web的上下⽂文结构的定义，确保 HTML文档的完整性，这类标签包括以下几个。

*   section
    用于表达书的一部分或一章，或者一章内的一节。在Web 页⾯面应 用中，该标签也可以 用于区域的章节表述。
*   hgroup
    对网页或区段（section）的标题进行组合。
*   header
    页面主体上的头部，注意区别于head标签。这里可以给初学者提供一个判断的小技巧：head标签中的内容往往是不可见的，而header标签往往在一对body标签之中。
*   footer
    页面的底部（页脚）。通常，人们会在这里标出网站的一些相关信息，例如关于我们、法律申明、邮件信息、管理入口等。
*   nav
    是专门用于菜单导航、链接导航的标签，是navigator的缩写。
*   article
    用于表示一篇文章的主体内容，一般为文字集中显示的区域。　　　

## [](#块级性标签)块级性标签

块级块性标签（block tag）主要完成Web页面区域的划分，确保内容的有效分隔，这类标签包括以下几。

*   aside
    用以表达注记、贴士、侧栏、摘要、插入的引 用等作为补充主体的内容。从一个简单页面显示上，就是边栏，可以在左边，也可以在右边。从一个页面的局部看，就是摘要。
*   figure
    标签规定独立的流内容，通常与figcaption联合使 用。
*   code
    表示一段代码块。
*   dialog
    对话标签配合dt dd标签使用

## [](#行内标签)行内标签

行内语义性标签（in-line tag ）主要完成Web页面具体内容的引用和表述，是丰富内容展示的基础，这类标签包括以下几个。

*   meter
    表示特定范围内的数值， 可用于工资、数量、百分比等。max表示最大值，min表示最小值，value代表当前值。

    ```
    <meter min="2" max="10"  value="3"></meter>

    ```

*   time
    表示时间值，属性datetime强调时间
*   progress
    用来表示进度条

## [](#多媒体标签)多媒体标签

*   video
    视频标签，用于支持和实现视频（含视频流）文件的直接 播放，支持缓冲预载和多种视频媒体格式如MPEG-4、OggV和WebM等。

    ```
    <video width="320" height="240" controls>
    <source src="video.mp4" type="video/mp4">
    <source src="video.ogg" type="video/ogg">
     您的浏览器不支持Video标签。
    </video>

    ```

    > `<video>` 元素提供了 播放、暂停和音量控件来控制视频。同时 `<video>` 元素元素也提供了 width 和 height 属性控制视频的尺寸.如果设置的高度和宽度，所需的视频空间会在页面加载时保留。。如果没有设置这些属性，浏览器不知道大小的视频，浏览器就不能再加载时保留特定的空间，页面就会根据原始视频的大小而改变。 `<video>`与`</video>` 标签之间插入的内容是提供给不支持 video 元素的浏览器显示的。 `<video>` 元素支持多个 `<source>` 元素。`<source>` 元素可以链接不同的视频文件。浏览器将使用第一个可识别的格式。

*   audio 音频标签，用于支持和实现音频（音频流）文件的直接播放，支持缓冲预载和多种音频媒体格式。

    ```
    <audio controls>
      <source src="audio.ogg" type="audio/ogg">
      <source src="audio.mp3" type="audio/mpeg">
      您的浏览器不支持 audio 元素。
    </audio>

    ```

| 属性 | 值 | 描述 |
| --- | --- | --- |
| autoplay | autoplay | 如果出现该属性，则音频在就绪后马上播放 |
| controls | controls | 如果出现该属性，则向用户显示音频控件（比如播放/暂停按钮） |
| loop | loop | 如果出现该属性，则每当音频结束时重新开始播放 |
| muted | muted | 如果出现该属性，则音频输出为静音。 |
| preload | auto、metadata、none | 规定当网页加载时，音频是否默认被加载以及如何被加载。 |
| src | URL | 规定音频文件的 URL。 |

## [](#列表标签)列表标签

*   datalist
    标签定义选项列表。请与 input 元素配合使用该元素，来定义 input 可能的值。datalist 及其选项不会被显示出来，它仅仅是合法的输入值列表。所有主流浏览器都支持 <datalist>标签，除了 Internet Explorer 和Safari。

    ```
    <input list="browsers" name="browser">
    <datalist id="browsers">
     <option value="Internet Explorer">
     <option value="Firefox">
     <option value="Chrome">
     <option value="Opera">
     <option value="Safari">
    </datalist>

    ```

    ## [](#交互性标签)交互性标签

    交互性标签（interactive tag）主要用于功能性的内容表达，会有一定的内容和数据的关联，是各种事件的基础，这类标签包括以下几个。主流浏览器不支持。</datalist>
*   menu
    主要用于交互菜单（这是一个曾被废弃现在又被重新启用的标签）。
*   command
    用来处理命令按钮

## [](#画板标签)画板标签

HTML5 `<canvas>` 元素用于图形的绘制，通过脚本 (通常是JavaScript)来完成。`<canvas>` 标签只是图形容器，您必须使用脚本来绘制图形。你可以通过多种方法使用Canva绘制路径，盒、圆、字符以及添加图像。

```
  <canvas id="myCanvas" width="200" height="100" style="border:1px solid #000000;">
  </canvas>

```
