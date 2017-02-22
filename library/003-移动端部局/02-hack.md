# [](#移动端布局常见问题)移动端布局常见问题

## [](#横竖屏限制问题)横竖屏限制问题

```
  <meta name="x5-orientation" content="portrait | landscape" />

```

> 只支持x5内核

```
  <meta name="screen-orientation" content="portrait">

```

> 只支持uc浏览器

## [](#全屏限制问题)全屏限制问题

```
  <meta name="x5-fullscreen" content="true" />

```

> 只支持x5内核

```
  <meta name="full-screen" content="yes">

```

> 只支持uc浏览器

## [](#禁止识别电话号码和邮箱)禁止识别电话号码和邮箱

```
  <meta name="format-detection" content="telephone=no, email=no" />

```

> 禁止识别后页面当中所有的邮箱和电话将不会识别,如果有特殊需求,要配合一下代码实现

```
  <a href="tel:110">请拨打电话110</a>
  <a href="mailto:qq@.com">请发送邮件qq@.com</a>

```

## [](#消除链接\表单\按钮 默认背景)消除链接\表单\按钮 默认背景

```
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);

```

## [](#消除按钮圆角)消除按钮圆角

```
  -webkit-appearance: none;

```

## [](#移动端字体)移动端字体

*   ios系统
    *   默认中文字体是Heiti SC
    *   默认英文字体是Helvetica
    *   默认数字字体是HelveticaNeue
    *   无微软雅黑字体
*   android 系统
    *   默认中文字体是Droidsansfallback
    *   默认英文和数字字体是Droid Sans
    *   无微软雅黑字体
*   winphone 系统
    *   默认中文字体是Dengxian(方正等线体)
    *   默认英文和数字字体是Segoe
    *   无微软雅黑字体
*   结论
    *   各个手机系统有自己的默认字体，且都不支持微软雅黑
    *   如无特殊需求，手机端无需定义中文字体，使用系统默认
    *   英文字体和数字字体可使用 Helvetica ，三种系统都支持

```
  body{font-family:Helvetica;}

```

## [](#禁止用户设置字体大小)禁止用户设置字体大小

```
 -webkit-text-size-adjust:100%

```

## [](#禁止文字选中)禁止文字选中

```
  -webkit-user-select:none  //安卓不支持

```

## [](#字体增强 font boosting)字体增强 font boosting

> 移动端设备为了使用户能看清楚大批量的字体,会自动对字体进行放大,但是只要指定了容器的高度,就能解决

```
  p{max-height:9999999px}

```

## [](#调用原生滚动事件)调用原生滚动事件

```
 -webkit-overflow-scrolling:touch

```

## [](#CSS动画页面闪白,动画卡顿)CSS动画页面闪白,动画卡顿

> 解决方法:
>
> *   尽可能地使用合成属性transform和opacity来设计CSS3动画，不使用position的left和top来定位
> *   使用 CSS3 动画的时尽量利用3D加速，从而使得动画变得流畅。动画过程中的动画闪白可以通过 backface-visibility 隐藏

```
  -webkit-transform: translate3d(0, 0, 0);transform: translate3d(0, 0, 0);

```

## [](#fixed定位缺陷)fixed定位缺陷

*   ios下fixed元素容易定位出错，软键盘弹出时，影响fixed元素定位
*   android下fixed表现要比iOS更好，软键盘弹出时，不会影响fixed元素定位
*   ios4下不支持position:fixed

> 解决方案： 可用iScroll插件解决这个问题

## [](#阻止旋转屏幕时自动调整字体大小)阻止旋转屏幕时自动调整字体大小

```
  html, body, form, fieldset, p, div, h1, h2, h3, h4, h5, h6 {-webkit-text-size-adjust:none;}

```

## [](#上下拉动滚动条时卡顿、慢)上下拉动滚动条时卡顿、慢

```
body {-webkit-overflow-scrolling:touch; overflow-scrolling: touch;}

```

> Android3+和iOS5+支持CSS3的新属性为overflow-scrolling

## [](#禁止复制、选中文本)禁止复制、选中文本

```
  -webkit-user-select:none;user-select:none;

```

> 解决移动设备可选中页面文本(视产品需要而定)

## [](#ios和android下触摸元素时出现半透明灰色遮罩)ios和android下触摸元素时出现半透明灰色遮罩

```
  -webkit-tap-highlight-color:rgba(255,255,255,0)

```

> 设置alpha值为0就可以去除半透明灰色遮罩，备注：transparent的属性值在android下无效。

## [](#关于 iOS 与 OS X 端字体的优化(横竖屏会出现字体加粗不一致等))关于 iOS 与 OS X 端字体的优化(横竖屏会出现字体加粗不一致等)

> iOS 浏览器横屏时会重置字体大小，设置 text-size-adjust 为 none 可以解决 iOS 上的问题，但桌面版 Safari 的字体缩放功能会失效，因此最佳方案是将 text-size-adjust 为 100% 。

```
  -webkit-text-size-adjust: 100%;
  text-size-adjust: 100%;

```
