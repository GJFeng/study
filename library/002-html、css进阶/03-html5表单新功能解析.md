# [](#html5表单新功能解析)html5表单新功能解析

> HTML表单一直都是Web的核心技术之一，有了它我们才能在Web上进行各种各样的应用,才能和服务器进行方便快捷的交互。HTML5 Forms新增了许多新控件及其API，方便我们做更复杂的应用，而不用借助其它前端脚本语言(如:javascript),极大的解放了我们的双手。

## [](#表单结构更自由)表单结构更自由

*   XHTML中需要放在form之中的诸如inpu/button/s人员配置:elect/textarea等标签元素，在HTML5中完全可以放在页面任何位置，然后通过新增的form属性指向元素所属表单的ID值，即可关联起来

```
<form id="myform"></form>
<input type="text" form="myform" value="">

```

## [](#多样的输入方式)多样的输入方式

### [](#email输入类型)email输入类型

> 说明：此类型要求输入格式正确的email地址,否则浏览器是不允许提交的,并会有一个错误信息提示,此类型必须指定name值,否则无效果.

```
<input type=email name=email>

```

### [](#url输入类型)url输入类型

> 要求输入格式正确的URL地址,Opera中会自动在开始处添加http://.

```
<input type=url name=url>

```

### [](#日期输入相关的类型)日期输入相关的类型

> 这一系列是很酷的一个类型,完全解决了烦琐的JS日历控件问题.但目前MS只有Opera/Chrome新版本支持,且展示效果也不一样..

```
<input type=date name=date>
<input type=time name=time>
<input type=month name=month>
<input type=week name=week>
<input type=datetime name=datetime>
<input type=datetime-local name=datetime-local>

```

### [](#number输入类型)number输入类型

> 输入一个数字字符,若未输入则会抛出一个错误

```
<input type=number max=10 min=0 step=1 value=5/>

```

| 属性 | 值 | 描述 |
| --- | --- | --- |
| max | number | 规定允许的最大值 |
| mub | number | 规定允许的最小值 |
| step | number | 规定合法的数字间隔 （如果 step="3"，则合法的数是 -3,0,3,6 等） |
| value | number | 规定默认值 |

### [](#range滑块类型)range滑块类型

> 特定值的范围的数值，以滑动条显示

```
<input type=range max=10 min=0 step=1 value=5/>

```

| 属性 | 值 | 描述 |
| --- | --- | --- |
| max | number | 规定允许的最大值 |
| mub | number | 规定允许的最小值 |
| step | number | 规定合法的数字间隔 （如果 step="3"，则合法的数是 -3,0,3,6 等） |
| value | number | 规定默认值 |

### [](#search输入类型)search输入类型

> 此类型表示输入的将是一个搜索关键字

```
<input type=search name=search >

```

### [](#tel输入类型)tel输入类型

> 此类型要求输入一个电话号码,但实际上它并没有特殊的验证,与text类型没什么区别.

```
<input type=tel name=tel >

```

### [](#color输入类型)color输入类型

> 说明：此类型表单,可让用户通过颜色选择器选择一个颜色值,并反馈到该控件的value值中

```
<input type=color name=color>

```

## [](#新增的属性)新增的属性

### [](#placeholder属性)placeholder属性

> 说明：这是一个很实用的属性,免去了用JS去实现点击清除表单初始值.浏览器支持也还不错,MS除了Firefox,其他标准浏览器都能很好的支持.

```
<input id=placeholder placeholder="点击我会以清除">

```

### [](#required/pattern属性)required/pattern属性

> 这是html5新加的验证属性 required类型，值不能为空，并会有一个提示。有两种写法，这个很有用。并且可以用于textarea以及hidden/image/submit类型 pattern类型为正则验证，可以完成各种复杂的验证。这两种类型必须指定name值，否则无效果。

```
<input id=placeholder name=require required>
<input id=placeholder name=require1 required="required">
<input name=require2 pattern="^[1-9]\d{5}$">

```

### [](#autofocus自动聚焦属性)autofocus自动聚焦属性

> 自动聚焦属性,可在页面加载时聚焦到一个表单控件,类似于js的focus()

```
<input autofocus=true >

```

### [](#autocomplete自动完成属性)autocomplete自动完成属性

> 此属性是为表单提供自动完成功能。如果该属性为打开状态可很好地自动完成。一般来说，此属性必须启动浏览器的自动完成功能。

```
<input autocomplete=on/off>

```

### [](#novalidate 属性)novalidate 属性

> novalidate 属性规定在提交表单时不应该验证 form 或 input 域。

```
<form action=demo_form.asp method=get novalidate=true>

```

### [](#multiple 属性)multiple 属性

> multiple 属性规定输入域中可选择多个.multiple 属性适用于以下类型的 `<input>` 标签：email 和 file。

```
<input type=file name=img multiple=multiple />

```

### [](#表单重写属性)表单重写属性

> 表单重写属性（form override attributes）允许您重写 form 元素的某些属性设定。表单重写属性适用于以下类型的 `<input>`标签：submit
>
> ```
> formaction - 重写表单的 action 属性
> formenctype - 重写表单的 enctype 属性
> formmethod - 重写表单的 method 属性
> formnovalidate - 重写表单的 novalidate 属性
> formtarget - 重写表单的 target 属性
>
> ```

### [](#list属性)list属性

> list 属性引用数据列表，其中包含输入字段的预定义选项。

```
<form action>
Webpage: <input type=url list=url_list name=link />
<datalist id=url_list>
  <option label=uek value=uek/>
  <option label=sxuek value=sxuek />
  <option label=tyuek value=tyuek />
</datalist>
<input type=submit />
</form>

```
