
# [](#CSS 兼容问题)CSS 兼容问题

CSS网站设计的浏览器兼容性问题比较突出各个浏览器对CSS的支持略有不同，但这些细小的不同也会使网站在各个浏览器中有较大的显示差异，甚至是面目全非，所以我们要学会如何处理这些问题。

## [](#浏览器给一些标签默认样式)浏览器给一些标签默认样式

*   解决：清除默认样式，保证在每个浏览器样式统一。

    ```
    body,p,ul,h1,h2,h3,h4,h5,h6,ol,dl,dd,form,input,ul,ol{
    margin:0;padding:0;list-style:none;font-weight:normal;
    }
    img{border:none;}

    ```

## [](#img标签底部间隙问题)img标签底部间隙问题

*   问题：div中包含一张图片，底部可能有2px 4px或更多的间隙，不同font-size会影响这个间隙的大小。
*   解决：将图片的垂直对齐方式vertical-align，值为top或bottom；将图片转换为块标签，display:block；将包含图片的父容器的字体大小设为零，font-size:0；

## [](#img标签IE下图片有边框)img标签IE下图片有边框

*   问题：html 图片img加了超链接（a标签）之后产生难看的蓝色边框！（IE6-10）
*   解决：img{border:0;}

## [](#margin-top没有加到指定元素身上)margin-top没有加到指定元素身上

*   问题：在一个容器中给子元素一个上边距，父元素和子元素一起往下移动这是一个bug。
*   解决：
    1.  通过给父元素一个像素的透明边框:border:1px solid rgba(0,0,0,0);
    2.  通过给父元素一个:padding-top来模拟margin-top;

## [](#IE6双倍边距 bug)IE6双倍边距 bug

*   问题：当我们给元素添加浮动的并指定左外边距的时候，IE6会出现双倍边距
*   解决：给浮动的元素指定 display:inline;

## [](#父容器（子元素浮动）高度为0)父容器（子元素浮动）高度为0

*   问题：父元素的高度不确定，且子元素个数不确定、而且还是float，会引发父元素高度为0问题，浮动的子元素层级高于父元素导致撑不开父元素的高度!
*   解决：
    1.  在使用float元素的父元素结束前加一个高为0宽为0且有clear:both样式的空div `<div style="clear:both;"></div>`
    2.  在父容器上添加overflow:hidden

## [](#IE6不支持固定定位)IE6不支持固定定位

*   问题：IE6不支持固定定位；（利用绝对定位模拟固定定位）
*   解决：

    ```
    选择器{
      width:200px;height:200px;background:red;
      position:fixed;bottom:50px;right:50px;
      *position:absolute;
      *top:expression(eval(document.documentElement.scrollTop+200));
    }
    *html{
      background-image:url(blank:about);
      background-attachment:absolute;
    }

    ```

## [](#IE6下png图片不支持透明度)IE6下png图片不支持透明度

*   问题：在ie6下png图片不支持透明度
*   解决：

    ```
    filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(enabled=true, sizingMethod=image,src="opacity.png");
    _background:none;

    ```

## [](#CSS hack)CSS hack

*各浏览器兼容CSS

```
    .bb{
        background-color:#f1ee18; /*所有识别*/
        background-color:#00deff\9; /*IE6、7、8识别*/
        +background-color:#a200ff; /*IE6、7识别*/
        _background-color:#1e0bd1; /*IE6识别*/
      }

```

![css hack表](amWiki/images/hack.png)
