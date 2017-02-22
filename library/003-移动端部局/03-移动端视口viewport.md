# [](#viewport)viewport

> viewport就是设备的屏幕上能用来显示我们的网页的那一块区域

## [](#viewport的三种分类)viewport的三种分类

*   layout viewport 默认的布局视口
    移动端设备的屏幕不是很宽,但是又想完整的呈现各种页面(pc端的页面),所以移动端浏览器把视口默认的定义为一个较宽的值,一般为980px,可以通过`document.documentElement.clientWidth`获取到,
    但是一般布局视口都会比我们的屏幕大,所以会出现滚动条,用户体验很不友好,于是出现了visual viewport ![图示](amWiki/images/iphone.png)

*   visual viewport 视觉视口
    一般来说视觉视口,就是我们移动设备屏幕的大小`window.innerWidth`,我们都知道移动设备的屏幕尺寸小于桌面端的屏幕尺寸,那么要想在有限的窗口内表达更多的像素, 移动端的设备就必须要通过物理手段来解决,在有限的屏幕内显示更多的像素点,于是就有了各种高清屏,比方说2k\4k\视网膜屏等,这些设备的dpi很高,dpi指的就是屏幕像素密度,我们也叫做物理像素,比方说:安卓分为ldpi、mdpi、hdpi、xhdpi等不同的等级,而css所表示的一个像素我们叫做独立像素 像素比:`devicePixelRatio = 物理像素 / 独立像素`,可以通过`window.devicePixelRatio` 获取,不过有些浏览器不支持,在有的浏览器里面会用物理像素表示独立像素,有的浏览器里面会用独立像素单独表示,就会出现要不然很小,要不然很大的情况.如何解决这个问题:浏览器帮我们创建了一个理想视觉窗口,让我们可以自己定义该视口有多大,并且强制用独立像素来表达
    ![图示](amWiki/images/iphone1.png)

*   ideal viewport 理想视口
    现在越来越多的网站都会为移动设备进行单独的设计，所以必须还要有一个能完美适配移动设备的viewport。所谓的完美适配指的是，首先不需要用户缩放和横向滚动条就能正常的查看网站的所有内容；第二，显示的文字的大小是合适，比如一段14px大小的文字，不会因为在一个高密度像素的屏幕里显示得太小而无法看清，理想的情况是这段14px的文字无论是在何种密度屏幕，何种分辨率下，显示出来的大小都是差不多的。当然，不只是文字，其他元素像图片什么的也是这个道理。浏览器把这个viewport叫做 ideal viewport，也就是第三个viewport——移动设备的理想viewport。
    ideal viewport并没有一个固定的尺寸，不同的设备拥有有不同的ideal viewport。所有的iphone的ideal viewport宽度都是320px，无论它的屏幕宽度是320还是640，也就是说，在iphone中，css中的320px就代表iphone屏幕的宽度。
    但是安卓设备就比较复杂了，有320px的，有360px的，有384px的等等。
    ![图示](amWiki/images/iphone2.png)

## [](#利用meta标签对viewport进行控制)利用meta标签对viewport进行控制

*   移动设备默认的viewport是layout viewport，也就是那个比屏幕要宽的viewport，但在进行移动设备网站的开发时，我们需要的是ideal viewport。那么怎么才能得到ideal viewport呢？这就该轮到meta标签出场了。

```

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">

```

该meta标签的作用是让当前viewport的宽度等于设备的宽度，同时不允许用户手动缩放。也许允不允许用户缩放不同的网站有不同的要求，但让viewport的宽度等于设备的宽度，这个应该是大家都想要的效果，如果你不这样的设定的话，那就会使用那个比屏幕宽的默认viewport，也就是说会出现横向滚动条。
width 设置layout viewport 的宽度，为一个正整数，或字符串"width-device" initial-scale 设置页面的初始缩放值，为一个数字，可以带小数 minimum-scale 允许用户的最小缩放值，为一个数字，可以带小数 maximum-scale 允许用户的最大缩放值，为一个数字，可以带小数 height 设置layout viewport 的高度，这个属性对我们并不重要，很少使用 user-scalable 是否允许用户进行缩放，值为"no"或"yes", no 代表不允许，yes代表允许 这些属性可以同时使用，也可以单独使用或混合使用，多个属性同时使用时用逗号隔开就行了。

## [](#把当前的viewport宽度设置为 ideal viewport 的宽度)把当前的viewport宽度设置为 ideal viewport 的宽度

> 要得到ideal viewport就必须把默认的layout viewport的宽度设为移动设备的屏幕宽度。因为meta viewport中的width能控制layout viewport的宽度，所以我们只需要把width设为`device-width`这个特殊的值就行了。

```
<meta name="viewport" content="width=device-width, initial-scale=1">

```
