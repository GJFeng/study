> 1.  [什么是webpack](#什么是webpack "什么是webpack")
> 2.  [Webpack 的特点](#Webpack 的特点 "Webpack 的特点")
> 3.  [开始使用](#开始使用 "开始使用")
>     1.  [安装](#安装 "安装")
>     2.  [使用](#使用 "使用")
>     3.  [Loader](#Loader "Loader")
>     4.  [配置文件](#配置文件 "配置文件")
> 4.  [插件（Plugins）](#插件（Plugins） "插件（Plugins）")
>     1.  [HtmlWebpackPlugin](#HtmlWebpackPlugin "HtmlWebpackPlugin")
>     2.  [ExtractTextPlugin](#ExtractTextPlugin "ExtractTextPlugin")
>     3.  [合并公共代码](#合并公共代码 "合并公共代码")
>     4.  [代码压缩](#代码压缩 "代码压缩")
> 5.  [其他用法](#其他用法 "其他用法")
>     1.  [缓存](#缓存 "缓存")
>     2.  [去除多个文件中的频繁依赖](#去除多个文件中的频繁依赖 "去除多个文件中的频繁依赖")
>     3.  [设置环境命令](#设置环境命令 "设置环境命令")
>     4.  [常用命令](#常用命令 "常用命令")
> 6.  [目录结构](#目录结构 "目录结构")
> 7.  [使用webpack构建本地服务器](#使用webpack构建本地服务器 "使用webpack构建本地服务器")

# [](#Webpack使用指南)[Webpack使用指南](http://zhaoda.net/webpack-handbook/module-system.html)

> Webpack 是当下最热门的前端资源模块化管理和打包工具。

## [](#什么是webpack)什么是webpack

Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。通过 loader 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等。

![](http://webpackdoc.com/images/what-is-webpack.png)

## [](#Webpack 的特点)Webpack 的特点

Webpack 和其他模块化工具有什么区别呢？

*   代码拆分
    Webpack 有两种组织模块依赖的方式，同步和异步。异步依赖作为分割点，形成一个新的块。在优化了依赖树后，每一个异步区块都作为一个文件被打包。
*   Loader
    Webpack 本身只能处理原生的 JavaScript 模块，但是 loader 转换器可以将各种类型的资源转换成 JavaScript 模块。这样，任何资源都可以成为 Webpack 可以处理的模块。
*   智能解析
    Webpack 有一个智能解析器，几乎可以处理任何第三方库，无论它们的模块形式是 CommonJS、 AMD 还是普通的 JS 文件。甚至在加载依赖的时候，允许使用动态表达式 require("./templates/" + name + ".jade")。
*   插件系统
    Webpack 还有一个功能丰富的插件系统。大多数内容功能都是基于这个插件系统运行的，还可以开发和使用开源的 Webpack 插件，来满足各式各样的需求。
*   快速运行
    Webpack 使用异步 I/O 和多级缓存提高运行效率，这使得 Webpack 能够以令人难以置信的速度快速增量编译。

## [](#开始使用)开始使用

### [](#安装)安装

首先要安装 Node.js， Node.js 自带了软件包管理器 npm，Webpack可以通过npm去安装。

用 npm 安装 Webpack：

```
$ npm install webpack -g

```

此时 Webpack 已经安装到了全局环境下，可以通过命令行 webpack -h 试试。

通常我们会将 Webpack 安装到项目的依赖中，这样就可以使用项目本地版本的 Webpack。

```
# 进入项目目录
# 确定已经有 package.json，没有就通过 npm init 创建
# 安装 webpack 依赖
$ npm install webpack --save-dev

```

查看webpack

```
# 查看 webpack 版本信息
$ npm info webpack

```

安装指定版本的 webpack

```
$ npm install webpack@1.12.x --save-dev

```

如果需要使用 Webpack 开发工具，要单独安装：

```
$ npm install webpack-dev-server --save-dev

```

### [](#使用)使用

首先创建一个静态页面 index.html 和一个 JS 入口文件 entry.js：

```
<!-- index.html -->
<html>
<head>
  <meta charset="utf-8">
</head>
<body>
  <script src="bundle.js"></script>
</body>
</html>

```

```
// entry.js
document.write('It works.')

```

然后编译 entry.js 并打包到 bundle.js：

```
$ webpack entry.js bundle.js

```

打包过程会显示日志：

```
Hash: e964f90ec65eb2c29bb9
Version: webpack 1.12.2
Time: 54ms
    Asset     Size  Chunks             Chunk Names
bundle.js  1.42 kB       0  [emitted]  main
   [0] ./entry.js 27 bytes {0} [built]

```

用浏览器打开 index.html 将会看到 It works. 。 接下来添加一个模块 module.js 并修改入口 entry.js：

```
// module.js
module.exports = 'It works from module.js.'

```

```
// entry.js
document.write('It works.')
document.write(require('./module.js')) // 添加模块

```

重新打包 webpack entry.js bundle.js 后刷新页面看到变化

```
It works.It works from module.js.
Hash: 279c7601d5d08396e751
Version: webpack 1.12.2
Time: 63ms
    Asset     Size  Chunks             Chunk Names
bundle.js  1.57 kB       0  [emitted]  main
   [0] ./entry.js 66 bytes {0} [built]
   [1] ./module.js 43 bytes {0} [built]

```

Webpack 会分析入口文件，解析包含依赖关系的各个文件。这些文件（模块）都打包到 bundle.js 。Webpack 会给每个模块分配一个唯一的 id 并通过这个 id 索引和访问模块。在页面启动时，会先执行 entry.js 中的代码，其它模块会在运行 require 的时候再执行。

### [](#Loader)Loader

Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用 loader 进行转换。

Loader 可以理解为是模块和资源的转换器，它本身是一个函数，接受源文件作为参数，返回转换的结果。这样，我们就可以通过 require 来加载任何类型的模块或文件，比如 CoffeeScript、 JSX、 LESS 或图片。

先来看看 loader 有哪些特性？

*   Loader 可以通过管道方式链式调用，每个 loader 可以把资源转换成任意格式并传递给下一个 loader ，但是最后一个 loader 必须返回 JavaScript。
*   Loader 可以同步或异步执行。
*   Loader 运行在 node.js 环境中，所以可以做任何可能的事情。
*   Loader 可以接受参数，以此来传递配置项给 loader。
*   Loader 可以通过文件扩展名（或正则表达式）绑定给不同类型的文件。
*   Loader 可以通过 npm 发布和安装。
*   除了通过 package.json 的 main 指定，通常的模块也可以导出一个 loader 来使用。
*   Loader 可以访问配置。
*   插件可以让 loader 拥有更多特性。
*   Loader 可以分发出附加的任意文件。

loader 一般以 `xxx-loader` 的方式命名，xxx 代表了这个 loader 要做的转换功能，比如 `json-loader`。

Loader 可以在 require() 引用模块的时候添加，也可以在 webpack 全局配置中进行绑定，还可以通过命令行的方式使用。

接上一节的例子，我们要在页面中引入一个 CSS 文件 style.css，首页将 style.css 也看成是一个模块，然后用 css-loader 来读取它，再用 style-loader 把它插入到页面中。

```
/* style.css */
body { background: yellow; }

```

修改 entry.js：

```
require("!style!css!./style.css") // 载入 style.css
document.write('It works.')
document.write(require('./module.js'))

```

安装 loader：

```
npm install css-loader style-loader

```

重新编译打包，刷新页面，就可以看到黄色的页面背景了。

如果每次 require CSS 文件的时候都要写 loader 前缀，是一件很繁琐的事情。我们可以根据模块类型（扩展名）来自动绑定需要的 loader。

将 entry.js 中的 `require("!style!css!./style.css")` 修改为 `require("./style.css")` ，然后执行：

```
$ webpack entry.js bundle.js --module-bind 'css=style!css'

```

```
# 有些环境下可能需要使用双引号
$ webpack entry.js bundle.js --module-bind "css=style!css"

```

显然，这两种使用 loader 的方式，效果是一样的。

### [](#配置文件)配置文件

Webpack 在执行的时候，除了在命令行传入参数，还可以通过指定的配置文件来执行。默认情况下，会搜索当前目录的 webpack.config.js 文件，这个文件是一个 node.js 模块，返回一个 json 格式的配置信息对象，或者通过 --config 选项来指定配置文件。

#### 示例

创建一个配置文件 webpack.config.js：

```
var webpack = require('webpack')

module.exports = {
  entry: './entry.js',
  output: {
    path: __dirname,
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {test: /\.css$/, loader: 'style!css'}
    ]
  }
}

```

#### webpack.config.js参数详解

webpack.config.js文件通常放在项目的根目录中，它本身也是一个标准的Commonjs规范的模块。在导出的配置对象中有几个关键的参数：

#### entry

entry参数定义了打包后的入口文件，有三种写法，每个入口称为一个chunk:

| 类型 | 示例 | 解释 |
| --- | --- | --- |
| 字符串 | entry: "./index/index.js" | 配置模块会被解析为模块，并在启动时加载。
chunk名为默认为main， 具体打包文件名视output配置而定。 |
| 数组 | entry: ['./src/mod1.js', [...,] './src/index.js'] | 所有的模块会在启动时 按照配置顺序
加载，合并到最后一个模块会被导出。chunk名默认为main |
| 对象 | entry:{index: '...', login : [...]} | 如果传入`Object`,则会生成多个入口打包文件
`key`是`chunk`名，`value`可以是字符串，也可是数组。 |

```
{
    entry: {
        page1: "./page1",

        //支持数组形式，将加载数组中的所有模块，但以最后一个模块作为输出
        page2: ["./entry1", "./entry2"]
    },
    output: {
        path: "dist/js/page",
        publicPath: "/output/",
        filename: "[name].bundle.js"
    }
}

```

该段代码最终会生成一个 page1.bundle.js 和 page2.bundle.js，并存放到 ./dist/js/page 文件夹下

#### output

output参数是个对象，定义了输出文件的位置及名字：

```
output: {
        path: "dist/js/page",
        publicPath: "/output/",
        filename: "[name].bundle.js"
    }

```

*   **path**: 打包文件存放的绝对路径
*   **publicPath**: 网站运行时的访问路径
*   **filename**:打包后的文件名

当我们在entry中定义构建多个文件时，filename可以对应的更改为[name].js用于定义不同文件构建后的名字。

#### module

在webpack中JavaScript，CSS，LESS，TypeScript，JSX，CoffeeScript，图片等静态文件都是模块，不同模块的加载是通过模块加载器（webpack-loader）来统一管理的。loaders之间是可以串联的，一个加载器的输出可以作为下一个加载器的输入，最终返回到JavaScript上： loader使用需要先安装再加入到配置下中。

Loaders需要单独安装并且需要在webpack.config.js下的modules关键字下进行配置，Loaders的配置选项包括以下几方面：

*   test：一个匹配loaders所处理的文件的拓展名的正则表达式（必须）
*   loader：loader的名称（必须）
*   include/exclude:手动添加必须处理的文件（文件夹）或屏蔽不需要处理的文件（文件夹）（可选）；
*   query：为loaders提供额外的设置选项（可选）

##### loaders之 预处理

*   css-loader 处理css中路径引用等问题
*   style-loader 动态把样式写入css
*   sass-loader scss编译器
*   less-loader less编译器
*   postcss-loader scss再处理 

```
module: {
        //加载器配置
        loaders: [
            //.css 文件使用 style-loader 和 css-loader 来处理
            { test: /\.css$/, loader: 'style-loader!css-loader' },
            //.less 文件使用 less-loader、cssloader来编译
            { test:/\.less$/, loader: 'style!less'}
            //.scss 文件使用 style-loader、css-loader 和 sass-loader 来编译处理
            { test: /\.scss$/, loader: 'style!css!sass?sourceMap'},

        ]
    }

```

##### loaders之 js处理

babel-loader [babel官网](http://babeljs.cn/)

```
// npm一次性安装多个依赖模块，模块之间用空格隔开
npm install --save-dev babel-core babel-loader babel-preset-es2015 babel-preset-react

```

```
module: {
  loaders: [
    {
        test:/\.jsx?$/,
        exclude:/node_modules/,
        loader:'babel',
        query:{presets:['react','es2015']}
    }
  ]
}

```

##### loaders之 图片处理

*   url-loader

```
npm install --save-dev url-loadr

```

```
module: {
  loaders: [
    {
      test: /\.(png|jpg|gif)$/,
      loader: 'url-loader?limit=10000&name=build/images/[name].[ext]'
    }
  ]
}

```

对于上面的配置，如果图片资源小于10kb就会转化成 base64 格式的 dataUrl，其他的图片会存放在build/images文件夹下。

##### loaders之 文件处理

*   file-loader 

```
npm install --save-dev file-loader

```

```
module: {
  loaders: [
    {
      test: /\.(png|jpg|jpeg|gif|svg|woff|woff2|ttf|eot)$/,
      loader: 'file'
      },
  ]
}

```

#### 示例

```
module: {
        //加载器配置
        loaders: [
            //.css 文件使用 style-loader 和 css-loader 来处理
            { test: /\.css$/, loader: 'style-loader!css-loader' },

            //.scss 文件使用 style-loader、css-loader 和 sass-loader 来编译处理
            { test: /\.scss$/, loader: 'style!css!sass?sourceMap'},

            //图片文件使用 url-loader 来处理，小于8kb的直接转为base64
            { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'}
        ]
    }

```

## [](#插件（Plugins）)插件（Plugins）

插件（Plugins）是用来拓展Webpack功能的，它们会在整个构建过程中生效，执行相关的任务。

Webpack有很多内置插件，同时也有很多第三方插件，可以让我们完成更加丰富的功能。

#### 使用插件的方法

要使用某个插件，我们需要通过npm安装它，然后要做的就是在webpack配置中的plugins关键字部分添加该插件的一个实例（plugins是一个数组）继续看例子，我们添加了一个实现版权声明的插件。

```
module.exports = {
  plugins: [
    new webpack.BannerPlugin("Copyright Nico inc.")
    //在这个数组中new一个就可以了
  ]
}

```

### [](#HtmlWebpackPlugin)HtmlWebpackPlugin

这个插件的作用是依据一个简单的模板，帮你生成最终的HTML5文件，这个文件中自动引用了你打包后的JS文件。每次编译都在文件名中插入一个不同的哈希值。

安装

```
npm install --save-dev html-webpack-plugin

```

这个插件自动完成了我们之前手动做的一些事情，在正式使用之前需要对一直以来的项目结构做一些改变：

在app目录下，创建一个Html文件模板，这个模板包含title等其它你需要的元素，在编译过程中，本插件会依据此模板生成最终的html页面，会自动添加所依赖的 css, js，favicon等文件，在本例中我们命名模板文件名称为index.tmpl.html，模板源代码如下

index.tmpl.html

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Webpack</title>
  </head>
  <body>
    <div id='box'>
    </div>
  </body>
</html>

```

webpack.config.js

```
var webpack = require('webpack');
var HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
    plugins: [
    new HtmlWebpackPlugin({
      template: __dirname + "/app/index.tmpl.html"//new 一个这个插件的实例，并传入相关的参数
    })
  ]
}

```

### [](#ExtractTextPlugin)ExtractTextPlugin

分离CSS和JS文件

安装

```
npm install --save-dev extract-text-webpack-plugin

```

webpack.config.js

```
var webpack = require('webpack');
var ExtractTextPlugin = require('extract-text-webpack-plugin');
    ...
  plugins: [
    new HtmlWebpackPlugin({
      template: __dirname + "/app/index.tmpl.html"
    }),
    new webpack.optimize.OccurenceOrderPlugin(),
    new webpack.optimize.UglifyJsPlugin(),
    new ExtractTextPlugin("style.css")
  ]
}

```

### [](#合并公共代码)合并公共代码

项目中，对于一些常用的组件，站点公用模块经常需要与其他逻辑分开，然后合并到同一个文件，以便于长时间的缓存。要实现这一功能，配置参照:

```
var webpack = require('webpack');
var CommonsChunkPlugin = webpack.optimize.CommonsChunkPlugin;

···
entry: {
   a: './index/a.js',
   b: './idnex/b.js',
   c: './index/c.js',
   d: './index/d.js'
},
···
plugins: [
   new CommonsChunkPlugin('part.js', ['a', 'b']),
   new CommonsChunkPlugin('common.js', ['part1', 'c'])
]
···

```

### [](#代码压缩)代码压缩

webpack 自带了一个压缩插件 UglifyJsPlugin，只需要在配置文件中引入即可。

```
{
  plugins: [
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false
      }
    })
  ]
}

```

加入了这个插件之后，编译的速度会明显变慢，所以一般只在生产环境启用。

## [](#其他用法)其他用法

### [](#缓存)缓存

缓存无处不在，使用缓存的最好方法是保证你的文件名和文件内容是匹配的（内容改变，名称相应改变） webpack可以把一个哈希值添加到打包的文件名中，使用方法如下,添加特殊的字符串混合体（[name], [id] and [hash]）到输出文件名前

```
var webpack = require('webpack');
var HtmlWebpackPlugin = require('html-webpack-plugin');
var ExtractTextPlugin = require('extract-text-webpack-plugin');

module.exports = {
  entry: __dirname + "/app/main.js",
  output: {
    path: __dirname + "/build",
    filename: "[name]-[hash].js"
  },
  module: {},
  plugins: [
    new HtmlWebpackPlugin({
      template: __dirname + "/app/index.tmpl.html"
    }),
    new webpack.optimize.OccurenceOrderPlugin(),
    new webpack.optimize.UglifyJsPlugin(),
    new ExtractTextPlugin("[name]-[hash].css")
  ]
}

```

### [](#去除多个文件中的频繁依赖)去除多个文件中的频繁依赖

当我们经常使用React、jQuery等外部第三方库的时候，通常在每个业务逻辑JS中都会遇到这些库。  如我们需要在各个文件中都是有jQuery的$对象，因此我们需要在每个用到jQuery的JS文件的头部通过require('jquery')来依赖jQuery。 这样做非常繁琐且重复，因此webpack提供了我们一种比较高效的方法，我们可以通过在配置文件中配置使用到的变量名，那么webpack会自动分析，并且在编译时帮我们完成这些依赖的引入。

webpack.config.js中

```
var webpack = require('webpack');

...
plugins: [
   new webpack.ProvidePlugin({
       'Moment': 'moment',
       "$": "jquery",
       "jQuery": "jquery",
       "window.jQuery": "jquery",
       "React": "react"
   })
]
...

```

### [](#设置环境命令)设置环境命令

要告诉webpack我们希望当前是什么环境，只需要在命令中写入 BUILD_DEV=1 webpck 那么webpack通过配置，就会将所有我们引用到的**DEV**变量设置为true。

我们可以在package.json中事先定义好命令：

```
"scripts": {
    "dev": "BUILD_DEV=1 webpack-dev-server --progress --colors",
    "build": "BUILD_PRERELEASE=1 webpack -p"
}

```

那么就可以避免输入冗长的命令了：

开发时输入：

```
npm run dev

```

发布时输入:

```
npm run build

```

### [](#常用命令)常用命令

 webpack的使用和browserify有些类似，下面列举几个常用命令：

```
webpack 最基本的启动webpack命令
webpack -w 提供watch方法，实时进行打包更新
webpack -p 对打包后的文件进行压缩
webpack -d 提供SourceMaps，方便调试
webpack --colors 输出结果带彩色，比如：会用红色显示耗时较长的步骤
webpack --profile 输出性能数据，可以看到每一步的耗时
webpack --display-modules 默认情况下 node_modules 下的模块会被隐藏，加上这个参数可以显示这些被隐藏的模块

```

## [](#目录结构)目录结构

```
/
 ├── shell/ 脚本
 │
 ├── conf/ 工程配置
 │
 ├── src/ 开发目录
 │      ├── components/ 组件
 │      ├── pages/ 页面
 │      ├──
 ├── dist/ 自动生成
 │
 ├── test/ 测试
 │
 ├── node_modules/ 自动生成，包含.Node 依赖以及开发依赖
 │
 ├── static/ 库文件等，不会被webpack的loader处理,手动管理
 │
 └── etc

```

完整的目录结构：

```
projectTemplate/  
    ├── shell/    node脚本    
    │    ├──
    │    ├── dev-server.js  本地开发服务器
    │    ├── build.js  打包脚本
    │    ├── utils.js  工具函数
    │    ├──        
    ├── conf/     工程配置  
    │    ├──
    │    ├── index.js  基础配置文件，在此可简单的修改webpack相关配置
    │    ├── webpack.base.js  webpack的基础配置，主要是loader、resolve的配置
    │    ├── webpack.dev.js  webpack开发配置，主要是eslint、livereload、hot module replacement及相关的插件
    │    ├── webpack.prod.js  webpack生产配置，主要是代码的压缩混淆，图片压缩，加hash
    │    ├── karma.conf.js  测试配置
    │    ├──
    ├── src/   开发目录
    │     ├── components/   组件
    │     ├── pages/        页面（页面下的项目目录需要遵循一定的规范以便创建webpack的入口文件，不过这些规范是可以调整的；以下只是推荐）
    │           ├── index/   首页
    │                ├── images/  图片资源
    │                ├── page.css 样式文件，文件名称可以按照自己意愿命名
    │                ├── page.js  脚本文件及webpack的入口文件，文件名称可以在/conf/index.js配置
    │                ├── template.html 模板文件及要撰写的html文件，文件名称可以在/conf/index.js配置
    │                ├──
    │              
    ├── dist/      自动生成
    │      
    ├── test/      测试（目录可以意愿来创建，但是测试文件名称必须遵循*_test.js的命名规范，可在/conf/karma.conf.js修改配置）
    │  
    ├── node_modules/     自动生成，包含node依赖以及开发依赖
    │  
    ├── static/           库文件等，不会被webpack的loader处理,手动管理
    │     
    └── etc

```

## [](#使用webpack构建本地服务器)使用webpack构建本地服务器

想不想让你的浏览器监测你都代码的修改，并自动刷新修改后的结果，其实Webpack提供一个可选的本地开发服务器，这个本地服务器基于node.js构建，可以实现你想要的这些功能，不过它是一个单独的组件，在webpack中进行配置之前需要单独安装它作为项目依赖

```
npm install --save-dev webpack-dev-server

```

devserver作为webpack配置选项中的一项，具有以下配置选项

| devserver配置选项 | 功能描述 |
| --- | --- |
| contentBase | 默认webpack-dev-server会为根文件夹提供本地服务器，
如果想为另外一个目录下的文件提供本地服务器，
应该在这里设置其所在目录（本例设置到“public"目录） |
| port | 设置默认监听端口，如果省略，默认为”8080“ |
| inline | 设置为true，当源文件改变时会自动刷新页面 |
| colors | 设置为true，使终端输出的文件为彩色的 |
| historyApiFallback | 在开发单页应用时非常有用，它依赖于HTML5 history API，
如果设置为true，所有的跳转将指向index.html |

如下配置：

```
module.exports = {
    ...
    devServer: {
    contentBase: "./public",//本地服务器所加载的页面所在的目录
    colors: true,//终端中输出结果为彩色
    historyApiFallback: true,//不跳转
    inline: true//实时刷新
  }
}

```
