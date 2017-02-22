## [](#overflow)overflow

> 有时候，子元素的宽高会超出父元素的尺寸，我们需要对超出的内容做一些设置。

| 属性值 | 描述 |
| --- | --- |
| hidden | 将超出的内容隐藏 |
| visible | 全部显示内容 |
| auto | 根据实际情况做出调整，如果说没有超出那么正常显示，否则将会出现滚动条。 |
| scroll | 始终出现滚动条 |

## [](#visibility)visibility

> 主要是控制元素的隐藏和显示状态,想当于opacity的0和1状态。

| 属性值 | 描述 |
| --- | --- |
| visible | 当前元素为显示状态 |
| hidden | 当前元素为隐藏状态 |

## [](#overflow、display、visibility)overflow、display、visibility

> 三个属性设置为隐藏状态时的区别

| 属性 | 描述 |
| --- | --- |
| overflow | 只是对超出容器的内容进行处理 |
| display | 整个元素的显示状态是不可见的,浏览器会认为这个元素不存在。 |
| visibility | 浏览器认为该元素存在，但是不显示出来，所有该隐藏的元素还会占据原有的位置 |

## [](#改变尺寸 resize)改变尺寸 resize

> 主要处理textarea的缩放

| 属性值 | 描述 |
| --- | --- |
| none | 不能拖动 |
| both | 任意拖动 |
| horizontal | 水平拖动 |
| vertical | 垂直拖动 |

## [](#CSS 背景)CSS 背景

> 主要用于给一个元素添加盒子模型的填充。盒子模型默认的背景色是透明的。

| 属性 | 描述 | 值 |
| --- | --- | --- |
| background-color | 背景颜色 | rgb,十六进制,英文单词 |
| background-image | 背景图片 | url(地址) |
| background-repeat | 设置背景平铺重复方向 | no-repeat,repeat-x,repeat-y |
| background-attachment | 设置背景图像是随对象内容滚动还是固定 | scroll,fixed |
| background-position | 设置背景图像位置。 | top,right,bottom,left,center,百分比,数值 |

`background: #ffffff url(uek.png) no-repeat left content fixed; 依次：颜色-背景图-平铺-背景图像位置-固定`

## [](#CSS背景之Sprite技术)CSS背景之Sprite技术

> 也叫做css背景图片精灵技术实现的方式：是将多张背景图片放到一个图片当中，通过定位的方式来获得相应位置的图片，使得一个图片一次载入，多次使用，使得页面的下载速度加快！
> 核心技术:background-position

![tushi](amWiki/images/sp.png)

## [](#CSS列表属性)CSS列表属性

### [](#列表样式类型属性 list-style-type)列表样式类型属性 list-style-type

| 属性值 | 描述 | 属性值 | 描述 | 属性值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| disc | 缺省值，黑圆点 | circle | 空心圆点 | none | 无列表项标记 |
| square | 小黑方块 | decimal | 数字排序 | upper-alpha | 大写字母排序 |
| lower-roman | 小写罗马字排序 | upper-roman | 大写罗马字排序 | lower-alpha | 小写字母排序 |

### [](#列表样式位置属性 list-style-position)列表样式位置属性 list-style-position

| 属性值 | 描述 |
| --- | --- |
| outside | 以列表项内容为准对齐 |
| inside | 以列表项标记为准对齐 |

### [](#列表样式图片属性 list-style-image)列表样式图片属性 list-style-image

> 列表项标记可以用图片来表示 `list-style-image:url(uek.png)`

### [](#列表样式实例)列表样式实例

```
  ul{
    list-style:circle inside url(uek.png)
  }

```

## [](#透明度)透明度

> 在前端处理时经常会用到透明色的处理，但是在IE与标准的CSS规范中使用是不同的

| 标准 | 属性 | 属性值 |
| --- | --- | --- |
| w3c | opacity | 0~1 |
| ie | filter:alpha(opacity = num) | 0~100 |

```
div{
  opacity:0.5;
  filter:alpha(opacity=50);
}

```

## [](#鼠标样式)鼠标样式

> 用于展示在鼠标的不同状态时候的样式。

| 属性值 | 描述 | 属性值 | 描述 |
| --- | --- | --- | --- |
| hand,pointer | 手型。推荐pointer | w-resize | 向左的箭头 |
| crosshair | 是十字型 | sw-resize | 左下的箭头 |
| text | 移动到文本上的那种效果 | sw-resize | 左下的箭头 |
| wait | 等待的那种效果 | s-resize | 向下的箭头 |
| default | 默认效果 | se-resize | 向右下的箭头 |
| help | 问号 | auto | 由系统自动给出效果 |
| e-resize | 向右的箭头 | n-resize | 向上的箭头 |
| ne-resize | 向右上的箭头 | nw-resize | 向左上的箭头 |

## [](#table设定样式)table设定样式

> 设定table表格的细胞边框是否合并，每一个td的宽度是否是固定的大小，以及表头的位置

| 属性 | 描述 | 值 |
| --- | --- | --- |
| border-collapse | 指定边框是否合并 | separate,collapse |
| table-layout | 固定或自动宽度 | fixed,auto |
| caption-side | 标题的位置 | top,left,right,bottom |
