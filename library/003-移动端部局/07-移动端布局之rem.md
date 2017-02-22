# [](#REM 布局解析)REM 布局解析

## [](#什么是rem？)什么是rem？

> rem:W3C官网描述是“font size of the root element”，即rem是相对于根元素。也就是说rem其实就是一个单位，1rem=1*html字体大小

```
html{
  font-size: 100px;
}
div{
  width:2rem;
  height:2rem;
  margin-left: 0.5rem;
  // 那么这里的实际值，其实就是2* 1*100px =200px 像素。
}

```

## [](#支持rem的浏览器)支持rem的浏览器

![rem](amWiki/images/rem.png);

## [](#rem布局方式 (js篇))rem布局方式 (js篇)

> 最简单的方式，引入如下代码

```
注/(function (doc, win) {
        var docEl = doc.documentElement,
            resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
            recalc = function () {
                var clientWidth = docEl.clientWidth;
                if (!clientWidth) return;
                if(clientWidth>=640){
                  // 这里的640 取决于设计稿的宽度
                    docEl.style.fontSize = '100px';
                }else{
                    docEl.style.fontSize = 100 * (clientWidth / 640) + 'px';
                }
            };

        if (!doc.addEventListener) return;
        win.addEventListener(resizeEvt, recalc, false);
        doc.addEventListener('DOMContentLoaded', recalc, false);
    })(document, window);

```

### [](#上述代码解析)上述代码解析

*   代码的大意为
    如果页面的宽度超过了640px，那么页面中html的`font-size`恒为100px，否则，页面中html的`font-size`的大小为： 100 * (当前页面宽度 / 640)
*   为什么是640px？
    对于手机屏幕来说，640px的页面宽度是一个安全的最大宽度，保证了移动端页面两边不会留白。注意这里的px是css逻辑像素，与设备的物理像素是有区别的。如iPhone 5使用的是Retina视网膜屏幕，使用2px x 2px的 device pixel 代表 1px * 1px 的 css pixel，所以设备像素数为640 x 1136px，而它的CSS逻辑像素数为320 x 568px。如果要切移动端页面，你可以先把效果图宽度等比例缩放到640px，很好用。
*   为什么要设置html的`font-size`？
    rem就是根元素（即：html）的字体大小。html中的所有标签样式凡是涉及到尺寸的（如：`height`,`width`,`padding`,`margin`,`font-size`。甚至，`left`,`top`等）你都可以放心大胆的用rem作单位。如果你把html的`font-size`设为20px，前面说过，rem就是html的字体大小，那么1rem = 20px 但是这样的话计算特别麻烦，所以我们一般采用1rem=100px。
*   为什么不设置成1rem=1px不是更好计算？
    浏览器一般都有最小字体限制，比如谷歌浏览器，最小中文字体就是12px，所以实际上没有办法让1rem=1px。

## [](#rem布局方式 (@media篇))rem布局方式 (`@media`篇)

> 引入如下的css,一般我们在做web app都会先统计自己网站有哪些主流的屏幕设备，然后去针对那些设备去做media query设置也可以实现适配.原理和上述JS的原理相同，这种方式只适配了主流的浏览器。而上述所有设备都可以适配。CSS如下：

```
html {
  font-size: 100px; }

body {
  font-size: 16px; }

@media screen and (min-width: 320px) {
  html {
    font-size: 42.66667px; } }

@media screen and (min-width: 360px) {
  html {
    font-size: 48px; } }

@media screen and (min-width: 375px) {
  html {
    font-size: 50px; } }

@media screen and (min-width: 412px) {
  html {
    font-size: 54.93333px; } }

@media screen and (min-width: 414px) {
  html {
    font-size: 55.2px; } }

```
