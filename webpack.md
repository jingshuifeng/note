# Vue.js - day05



## 前端工程化

通俗来说前端工程化就是把一整套前端工作流程中能用工具搞定的部分，用工具搞定。

比如：

以前创建配置初始项目文件结构和基本文件，以前靠复制，现在输入命令自动生成。

以前校验 JS 文件是否规范，你可能复制一下放到 jshint 上校验一下，现在配置 grunt/gulp/webpack 监听文件变动自动校验显示校验结果。

以前修改代码查看效果，要手动刷新浏览器，现在有一大堆插件可以监听文件变动自动刷新。

以前压缩合并文件用手工复制到压缩工具然后复制到一个文件里面，现在配置一下 grunt /gulp/webpack等自动监听文件变动，自动合并压缩。

以前发布到服务器上，要手动使用 FTP 软件上传，现在也可以用工具自动打包上传。

。。。。。

把这些玩意规范一下，给一堆通用的命令来调用这些功能，就是前端工程化。



[拓展阅读](https://www.zhihu.com/question/24558375)



## webpack基本概念

### 什么是Webpack

WebPack可以看做是**模块打包机**：它做的事情是，分析你的项目结构，找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言（Scss，TypeScript等），并将其打包为合适的格式以供浏览器使用。

### 为什要使用WebPack

今的很多网页其实可以看做是功能丰富的应用，它们拥有着复杂的JavaScript代码和一大堆依赖包。为了简化开发的复杂度，前端社区涌现出了很多好的实践方法

1. 模块化，让我们可以把复杂的程序细化为小的文件;
2. ES6，7，8，9，10甚至更新的语法，让我们在开发时，可以使用更为简洁的语法，实现更加强大的功能；
3. 类似于TypeScript这种在JavaScript基础上拓展的开发语言：使我们能够实现目前版本的JavaScript不能直接使用的特性，并且之后还能能装换为JavaScript文件使浏览器可以识别；
4. scss，less等CSS预处理器

.........

这些改进确实大大的提高了我们的开发效率，但是利用它们开发的文件往往需要进行额外的处理才能让浏览器识别,而手动处理又是非常繁琐的，这就为WebPack类的工具的出现提供了需求。

### WebPack和Grunt以及Gulp相比有什么特性

在webpack之前其实流行过一些其他的工具，比如Grunt，Gulp

1. Gulp/Grunt是一种能够优化前端的开发流程的工具
2. 而WebPack是一种模块化的解决方案

从设计目来看其实Webpack和另外两个并没有太多的可比性，不过Webpack的优点使得Webpack可以替代Gulp/Grunt类的工具。

Grunt和Gulp的工作方式是：在一个配置文件中，指明对某些文件进行类似编译，组合，压缩等任务的具体步骤，这个工具之后可以自动替你完成这些任务。

Webpack的工作方式是：**把你的项目当做一个整体，通过一个给定的主文件（如：index.js），Webpack将从这个文件开始找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个浏览器可识别的JavaScript文件。**



## webpack基本使用

[官方文档](https://www.webpackjs.com/)

[入门指南](https://www.webpackjs.com/guides/)

### 起步

[传送门](https://www.webpackjs.com/guides/getting-started/)

1. 新建文件夹`webpack-demo`
2. 初始化npm
3. 本地安装`webpack`以及`webpack-cli`

```bash
npm init -y
npm install webpack webpack-cli --save-dev
```

### 项目结构

创建文件夹,文件 最终结果如下

![image-20190428210236080](Vue.js - day05.assets/image-20190428210236080.png)

index.js中代码如下

```js
// 操作body的样式
document.body.style.backgroundColor = 'hotpink'
```

index.html中代码如下

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

目前只是准备工作，并未开始进行打包

### 打包自己的js

打开终端，在终端中进入到`webpack-demo`文件夹,输入命令

```bash
npx webpack
```

稍等片刻，终端在应该会打印类似内容

![image-20190428210322408](Vue.js - day05.assets/image-20190428210357508.png)

打开dist文件夹，内部已经多了一个`main.js`文件

![image-20190428210402321](Vue.js - day05.assets/image-20190428210402321.png)

打开`index.html`增加引入`main.js`的代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
<!-- 导入生成的main.js -->
<script src="./main.js"></script>
```

打开浏览器，会发现浏览器已经变色了，换句话说js文件生效啦

![image-20190428210546382](Vue.js - day05.assets/image-20190428210546382.png)

你可以多写一些其他的js进去，测试效果



### 使用模块

为了体现`webpack`是模块打包机的特点，我们安装并使用一个第三方模块进行测试

1. 在终端中输入命令 安装jQuery
2. 在index.js中导入jQuery
3. 使用jQuery修改body的内容
4. 重新打包

终端中
```bash
npm i jquery 
```
index.js中
```js
import $ from 'jquery'
// 操作body的样式
document.body.style.backgroundColor = 'hotpink'
$('body').html("<h2>黑马程序员</h2>")
```

终端中

```
npx webpack
```

等待中出现提示信息，然后刷新浏览器，会看到如下结果:页面中多了一个h2标签，换句话说代码生效了

![image-20190428211046486](Vue.js - day05.assets/image-20190428211046486.png)

### 使用配置文件

为什么输入`npx webpack`他就会按照index.js中的内容进行打包，以及为什么打包之后的文件去到了dist目录下，这是因为`webpack`默认的设置就是这样，如果想要自己定制，可以在项目中创建一个`webpack.config.js`作为配置文件

新建文件

![image-20190428211911440](Vue.js - day05.assets/image-20190428211911440.png)



webpack.config.js中的代码

```js
const path = require("path")

module.exports = {
  // 打包的入口文件
  entry: "./src/index.js",
  // 打包的出口文件
  output: {
    // 打包之后的文件名
    filename: "main.js",
    // 打包之后保存的文件夹
    path: path.resolve(__dirname, "dist")
  }
}

```

接下来 我们可以在打包的时候指定使用这个配置

```bash
npx webpack --config webpack.config.js
```

因为配置的内容和之前没有任何区别，所以结果一直，大伙可以根据注释修改文件，重新打包进行尝试

### npm脚本

通过指定配置文件，可以进行入口以及出口的配置，但是每次打包都需要输入这么说内容十分不便，我们可以通过**npm脚本**简化这个操作

1. 打开package.json
2. 找到scripts分类
3. 增加build 选项

```diff
  {
    "name": "webpack-demo",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
+     "build": "webpack --config webpack.config.js"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "devDependencies": {
      "webpack": "^4.0.1",
      "webpack-cli": "^2.0.9",
      "lodash": "^4.17.5"
    }
  }
```

接下来输入在终端中输入如下代码，就等同于`npx webpack --config webpack.config.js`

```bash
npm run build
```



### 打包css

webpack是一个模块打包工具，但是他默认只能打包js，如果要能够识别其他的文件类型，需要安装对应的loader，接下来我们先演示如何打包css

1. 在src下新建css文件夹
2. 新增base.css，编写样式
3. 在index.js中导入base.css
4. 安装`style-loader`和`css-loader`
5. 修改`webpack.config.js`增加`loader`的配置
6. 打包并查看结果

![image-20190428212928714](Vue.js - day05.assets/image-20190428212928714.png)

/src/css/base.css中代码

```css
h2{
    color:yellow;
}
```

/src/index.js中代码

```js
import $ from 'jquery'
import './css/base.css'
// 操作body的样式
document.body.style.backgroundColor = 'hotpink'
$('body').html("<h2>黑马程序员</h2>")
```

终端中执行

```base
npm install --save-dev style-loader css-loader
```

/webpack.config.js中代码

```js
const path = require("path");

module.exports = {
  // 打包的入口文件
  entry: "./src/index.js",
  // 打包的出口文件
  output: {
    // 打包之后的文件名
    filename: "main.js",
    // 打包之后保存的文件夹
    path: path.resolve(__dirname, "dist")
  },
  // 项目中模块的处理配置
  module: {
    // 不同文件的处理规则
    rules: [
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  }
};

```

执行打包命令

```bash
npm run build
```

等待打包成功之后，打开浏览器，查看结果，会发现样式已经生效了

![image-20190428213653511](Vue.js - day05.assets/image-20190428213653511.png)

![image-20190428213634773](Vue.js - day05.assets/image-20190428213634773.png)

### 打包其他文件

`webpack`默认只能打包js文件，之前打包css文件需要通过loader以及修改配置来实现，如果要打包其他的文件，比如`less`,`sass`,`vue`…也需要安装对应的loader，并且修改配置，因为步骤完全一致，对应的loader名以及配置方式可以直接通过文档c+v，这里直接附上文档地址

[loaders](https://www.webpackjs.com/loaders/)

需要打包什么文件，找到对应的loader即可



### 开发服务器

目前每次打包都需要自己运行命令，十分费时费力，我们可以通过配置`webpack-dev-server`来实现检测文件变更，自动刷新浏览器

1. 安装`webpack-dev-server`
2. 修改配置文件
3. 增加npm脚本
4. 运行npm脚本

通过如下命令安装`webpack-dev-server`

```bash
npm install --save-dev webpack-dev-server
```

`webpack.config.js`修改为 

```js
const path = require("path");

module.exports = {
  // 打包的入口文件
  entry: "./src/index.js",
  // 打包的出口文件
  output: {
    // 打包之后的文件名
    filename: "main.js",
    // 打包之后保存的文件夹
    path: path.resolve(__dirname, "dist")
  },
  // 开发服务器配置
  devServer: {
    // 网站根目录
    contentBase: "./dist"
  },
  // 项目中模块的处理配置
  module: {
    // 不同文件的处理规则
    rules: [
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  }
};

```

`package.json`增加npm脚本

```json
{
  "name": "webpack-demo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --config webpack.config.js",
    "serve": "webpack-dev-server --open"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "css-loader": "^2.1.1",
    "style-loader": "^0.23.1",
    "webpack": "^4.30.0",
    "webpack-cli": "^3.3.1"
  },
  "dependencies": {
    "jquery": "^3.4.0"
  }
}

```

终端中输入命令

```bash
npm run serve
```

尝试修改index.js以及base.css保存之后会发现浏览器自动刷新，



1. 打包js
2. 打包css
3. 编译scss
4. 编译less
5. 检测文件更改
6. 自动打开服务器
7. 自动刷新浏览器
8. 合并文件
9. 压缩文件

## vue-loader

### 什么是vue-loader

[传送门](https://vue-loader.vuejs.org/zh/#vue-loader-%E6%98%AF%E4%BB%80%E4%B9%88%EF%BC%9F)

Vue Loader 是一个 [webpack](https://webpack.js.org/) 的 loader，它允许你以一种名为[单文件组件 (SFCs)](https://vue-loader.vuejs.org/zh/spec.html)的格式撰写 Vue 组件：

```vue
<template>
  <div class="example">{{ msg }}</div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Hello world!'
    }
  }
}
</script>

<style>
.example {
  color: red;
}
</style>
```

### 自己配置

你应该将 `vue-loader` 和 `vue-template-compiler` 一起安装——除非你是使用自行 fork 版本的 Vue 模板编译器的高阶用户：

```bash
npm install -D vue-loader vue-template-compiler
```

`vue-template-compiler` 需要独立安装的原因是你可以单独指定其版本。

每个 `vue` 包的新版本发布时，一个相应版本的 `vue-template-compiler` 也会随之发布。编译器的版本必须和基本的 `vue` 包保持同步，这样 `vue-loader` 就会生成兼容运行时的代码。这意味着**你每次升级项目中的 vue 包时，也应该匹配升级 vue-template-compiler。**

### [#](https://vue-loader.vuejs.org/zh/guide/#webpack-配置)webpack 配置

Vue Loader 的配置和其它的 loader 不太一样。除了通过一条规则将 `vue-loader` 应用到所有扩展名为 `.vue` 的文件上之外，请确保在你的 webpack 配置中添加 Vue Loader 的插件：

```js
// webpack.config.js
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
  module: {
    rules: [
      // ... 其它规则
      {
        test: /\.vue$/,
        loader: 'vue-loader'
      }
    ]
  },
  plugins: [
    // 请确保引入这个插件！
    new VueLoaderPlugin()
  ]
}
```

**这个插件是必须的！** 它的职责是将你定义过的其它规则复制并应用到 `.vue` 文件里相应语言的块。例如，如果你有一条匹配 `/\.js$/` 的规则，那么它会应用到 `.vue` 文件里的 `<script>` 块。



##  Vue CLI

如果你不想手动设置 webpack，我们推荐使用 [Vue CLI](https://github.com/vuejs/vue-cli) 直接创建一个项目的脚手架。通过 Vue CLI 创建的项目会针对多数常见的开发需求进行预先配置，做到开箱即用。

如果 Vue CLI 提供的内建没有满足你的需求，或者你乐于从零开始创建你自己的 webpack 配置，那么请继续阅读这篇指南。

### Vue-cli基本使用
Node 版本要求

Vue CLI 需要 Node.js 8.9 或更高版本 (推荐 8.11.0+)。你可以使用 nvm 或 nvm-windows 在同一台电脑中管理多个 Node 版本。

可以使用下列任一命令安装这个新的包：

```bash
npm install -g @vue/cli

yarn global add @vue/cli
```


安装之后，你就可以在命令行中访问 vue 命令。你可以通过简单运行 vue，看看是否展示出了一份所有可用命令的帮助信息，来验证它是否安装成功。

你还可以用这个命令来检查其版本是否正确 (3.x)：

```bash
vue --version
```



###  vue create

运行以下命令来创建一个新项目：然后一路回车即可

```bash
vue create hello-world
```



稍等片刻项目创建好了之后，我们日常编码的位置就是src下面的文件哈