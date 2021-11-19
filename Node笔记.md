# Node开发

## Node简介

`Node.js` 诞生于 2009 年，由 `Joyent` 的员工 `Ryan Dahl` 开发而成, 目前官网最新版本已经更新到 12.0.0版本，最新稳定的是10.15.3。`Node.js` 不是一门语言也不是框架，它只是基于 `Google `V8`` 引擎的 `JavaScript` 运行时环境，同时结合 `Libuv `扩展了 `JavaScript` 功能，使之支持 `io`、`fs `等只有语言才有的特性，使得 `JavaScript` 能够同时具有 DOM 操作(浏览器)和 I/O、文件读写、操作数据库(服务器端)等能力，是目前最简单的全栈式语言。

这里我们可以简单理解 `Node.js`是一个内置有chrome `V8`引擎的 `JavaScript`运行环境，他可以使原本在浏览器中运行的 `JavaScript`有能力跑后端，从而操作我们数据库，进行文件读写等。

目前市面上高密集的I/O模型，比如 Web 开发，微服务，前端构建等都有做 `Node.js`的身影。不少大型网站都是使用 `Node.js` 作为后台开发语言的，比如 淘宝 双十一、去哪儿网 的 PC 端核心业务等。另外我们一些前端工具譬如 `VSCode`,`webpack`等也是有 `Node.js`开发。

`Node.js`的包管理工具，`npm`已经成为世界开源包管理中最大的生态，功能强大，目前单月使用者接近1000万。

### Node.js的特点

- 异步、非阻塞 IO 模型
- 事件循环
- 单线程
- 总结：轻量和高效

Node.js 的性能和效率非常高。

传统的 Java 语言是一个请求开启一个线程，当请求处理完毕后就关闭这个线程。而 Node.js 则完全没有采用这种模型，它本质上就是一个单线程。

你可能会疑问：一个线程如何服务于大量的请求、如何处理高并发的呢？这是因为，Node.js 采用的是异步的、非阻塞的模型。

这里所谓的“单线程”，指的是 Node 的主线程只有一个。为了确保主线程不被阻塞，主线程是用于接收客户端请求。但不会处理具体的任务。而 Node 的背后还有一个线程池，线程池会处理长时间运行的任务（比如 IO 操作、网络操作）。线程池里的任务是通过队列和事件循环的机制来执行。

### 使用 Node.js 时的劣势

- 程序运行不稳定，可能会出现服务不可用的情况
- 程序运行效率较低，每秒的请求数维持在一个较低的水平
- 前端同学对服务器端的技术不太熟悉。

### Node和JavaScript的区别

JavaScript：ecmascript/BOM/DOM，以及其他的内置对象（RegExp、Date、Math、...）

Node.js :

```
Ecmascript/Node提供的方法，没有DOM和BOM。（let、const、for、数据类型、表达式、运算符、函数、 class、RegExp、Date、Math、...）
```


```
Node.js 新增的 API，文件操作，HTTP 协议，Commonjs 模块化、npm 包工具等
```


在 Node.js 里运行 JavaScript，跟在 Chrome 里运行 JavaScript 有什么不同？

二者采用的是同样的 JS 引擎。在 Node.js 里写 JS，和在前端写 JS，几乎没有不同。在写法上的区别在于：Node.js 没有浏览器、页面标签相关的 API，但是新增了一些 Node.js 相关的 API。通俗来说，对于开发者而言，在前端写 JS 是用于控制浏览器；而 Node.js 环境写 JS 可以控制整个计算机。

如下图所示：

![](http://img.smyhvae.com/20200409_1545.png)

### 补充

### Node的应用领域

善于 I/O，不善于计算。因为 Node.js 最擅长的就是任务调度：

```
Web 服务 API（开发接口）
```


```
后端的 Web 服务，例如跨域、服务器端的请求
```


```
基于 Web 的动态网站应用
```


```
多客户端的通信，如即时通信（websocket）
```


```
基于node的前端工具
```


### 前端同学为什么要学习后端/后端同学为什么要学习前端

- 了解前后端交互流程。
- 前端同学能够和后台开发的程序员更佳紧密地结合、更顺畅地沟通。
- 当网站的业务逻辑需要前置时，前端人员需要学习一些后台开发的技术，以完成相应的任务；；反过来也一样。
- 拓宽知识视野和技术栈，能够站在全局的角度审视整个项目。

### 前端同学为什么要学 Node.js

1、Node.js 使用 JavaScript 语言开发服务器端应用，**便于前端同学上手**（一些公司甚至要求前端工程师掌握 Node.js 开发）。

2、实现了前后端的语法统一，**有利于和前端代码整合**，甚至共用部分代码。

比如说，针对接口返回的各种字段，前后端都必须要做校验。此时，如果用 Node.js 来做后台开发的话，前后端可以共用校验的代码。

3、Node.js 性能高、生态系统活跃，提供了大量的开源库。

4、Jeff Atwood 在 2007 年提出了著名的 Atwood 定律：**任何能够用 JavaScript 实现的应用系统，最终都必将用 JavaScript 实现**。 Jeff Atwood 是谁不重要（他是 Stack Overflow 网站的联合创始人），重要的是这条定律

## Node在一线企业中的运用

### 作为BFF中间层

BFF，即 Backend For Frontend（服务于前端的后端）。

在 Web 服务里，搭建一个中间层，前端访问中间层的接口，中间层再访问后台的 Java/C++ 服务。这类服务的特点是不需要太强的服务器运算能力，但对程序的灵活性有较高的要求。这两个特点，正好和 Node.js 的优势相吻合。Node.js 非常适合用来做 BFF 层，优势如下：

- 对于前端来说：让前端**有能力自由组装后台数据**，这样可以减少大量的业务沟通成本，加快业务的迭代速度；并且，前端同学能够**自主决定**与后台的通讯方式。
- 对于后台和运维来说，好处是：安全性（不会把主服务器暴露在外面）、降低主服务器的复杂度等。

我们通常说前端和后端，前端负责用户界面，而后端负责提供数据和业务接口。现在我们在两者间加入一层，前端并不是直接去请求后端业务接口，而是请求到中间层。再由中间层去请求业务接口。

整个流程可以描述为：客户端直接请求到中间层的 `Node`服务，`Node`服务分析请求，看需要哪个页面，再去请求对应数据，拿到数据后和模版结合成用户看到页面，再给到客户端。

那么有的人可能会觉得，这种模式不是更麻烦了吗？其实不然，我们来看看 **中间层的优点** ：

1. 减轻客户端内存，项目用户体验好。不会像 `mvvm`模式的项目把页面渲染和数据请求都压在客户端，而是在服务端完成。
2. `SEO`性好，不像 `mvvm`模式页面由 `js`生成，而是在服务器渲染好 `html`字符，有利于网页被搜索到。
3. 保持了前后端分离的优点和目的，即解放后端，后端可以继续以接口的形式写业务代码。
4. 前端可以操控的范围增多，甚至可以做服务器，数据库层面的优化，比如中间层中常常用 `nginx`，`redis`来优化项目，应对高并发。

中间层模式是一种开发模式上的进步，为什么这么好的模式我从来没有听说过呢？因为这种模式成本过高，如果没有一定量级的项目没必要去采用。

### 服务端渲染

**客户端渲染**（CSR / Client side render）：前端通过一大堆接口请求数据，然后通过 JS 动态处理和生成页面结构和展示。优点是**前后端分离**、减小服务器压力、局部刷新。缺点是不利于 SEO（如果你的页面然后通过 Ajax 异步获取内容，抓取工具并不会等待异步完成后再行抓取页面内容）、首屏渲染慢。

**服务端渲染**（SSR / Server Side Render）：服务器返回的不是接口数据，而是一整个页面（或整个楼层）的 HTML 字符串，浏览器直接显示即可。也就是说，在服务器端直接就渲染好了，然后一次性打包返回给前端。优点是**有利于 SEO、首屏渲染很快**。

**总结： 搜索引擎优化 + 首屏速度优化 = 服务端渲染**。

备注：这里的「服务端渲染」只是让 Node.js 做中间层，不会替代后端的，后台同学请放心。

### 做项目构建工具

这里说的项目构建工具，我相信大家都用过，我们的 ``webpack``，`vue-cli`都是输入项目构建工具。那么大家觉得这一类工具神奇好用方便的同时，有没有想过这些工具是拿什么语言写的？其实它们并不难，这些工具都是用 `Node`来写的。

很多公司都会开发自己公司的项目构建工具，帮助公司项目做的更标准更方便，一个好的项目构建工具，会极大的加快整个公司的项目开发效率。

这一类的项目构建工具一般都要很多的文件操作，`Node`对于i/o流的操作，在目前的主流后端语言中数一数二。所以越来越多的公司选择用 `Node`来做项目构建工具。

### 做一些小型网站后端

用 `Node`做后端，可能是大多数人认为的 `Node`作用。其实真正在企业之中，很少会让你去用 `Node`去做后端。 所以一般来说都是做一些小型或者个人站的后端。

*注意*

Node.js使得JavaScript可以脱离浏览器的窗口，独立运行在Node.js提供的环境中，所以Node.js中没有**BOM，DOM**这些概念。Node.js中根本没有页面，主要是进行一些服务器上的操作（比如：读写文件，网络通信...）。我们只需要基本的JavaScript语法基础（ES6）即可学习。

## 环境变量

环境变量是什么呢？其实我们可以把它理解为【系统的视线范围】，没错，配置进入了环境变量的程序，就等于是进入了系统的视线范围，打开DOS命令窗口后输入程序名，系统就会把在其视线内的（环境变量内）的程序找出来，如果程序没有配置进入环境的变量的话，那系统自然就找不到。

在没有配置node的环境变量前，我就只能在其node.exe所在目录下使用node，但是配置成功后我就可以在任何地方使用他了。现在我在c盘下直接使用node命令查看效果。

## 进程和线程

进程进程是资源(CPU、内存等)分配的基本单位，它是程序执行的一个实例，程序运行时系统就会创建一个进程，并为它分配资源，然后把该进程放入进程就绪队列（负责为程序运行提供一个必备的环境，可以把它比喻为工厂的车间)

线程是程序执行的最小单位，线程是进程的一个执行流，负责执行进程中的程序，相当于工厂中的工人

## NodeJs模块化规范

网站越来越复杂，js代码、js文件也越来越多，会遇到**一些问题**：

- 文件依赖
- 全局污染、命名冲突

程序模块化包括：

- 日期模块
- 数学计算模块
- 日志模块
- 登陆认证模块
- 报表展示模块等。

所有这些模块共同组成了程序软件系统。

一次编写，多次使用，才是提高效率的核心。

### 模块化的理解

#### 什么是模块化

**概念**：将一个复杂的程序依据一定的规则（规范）封装成几个块（文件），并组合在一起。

模块的内部数据、实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信。

最早的时候，我们会把所有的代码都写在一个js文件里，那么，耦合性会很高（关联性强），不利于维护；而且会造成全局污染，很容易命名冲突。

#### 模块化的好处

- 避免命名冲突，减少命名空间污染
- 降低耦合性；更好地分离、按需加载
- **高复用性**：代码方便重用，别人开发的模块直接拿过来就可以使用，不需要重复开发类似的功能。
- **高可维护性**：软件的声明周期中最长的阶段其实并不是开发阶段，而是维护阶段，需求变更比较频繁。使用模块化的开发，方式更容易维护。
- 部署方便

假设我们引入模块化，首先可能会想到的思路是：在一个文件中引入多个js文件。如下：

```html
<body>
    <script src="zepto.js"></script>
    <script src="fastClick.js"></script>
    <script src="util/login.js"></script>
    <script src="util/base.js"></script>
    <script src="util/city.js"></script>
</body>
```

但是这样做会带来很多问题：

- 请求过多：引入十个js文件，就有十次http请求。
- 依赖模糊：不同的js文件可能会相互依赖，如果改其中的一个文件，另外一个文件可能会报错。

以上两点，最终导致：**难以维护**。

于是，这就引入了模块化规范。

### 模块化的概念解读

模块化起源于 Node.js。Node.js 中把很多 js 打包成 package，需要的时候直接通过 require 的方式进行调用（CommonJS），这就是模块化的方式。

那如何把这种模块化思维应用到前端来呢？这就产生了两种伟大的 js：RequireJS 和 SeaJS。

### 模块化规范

服务器端规范：

- [**CommonJS规范**](http://www.commonjs.org/)：是 Node.js 使用的模块化规范。

CommonJS 就是一套约定标准，不是技术。用于约定我们的代码应该是怎样的一种结构。

浏览器端规范：

- [**AMD规范**](https://github.com/amdjs/amdjs-api)：是 **[RequireJS](http://requirejs.org/)** 在推广过程中对模块化定义的规范化产出。

```
- 异步加载模块；

- 依赖前置、提前执行：require([`foo`,`bar`],function(foo,bar){});   //也就是说把所有的包都 require 成功，再继续执行代码。

- define 定义模块：define([`require`,`foo`],function(){return});
```

- **[CMD规范]()**：是 **[SeaJS](http://seajs.org/)** 在推广过程中对模块化定义的规范化产出。淘宝团队开发。

```
  同步加载模块；

  依赖就近，延迟执行：require(./a) 直接引入。或者Require.async 异步引入。   //依赖就近：执行到这一部分的时候，再去加载对应的文件。

  define 定义模块， export 导出：define(function(require, export, module){});
```

PS：面试时，经常会问AMD 和 CMD 的区别。

另外，还有ES6规范：import & export。

我们来讲一下 `CommonJS`，它是 Node.js 使用的模块化规范。

### CommonJS 的介绍

ECMAScript标准的缺陷：

- 没有模块系统
- 标准库少
- 没有标准接口
- 缺乏管理系统

如果程序设计的规模达到了一定的程度，则必须对其进行模块化。模块化可以有多种形式，但至少应该提供将代码分割为多个源文件的机制，CommonJS的模块功能可以帮我们解决该问题。CommonJS规范的提出主要是为了弥补当前JavaScript没有标准的缺陷，CommonJS规范为JS指定了一个美好的愿景，希望JS能够在任何地方运行。

[CommonJS](http://www.commonjs.org/)：是 Node.js 使用的模块化规范。也就是说，Node.js 就是基于 CommonJS 这种模块化规范来编写的。

CommonJS对模块的定义十分简单：

- 模块引用
- 模块定义
- 模块标识

CommonJS 规范规定：每个模块内部，module 变量代表当前模块。这个变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口对象。加载某个模块，其实是加载该模块的 module.exports 对象。

在 CommonJS 中，每个JS文件都可以当作一个模块：

- 在服务器端：模块的加载是运行时同步加载的。
- 在浏览器端: 模块需要提前编译打包处理。首先，既然同步的，很容易引起阻塞；其次，浏览器不认识 `require`语法，因此，需要提前编译打包。

### 模块的暴露和引入

在node中，一个JS文件就是一个模块，每一个JS文件中的JS代码都是独立运行在一个函数中，而不是全局作用域，所以一个模块中的变量和函数在其他模块中无法访问，只能在当前模块被访问，这叫做模块作用域。

注意：暴露的原理：在一个自定义模块中，默认情况下，module.exports={ }，我们在外界使用require方法导入一个自定义模块的时候，得到的成员，其实就是module.exports所指向的这个对象。通过require方法导入的结果，永远以module.exports指向的对象为准！

```js
//在node中有一个全局对象global,他的作用和网页中的window类似,在全局中的变量都会作为global的属性保存,在全局中创建的函数都会作为global的方法保存。
var a = 10;
console.log(global.a)//前面添加var 不是一个全局变量 输出undefined
b=5;
console.log(global.b)//前面不加var或let 变成一个全局变量 输出5
//当node在执行模块中的代码时，他会首先在代码的最顶部添加如下代码
function(exports,require,module,__filename,__dirname){
//在代码的最底部，添加一个花括号
}
//NodeJs引擎在执行Js代码的时候用一个函数把它包起来了，并且在函数执行的时候，同时传递了5个实参
exports//该对象用来将变量或函数暴露到外部
require//用来引入外部模块
module//module代表的是当前模块本身，exports就是模块的属性
__filename//当前模块的完整路径
——dirname//文件所在文件夹的完整路径
```

Node.js 中只有模块级作用域，两个模块之间的变量、方法，默认是互不冲突，互不影响，这样就导致一个问题：模块 A 要怎样使用模块B中的变量&方法呢？这就需要通过 `exports` 关键字来实现。

Node.js中，每个模块都有一个 exports 接口对象，我们可以把公共的变量、方法挂载到这个接口对象中，其他的模块才可以使用。

接下来详细讲一讲模块的暴露、模块的引入。

### 暴露模块的方式一： module.exports

`module.exports`用来导出一个默认对象，没有指定对象名。

语法格式：

```javascript
// 方式一：导出整个 exports 对象
module.exports = value;

// 方式二：给 exports 对象添加属性
module.exports.xxx = value;
```

这个 value 可以是任意的数据类型。

代码举例：

```js
// 方式1
module.exports = {
    name: '我是 module1',
    foo(){
        console.log(this.name);
    }
}

// 我们不能再继续写 module.exports = value2。因为重新赋值，会把 exports 对象 之前的赋值覆盖掉。

// 方式2
const age = 28;
module.exports.age = age;

```

`module.exports` 还可以修改模块的原始导出对象。比如当前模块原本导出的是一个对象，我们可以通过 module.exports 修改为导出一个函数。如下：

```js
module.exports = function () {
    console.log('hello world')
}
```

### 暴露模块的方式二： exports

由于module.exports单词写起来较复杂，为了简化向外共享成员的代码，Node提供了exports对象，默认情况下，exports和module.exports指向的是同一个对象，但最终暴露的结果，还是以module.exports指向的对象为准！

`exports`对象用来导出当前模块的公共方法或属性，只需要将需要暴露的变量或方法设置为exports的属性，别的模块通过 require 函数调用当前模块时，得到的就是当前模块的 exports 对象。

**语法格式**：

```js
// 相当于是：给 exports 对象添加属性
exports.xxx = value
```

这个 value 可以是任意的数据类型。

**注意**：暴露的关键词是 `exports`，不是 `export`。其实，这里的 exports 类似于 ES6 中的 export 的用法，都是用来导出一个指定名字的对象。

**代码举例**：

```js
const name = 'qianguyihao';

const foo = function (value) {
	return value * 2;
};

exports.name = name;
exports.foo = foo;
```

### exports 和 module.exports 的区别

最重要的区别：

- 使用exports时，只能单个设置属性 `exports.a = a;`
- 使用module.exports时，既单个设置属性 `module.exports.a`，也可以整个赋值 `module.exports = obj`。

其他要点：

- Node中每个模块的最后，都会执行 `return: module.exports`。
- Node中每个模块都会把 `module.exports`指向的对象赋值给一个变量 `exports`，也就是说 `exports = module.exports`。
- `module.exports = XXX`，表示当前模块导出一个单一成员，结果就是XXX。
- 如果需要导出多个成员，则必须使用 `exports.add = XXX; exports.foo = XXX`。或者使用 `module.exports.add = XXX; module.export.foo = XXX`。

### export和module.exports的使用误区

```js
//案例一
export.username="美猴王"
module.exports={
    gender:"男",
    age:500
}
//最终暴露的是{gender:"男",age=500}

//案例二
module.exports.username="如来佛"
exports={
    gender:"男",
    age:10000
}
//最终暴露的结果是{username:"如来佛"}

//案例三
exports.username="菩提祖师"
module.exports.gender="男"
//最终暴露的结果是{username:"菩提祖师",gender:"男"}

//案例四
exports={
    username:"玉皇大帝",
    gender:"男"
}
module.exports=exports
module.exports.age=15000
//最终暴露的结果是{username:"玉皇大帝",gender:"男",age:15000}
//时刻谨记：	require()模块时，得到的永远是module.exports指向的对象
```

### 问题: 暴露的模块到底是谁？

**答案**：暴露的本质是 `exports`对象。【重要】

比如，方式一的 `exports.a = a` 可以理解成是，**给 exports 对象添加属性**。方式二的 `module.exports = a`可以理解成是给整个 exports 对象赋值。方式二的 `module.exports.c = c`可以理解成是给 exports 对象添加属性。

Node.js 中每个模块都有一个 module 对象，module 对象中的有一个 exports 属性称之为**接口对象**。我们需要把模块之间公共的方法或属性挂载在这个接口对象中，方便其他的模块使用。

### 引入模块的方式：require

require函数用来在一个模块中引入另外一个模块。传入模块名，返回模块导出对象。

**语法格式**：

```js
const module1 = require('模块名');
```

解释：

- 内置模块：require的是**包名**。
- 下载的第三方模块：require的是**包名**。
- 自定义模块：require的是**文件路径**。文件路径既可以用绝对路径，也可以用相对路径。后缀名 `.js`可以省略。

**代码举例**：

```js
const module1 = require('./main.js');
const module2 = require('./main');
const module3 = require('Demo/src/main.js');
```

**require()函数的两个作用**：

- 执行导入的模块中的代码。
- 返回导入模块中的接口对象。

### 包

Node.js中的第三方模块又被叫做包

就像电脑和计算机指的是相同的东西，第三方模块和包指的是同一个概念，只不过叫法不同。包是由第三方个人或团队开发出来的，免费供所有人使用。

由于Node.js的内置模块仅提供了一些底层的API，导致其在基于内置模块进行项目开发时，效率很低。包是基于内置模块封装出来的，提供了更加高级、更方便的API，极大的提高了开发效率。包和内置模块之间的关系，类似于jQuery和浏览器内置API之间的关系。

### 模块的加载机制

#### 优先从缓存中加载

模块在第一次加载后会被缓存，这也意味着多次调用require( )不会导致模块中的代码被执行多次

注意：不论是内置模块、用户自定义模块还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率

#### 内置模块的加载机制

内置模块是由Node.js官方提供的模块，内置模块的加载优先级最高

例如：require("fs")始终返回内置的fs模块，即使在node_modules目录下有名字相同的包也叫fs

#### 自定义模块的加载机制

使用require()加载自定义模块时，必须以./或../开头的路径标识符，在加载自定义模块时，如果没有指定这样的路径标识符，则node会把它当作内置模块或第三方模块进行加载。

同时，在使用require()导入自定义模块时，如果省略了文件的扩展名，则node.js会按顺序分别尝试加载以下文件：

- 按照确切的文件名进行加载
- 补全.js扩展名进行加载
- 不全.json扩展名进行加载
- 补全.node扩展名进行加载
- 加载失败，终端报错

####　加载第三方包的机制

```js
const express = require('express');
```

require 加载第三方包的机制：

（1）第三方包安装好后，这个包一般会存放在当前项目的 node_modules 文件夹中。我们找到这个包的 package.json 文件，并且找到里面的main属性对应的入口模块，这个入口模块就是这个包的入口文件。

（2）如果第三方包中没有找到package.json文件，或者package.json文件中没有main属性，则默认加载第三方包中的index.js文件。

（3）如果在 node_modules 文件夹中没有找到这个包，或者以上所有情况都没有找到，则会向上一级父级目录下查找node_modules文件夹，查找规则如上一致。

（4）如果一直找到该模块的磁盘根路径都没有找到，则会报错：can not find module xxx。

####　目录（文件夹）作为模块时的加载机制

把目录作为模块标识符,传递给require()进行加载时,有三种加载方式

- 在被加载的目录下查找一个叫做package.json的文件,并寻找main属性,作为require()加载的入口
- 如果目录里面没有package.json文件,后者main入口不存在或无法解析,则node.js将会试图加载目录下的index.js文件
- 如果以上两步都失败了,则node.js会报错

### 主模块

主模块是整个程序执行的入口，可以调度其他模块。

```bash
# 运行main.js启动程序。此时，main.js就是主模块
$ node main.js
```

### 模块的初始化

一个模块中的 JS 代码仅在模块**第一次被使用时**执行一次，并且在使用的过程中进行初始化，然后会被缓存起来，便于后续继续使用。

代码举例：

（1）calModule.js:

```js
var a = 1;

function add () {
  return ++a;
}

exports.add = add;

```

（2）main.js:在main.js中引入calModule.js模块

```js
var addModule1 = require('./calModule')
var addModule2 = require('./calModule')

console.log(addModule1.add());
console.log(addModule2.add());
```

在命令行执行 `node main.js` 运行程序，打印结果：

```bash
2
3
```

从打印结果中可以看出，`calModule.js`这个模块虽然被引用了两次，但只初始化了一次。

### CommonJS 在服务器端的实现举例

#### 初始化项目

在工程文件中新建如下目录和文件：

```
modules
    | module1.js
    | module2.js
    | module3.js

app.js
```

然后在根目录下新建如下命令：

```
  npm init
```

然后根据提示，依次输入如下内容：

- **包名**：可以自己起包名，也可以用默认的包名。注意，包名里不能有中文，不能有大写。
- **版本**：可以用默认的版本 1.0.0，也可以自己修改包名。

其他的参数，一路回车即可。效果如下：

![](http://img.smyhvae.com/20180410_1425.png)

于是，根目录下会自动生成 `package.json`这个文件。点进去看一下：

```json
{
  "name": "commonjs_node",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "smyhvae",
  "license": "ISC"
}

```

#### 导入第三方包

`uniq`这个第三方包的作用是保证唯一性（我们拿它来举例）。我们在当前工程目录下，输入如下命令进行安装：

```
  npm install uniq
```

安装成功后，根目录下会自动生成相应的文件：

![](http://img.smyhvae.com/20180410_1450.png)

需要说明的是，我的node版本是 v8.10.0（v8以上），对应的 npm 版本是 v5.6.0，版本比较高，因此，当我输入完 `npm install uniq`之后，`package.json`中就会自动添加 `uniq`包的依赖

如果有些童鞋的npm版本较低，就需要手动去添加依赖；另一种方式是，可以使用 `npm install uniq --save`命令，这个多出来的 `--save`就可以自动添加依赖。

我们去[官网](https://www.npmjs.com/package/uniq)看一下 `uniq`的用法：

```javascript
  let uniq = require('uniq');

  let arr = [1, 1, 2, 2, 3, 5];
  uniq(arr);
  console.log(arr);  //输出结果：[ 1, 2, 3, 5 ]

```

可以看出，这个包可以起到数组去重的作用。

#### 自定义模块

（1）module1.js：

```javascript
//暴露方式一：module.exports = value

//暴露一个对象出去
module.exports = {
    name: '我是 module1',
    foo(){
        console.log(this.name);
    }
}

//我们不能再继续写 module.exports = xxx。因为重新赋值，会把之前的赋值覆盖掉。

```

（2）module2.js：

```javascript
//暴露方式一：module.exports = value

//暴露一个函数出去
module.exports = function(){
    console.log('我是 module2');
}
```

注意，此时暴露出去的 exports 对象 等价于整个函数。

（3）module3.js：

```javascript
//暴露方式二：exports.xxx = value

//可以往 export 对象中不断地添加属性，进行暴露

exports.foo1 = function(){
    console.log('module3 中的 foo1 方法');
}

exports.foo2 = function(){
    console.log('module3 中的 foo2 方法');
}

exports.arr = [1,1,2,2,3,5,11];

```

（4）app.js：（将其他模块汇集到主模块）

```javascript
//将其他模块汇集到主模块

let uniq = require('uniq'); //引入时，第三方模块要放在自定义模块的上面

let module1 = require('./modules/module1');
let module2 = require('./modules/module2');
let module3 = require('./modules/module3');

//调用module1对象的方法
module1.foo();

//调用module2的函数
module2();  //注意，在定义时，module2对象等价于整个函数function。所以，module2()的意思是，直接调用了函数。

//调用module3中的属性
module3.foo1();
module3.foo2();

uniq(module3.arr); //将module3中的数组进行去重操作
console.log(module3.arr); //打印数组去重后的结果
```

这样的话，我们的代码就写完了。

我们在命令行中输入 `node app.js`，就可以把代码跑起来了。打印结果如下：

```bash
我是 module1
我是 module2
module3 中的 foo1 方法
module3 中的 foo2 方法
[ 1, 11, 2, 3, 5 ]

```

### CommonJS 基于浏览器端的实现举例

#### 初始化项目

在工程文件中新建如下目录和文件：

```
js
    dist //打包生成文件的目录
    src //源码所在的目录
      | module1.js
      | module2.js
      | module3.js
      | app.js //应用主源文件
index.html    //因为CommonJS是基于浏览器端，js文件要跑在浏览器的页面上，所以要有这个html页面
```

然后在根目录下新建如下命令：

```
  npm init
```

然后根据提示，依次输入如下内容：

- **包名**：可以自己起包名，也可以用默认的包名。注意，包名里不能有中文，不能有大写。
- **版本**：可以用默认的版本 1.0.0，也可以自己修改包名。

其他的参数，一路回车即可。

于是，根目录下会自动生成 `package.json`这个文件。点进去看一下：

```json
{
  "name": "commonjs_browser",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


```

#### 下载第三方包：Browserify

这里需要用到[Browserify](http://browserify.org/)这个工具进行编译打包。Browserify 称为 CommonJS 的浏览器端的打包工具。

输入如下命令进行安装：（两个命令都要输入）

```javascript
    npm install browserify -g          //全局
    npm install browserify --save-dev  //局部。
```

上面的代码中，`-dev`表示开发依赖。这里解释一下相关概念：

- 开发依赖：当前这个包，只在开发环境下使用。
- 运行依赖：当前这个包，是在生产环境下使用。

#### 自定义模块 & 代码运行

（1）module1.js：

```javascript
//暴露方式一：module.exports = value

//暴露一个对象出去
module.exports = {
    name: '我是 module1',
    foo(){
        console.log(this.name);
    }
}

//我们不能再继续写 module.exports = xxx。因为重新赋值，会把之前的赋值覆盖掉。

```

（2）module2.js：

```javascript
//暴露方式一：module.exports = value

//暴露一个函数出去
module.exports = function(){
    console.log('我是 module2');
}
```

注意，此时暴露出去的 exports 对象 等价于整个函数。

（3）module3.js：

```javascript
//暴露方式二：exports.xxx = value

//可以往export对象中不断地添加属性，进行暴露

exports.foo1 = function(){
    console.log('module3 中的 foo1 方法');
}

exports.foo2 = function(){
    console.log('module3 中的 foo2 方法');
}
```

（4）app.js：（将其他模块汇集到主模块）

```javascript
let module1 = require('./module1');  // ./ 指的是当前路径
let module2 = require('./module2');
let module3 = require('./module3');

module1.foo();
module2();
module3.foo1();
module3.foo2();
```

引入的路径解释：

- `./`是相对路径，指的是当前路径（app.js的当前路径是src）

到此，我们的主要代码就写完了。

但是，如果我们直接在index.html中，像下面这样写，是不行的：（因为浏览器不认识 require 关键字）

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
    <script src="./js/src/app.js"></script>
</body>
</html>

```

为了能够让index.html引入app.js，我们需要输入如下命令：

打包处理js:

```
    browserify js/src/app.js -o js/dist/bundle.js
```

然后在index.html中引入打包后的文件：

```html
    <script type="text/javascript" src="js/dist/bundle.js"></script>
```

## Buffer缓冲区

从结构上看Buffer非常像一个数组，操作方法也跟数组很像。数组中不能存储二进制的文件，而Buffer就是专门用来存储二进制数据的，但是是以十六进制形式显示的，使用buffer不需要引入直接使用即可。

```JS
let str = "hello Atguigu";
let buf = Buffer.from(str);
console.log(buf)//<Buffer 48 65 6c 6c 6f 20 41 74 67 75 69 67 75>
console.log(buf.length)//占用内存的大小
console.log(str.length)//字符串的长度
/*
    Buffer.from(str) 将一个字符串转换为Buffer
    Buffer.alloc(size) 创建一个指定大小的Buffer  Buffer的大小一旦被指定就是固定的 
    Buffer.alloUnsafe(size) 创建一个指定大小的Buffer 但是可能会泄露数据 
    Buffer.toString() 将缓冲区的数据转换为字符串
*/
```

## 文件系统模块

### 文件写入

在使用文件模块之前，记得先导入：

```js
// 导入文件模块
const fs = require('fs');
```

fs 的英文全称是 File System。fs 模块提供了很多 api 方法，我们首先应该学习的方法是文件写入。

fs模块中所有的操作都有两种形式可供选择，同步和异步：同步文件系统会阻塞程序的执行，也就是除非操作完毕，否则不会向下执行代码；异步文件系统不会阻塞程序的执行，而是在操作完成后通过回调函数将结果返回。

Node中文件写入的方式主要有以下几种。

#### 同步文件的写入 fs.writeSync()

语法格式：

```js
/*
    1、打开文件
        fs.openSync(path,flags,[mode])
        -path 要打开文件的路径
        -flags 打开文件要操作的类型 r-只读的 w-可写的
        -mode 设置文件的操作权限 一般不传
        返回值：
        -该方法会返回一个文件的描述符作为结果,我们可以通过该描述符来对文件进行各种操作
      2、向文件中写入内容
        fs.writeSync(fd,string,position,encoding)
        -fd 文件的描述符
        -string 要写入的内容
        -position 写入的起始位置 一般不传
        -encoding 写入的编码 默认是utf-8
      3、保存并关闭文件
        fs.closeSync 
 */
```

代码举例：

```javascript
let fs = require("fs")
let fd = fs.openSync("hello.txt","w")//第二个参数为w的时候会自动创建这个文件，不需要原本就有这个文件，第二个参数为r的时候就需要原本就有这个文件，否则会报错
fs.writeSync(fd,"今天天气真不错~~")
fs.closeSync(fd)
```

####　异步文件的写入fs.write()

语法格式：

```js
/*
    1、打开文件
        fs.open(path,flags,[mode],(err,fd)=>{})
        -用来打开一个文件
        -异步调用的方法，结果都是通过回调函数的参数返回
        -回调函数有两个参数
 			-err 错误对象，如果没有错误值是null
 			-fd 文件的描述符
      2、向文件中写入内容
        fs.write(fd,string,position,encoding,(err)=>{})
        -fd 文件的描述符
        -string 要写入的内容
        -position 写入的起始位置 一般不传
        -encoding 写入的编码 默认是utf-8
        -回调函数的参数只有err
      3、保存并关闭文件
        fs.closeSync 
 */
```

代码举例：

```javascript
let fs = require("fs")
fs.open("./data.txt", "w", (err, fd) => {
    if (!err) {
        fs.write(fd, "我们的目的一定会实现，我们的目的一定能够实现~~~", (err) => {
            if (!err) {
                console.log("写入成功~");
            } else {
                console.log(err);
            }
        })
        fs.close(fd,(arr)=>{
            if(!err){
                console.log("文件已经关闭成功~~~");
            }
        })
    } else {
        console.log(err);
    }
})
console.log("哈哈哈");//即使上面出现错误也能正常输出
```

#### 简单文件写入

```js
/*
	简单文件写入
    fs.writeFile(filePath,data,options{encoding,mode,flag},callback)
    	-filePath 要操作的文件的路径
    	-data 要写入的数据
    	-options 选项，可以对写入进行一些设置,默认设置了一般不填这个参数
    	-callback 当写入完成以后执行的函数
*/
let fs = require("fs")
fs.writeFile("./data.txt","哈哈哈",{encoding:'utf8',flag:"w"})
```

*注意*：文件的打开状态

| 模式 |                           说明                           |
| :--: | :------------------------------------------------------: |
|  r  |              读取文件，文件不存在则出现异常              |
|  r+  |              读写文件，文件不存在则出现异常              |
|  rs  |               在同步模式下打开文件用于读取               |
| rs+ |               在同步模式下打开文件用于读写               |
|  w  |   打开文件用于写操作，如果不存在则创建，如果存在则截断   |
|  wx  |   打开文件用于写操作，如果存在则打开失败（只能新创建）   |
|  w+  |    打开文件用于读写，如果不存在则创建，如果存在则截断    |
| wx+ |    打开文件用于读写，如果存在则打开失败（只能新创建）    |
|  a  |            打开文件用于追加，如果不存在则创建            |
|  ax  |    打开文件用于追加，如果路径存在则失败（只能新创建）    |
|  a+  |      打开文件用于读取和追加，如果不存在则创建该文件      |
| ax+ | 打开文件进行读取和追加，如果路径存在则失败（只能新创建） |

#### 流式文件的写入

同步、异步、简单文件的写入都不适合大文件的写入，性能较差，容易导致内存溢出

```js
let fs = require("fs")
//流式文件的写入
//创建一个可写流
//fs.createWriteStream(path,options)
let ws = fs.createWriteStream("./data.txt")
//可以通过监听流的open和close事件来监听流的打开和关闭
/*
 	on(事件字符串，回调函数)
 		-可以为对象绑定一个事件
    once(时间字符串,回调函数)
         -可以为对象绑定一个一次性事件，该事件将会在触发一次后自动失效
*/
ws.once("open",function(){
    console.log("流打开了~~~");
});
ws.once("close",function(){
    console.log("流关闭了~~~");
});
//通过ws向文件中写入内容
ws.write("锄禾日当午")
ws.write("今天天气真不错")
ws.write("红掌拨清波")
ws.write("日照香炉生紫烟")
ws.write("一日看遍长安花")
ws.close();//关闭文件
```

### 文件读取

```js
/*
    fs.readFile(path,options,callback)
     --path:相对路径，相对的是小黑屏命令行的路径
     --options:{encoding,flag,signal}
     --callback:(err,data)=>{}
        --err 错误对象
        --data 未指定encoding则返回buffer格式的数据
     为什么会默认返回buffer格式数据？
     因为读取的不一定是文字，还有可能是图片、音频、视频，buffer存储的是二进制数据，通用性更好~~~
*/
//简单文件读取
let fs = require("fs");
fs.readFile("../../../ftp信息.txt",(err, data) => {//这里的相对路径相对的式小黑屏的命令行的路径
    if (!err) {
        console.log("文件读取成功~~");
        fs.writeFile("./6.txt", data, (err) => {//文件存在则写入不存在则创建
            if (!err) {
                console.log("文件写入成功~~");
                console.log(data);
            }
        })
    } else {
        console.log(err);
    }
})
```

### 文件夹的操作

```js
//同步
let fs=require("fs")
//创建文件夹
/* let res=fs.mkdirSync("logs")
console.log(res);//undefined */
//删除文件夹
/* let res = fs.rmdirSync("./logs")
console.log(res);//undefined */
/* let res=fs.readdirSync("./练习");
console.log(res);//[ 'data.json', 'login.js', 'register.js', '要求.txt' ] */

//异步
let fs=require("fs")
//创建文件夹
/* fs.mkdir("log",(err)=>{
    if(err){
        throw err;
    }else{
        console.log("文件夹创建成功~~");
    }
}) */
//重命名文件夹
/* fs.rename("./log","./logs",(err)=>{
    if(!err){
        console.log("文件夹重命名成功~");
    }else{
        throw err;
    }
}) */
//删除文件夹
/* fs.rmdir("./logs",(err)=>{
    if (!err) {
        console.log("文件夹删除成功~~");
    }else{
        console.log(err);
    }
}) */
//读取文件夹
/* fs.readdir("./练习",(err,data)=>{
    if(!err){
        console.log(data);//[ 'data.json', 'login.js', 'register.js', '要求.txt' ]
    }else{
        console.log(err);
    }
}) */
```

### 路径拼接问题解决方案

在使用fs操作模块时候，如果提供的路径时以./或../开头的相对路径时，很容易出现路径动态拼接错误的问题，原因时代码在运行过程中，会以执行node命令时所处的目录，动态拼接出被操作文件的完整路径

解决方案：在使用fs模块操作文件时，直接提供完整路径，不要提供以./或../开头的相对路径，从而防止动态拼接的问题。但是直接填写绝对路径固然能解决拼接的问题，但是又会产生另外一个问题：移植性非常差。因此，node给我们提供了一个__dirname全局对象，表示当前文件所在的目录，使用代码实例如下：

```js
const fs = require("fs")
fs.readFile(__dirname + "\\学生成绩.txt", "utf-8", (err, result) => {
    if (!err) {
        console.log("读取成功~~");
        let res = result.split(" ")
        res.forEach((val) => {
            let newRes = val.replace("=", ":");
            fs.writeFile(__dirname + "\\成绩结果.txt", newRes + "\n", { encoding: "utf-8", flag: "a" }, (err) => {
                if (!err) {
                    console.log("写入成功");
                }
            })
        })
    } else {
        console.log("读取失败~~");
    }
})
```

## path路径模块

path模块是node.js官方提供的、用来处理路径的模块，他提供了一系列的方法和属性，用来满足用户对路径处理的需求

例如：

- path.join()方法，用来将多个路径片段拼接成一个完整的路径字符串
- path.basename()方法，用来从路径字符串中将文件名解析出来

如果需要在JavaScript中使用这个模块来处理路径，则需要使用以下方法导入这个模块

```js
const path=require("path")
```

### path.join( )语法格式

使用path.join()方法，可以把多个路径片段拼接成一个完整的路径字符串,语法格式如下

```js
//path.join(路径1，路径2，路径3 ...) 拼接路径
//../会抵消前面的一层路径
console.log(path.join("a\\b\\c\\d","e/f/g"));//a\b\c\d\e\f\g
console.log(path.join("a/b/c/d","e/f/g"));//a\b\c\d\e\f\g
console.log(path.join("a/b////c/d","e\\\\\\f\\g"));//a\b\c\d\e\f\g
console.log(path.join("a/b/c/d","./e/f/g"));//a\b\c\d\e\f\g
console.log(path.join("a/b/c/d","../e/f/g"));//a\b\c\e\f\g
```

### 获取路径中的文件名 basename( )方法

使用path.basename( )方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下

```js
//定义一个文件存放路径
const path = require("path")
const fpath = '/a/b/c/index.html'
const fileName = path.basename("fpath")
console.log(file.name)//index.html
//如果不希望获取到的文件名有扩展名，就可以传递第二个参数
const fileNameWithoutExt = path.basename("fpath",".html")
console.log(fileNameWithoutExt)//index
```

### 获取路径中的文件扩展名

使用path.extname( )方法，可以获取路径中文件名的扩展名部分，语法如下

```js
const fext = path.extname("fpath")
console.log(fext)//.html
```

## http模块

在网络节点中，负责消费资源的电脑，叫做客户端，负责对外提供网络资源的电脑叫做服务器。

http模块是Node.js官方提供的，用来创建web服务器的模块，通过http模块提供的http.createServer()方法，就能方便的把一台普通的电脑变成一台web服务器，从而对外提供web资源服务。如果要希望使用http模块创建web服务器就需要先导入它。

```js
const http = require("http")
```

服务器和普通电脑的区别就在于，服务器上安装了web服务器软件，例如IIS，Apache等，通过安装这些服务器软件就能把一台普通的电脑变成一台web服务器。在Node.js中，我们不需要使用IIS、Apache等这些第三方web服务器软件，因为我们可以基于Node.js提供的http模块，通过几行简单的代码就能轻松手写一个服务器软件，从而对外提供web服务。

### IP地址相关的概念

IP地址就是互联网上每台计算机的唯一标识，因此IP地址具有唯一性。如果把个人电脑比作一台电话，那么IP地址就相当于电话号码，只有在知道对方IP地址的前提下才能与对应的电脑之间进行数据通信。

IP地址的格式：通常用“点分十进制”表示成（a.b.c.d)的形式，其中，a，b，c，d都是0-255之间的十进制整数，例如点分十进制标识的IP地址(192.168.11)

注意：

- 互联网中每台web服务器都有自己的IP地址。例如大家可以在windows的终端中运行ping www.baidu.com命令，即可查看到百度服务器的IP地址。
- 在开发期间，自己的电脑既是一台服务器也是一个客户端，为了方便测试，可以在自己的浏览器中输入127.0.0.1这个IP地址，就能把自己的电脑当作一台服务器进行访问了。

### 域名和域名服务器

尽管IP地址能够唯一地标记网络上的计算机，但是IP地址是一长串数字，不直观，而且不便于记忆，于是人民又发明了字符型的地址方案，即所谓的域名(Domin Name)地址。

IP和域名是一一对应的关系，这份对应关系存放在一种叫域名服务器(DNS)的电脑中。使用者只需要通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，域名服务器就是提供IP地址和域名之间的转换的服务器。

注意：

- 单纯使用IP地址，互联网中的电脑也能正常工作。但是有了域名的加持，能然互联网的世界变得更加方便
- 在开发测试期间，127.0.0.1对应的域名是localhost，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。

### 端口号

计算机中的端口号，就好像是现实生活中的门牌号一样，通过门牌号，外卖小哥在整栋大楼众多的房间中，准确把外卖送到你的手中一样。同样的道理，在一台电脑中，可以运行成百上千个web服务，每个web服务器都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号就可以被准确地交给对应的web服务进行处理。

注意：每个端口号不能同时被多个web服务占用，在实际应用中，URL中的80端口可以被省略，因为在不写端口号的时候，80端口是很多web服务器的默认端口号。

### 创建最基本的web服务器

####　步骤１-导入http模块

如果希望在自己电脑上创建一个web服务器,从而对外提供web服务,则需要导入http模块:

```js
const http = require("http")
```

#### 步骤2-创建web服务器实例

调用http.createServer()方法,即可快速创建一个web服务器实例

```js
const server = http.createServer()
```

#### 步骤3-为服务器实例绑定request事件

为服务器绑定request事件,即可监听客户端发送过来的网络请求:

```js
//使用服务器的.on()方法,为服务器绑定一个request事件
server.on("request",(req,res)=>{
	//只要有客户端来请求我们自己的服务器,就会触发request事件,从而调用这个事件处理函数
	console.log("Someone visit our web server")
})
```

#### 步骤4-启动服务器

调用服务器实例的.listen()方法,即可启动当前的web服务器实例:

```js
server.listen(8080,()=>{
	console.log("http server is running at http://127.0.0.1:8080")
})
```

#### req请求对象

只要服务器接收到了客户端的请求,就会调用通过server.on()为服务器绑定的request事件处理函数,如果想在事件处理函数中访问与客户端相关的数据或属性,可以使用如下的方式:

```js
server.on("request",(req)=>{
	//req是请求对象,它包含了与客户端相关的数据和属性,例如
	//req.url是客户端请求的url地址
	//req.method是客户端的method请求类型
	console.log(req.url,req.method)
})
```

#### res响应对象

在服务器的request事件处理函数中,如果想访问与服务器相关的数据或属性,可以使用如下的方式:

```js
server.on("request",(req,res)=>{
	//res是响应对象,它包含了与服务器相关的数据或属性,例如
	//要发送到客户端的字符串
const str = "你好，欢迎访问~~";
//res.end()方法的作用
//向客户端发送指定的内容，并结束这次请求的处理过程
res.end(str)
```

#### 解决中文乱码问题

当调用res.end()方法，向客户端发送中文内容时候，会出现乱码问题，此时需要手动设置内容的编码格式

```js
server.on("request",(req,res)=>{
//发送的内容包含中文
const str = "你好，欢迎访问~~";
//为了防止出现乱码问题，需要设置响应头Content-Type的值为text/html;charset:utf-8
res.setHeader("Content-Type","text/html;Charset=utf-8")
//把包含中文的内容响应给客户端
res.end(str)
```

#### 根据不同的url响应不同的html内容

实现步骤：

- 获取请求的url地址
- 设置默认的相应内容为404 Not found
- 判断用户请求的是否为 / 或 / index.html首页
- 判断用户请求的是否为/login.html登录页面
- 设置Content-Type响应头，防止中文乱码
- 使用res.end( )把内容响应给客户端

```js
const http = require("http")
const server = http.createServer()
server.on("request",(req,res)=>{
    //1、获取请求的url地址
    const url = req.url
    //2、设置默认的相应内容为404 Not found
    let content = "<h1>404 Not found</h1>"
   	//3、判断用户请求的是否为 / 或/index.html
    //4、判断用户请求的是否为 / 或/login.html
    if(url == "/" || url == "/index.html"){
        content = "<h1>index</h1>"
    }else if(url == "/login.html"){
        conent = "<h1>login</h1>"
    }
    //5、设置响应头防止中文乱码
    r.setHeader("Content-Type","text/html;charset=utf-8")
    res.end(content)
})
```

## Express框架

### 用express创建基本的web服务器

```js
//1.导入express
const express = require("express")
//2.创建web服务器
const app = express()
//调用app.listen(端口号,启动成功后的回调函数),启动服务器
app.listen(80,()=>{
    console.log("express server running at http://127.0.0.1")
})
```

### 监听GET请求

通过app.get()方法,可以监听客户端的GET请求,具体的语法格式如下

```js
//参数1:客户端请求的URL地址
//参数2:请求对应的处理函数
//	req:请求对象(包含了与请求相关的属性和方法)
//	res:响应对象(包含了与响应相关的属性和方法)
app.get("请求URL",function(req,res){/*处理函数*/})
```

### 监听POST请求

通过app.post()方法,可以监听客户端的POST请求,具体的语法格式如下

```js
//参数1:客户端请求的URL地址
//参数2:请求对应的处理函数
//req:请求对象(包含了与请求相关的属性和方法)
//res:响应对象(包含了与响应相关的属性和方法)
app.post("请求URL",function(req,res){/*请求函数*/})
```

### 把内容响应给客户端

通过res.send()方法,可以把处理好的内容发送给客户端:

```js
//监听post和get请求并响应内容
app.get("/index",(req,res)=>{
    console.log("有人发送了一个GET请求");
    res.send("GET")
})
app.post("/login",(req,res)=>{
    console.log("有人发送了一个POST请求");
    res.send("POST")
})
```

### 获取URL中携带的查询参数

通过req.query对象,可以访问到客户端通过查询字符串的形式发送到服务器的参数

```js
app.get("/",(req,res)=>{
    //req.query 默认时应该空对象
    //客户使用?name=zs&age=20 这种查询字符串的形式,发送到服务器的参数
    //可以通过req.query对象访问到,例如:
    //req.query.name req.query.age
    console.log(req.query)
})
```

### 获取URL中的动态参数

通过req.params对象,可以访问到URL中通过:匹配到的动态参数:

```js
//URL地址中,可以通过:参数名的形式,匹配到动态参数值
app.get("/user/:id",(req,res)=>{//冒号是必需的,冒号后面的字符名是任意起的
    //req.params 默认是一个空对象
    //里面存放着通过冒号动态匹配到的参数值
    console.log(req.params)
})
```

### 托管静态资源

#### express.static()

express提供了一个非常好用的函数,叫做express.static(),通过它,我们可以非常方便地创建一个静态资源服务器,例如,通过如下代码就可以将public目录下的图片,CSS文件和JS文件对外开放访问了:

```js
app.use(express.static("public"))
```

现在,你就可以访问public目录下的所有文件了

http://localhost:3000/images/bg.jpg

http://localhost:3000/css/style.css

http://localhost:3000/js/login.js

注意:Express在指定的静态目录中查找文件,并对外提供资源的访问路径,因此,存放静态文件的目录名不会出现在URL中.

#### 托管多个静态资源

如果要托管多个静态资源目录,请多次调用express.static()函数

```js
app.use(express.static("public"))
app.use(express.static("files"))
```

#### 挂载路径前缀

如果希望在托管的静态资源访问路径之前挂载路径前缀，则可以使用如下的方式

```js
app.use("/public",express.static("public"))
```

这样就可以通过带有/public前缀地址来访问public目录中的文件了：

- http://localhost:3000/public/images/kitten.jpg
- http://localhost:3000/public/css/style.css
- http://localhost:3000/public/js/app.js

### 路由

从广义上讲，路由就是映射关系

现实中的路由：拨打10086人工客服的时候，不同的数字按键对应不同的业务服务名称，在这里，路由就是按键和服务之间的映射关系。

#### Express中的路由

在Express中，路由指的是客户端的请求与服务器处理函数之间的映射关系。

Express中的路由分3部分组成，分别是请求的类型、请求的URL地址、处理函数，格式如下：

```js
//app.method(path,处理函数)
//匹配GET请求，且请求URL为/
app.get("/",function(req,res){
    res.send("hello world!")
})
//匹配POST请求，且请求的URL为/
app.post("/",function(req,res){
    res.send("Got a POST request")
})
```

#### 路由的匹配过程

每当一个请求到达服务器后，需要先经过路由的匹配，只有匹配成功后，才会调用对应的处理函数。在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的URL同时匹配成功，则Express会将这次请求转交给对应的function函数进行处理

```js
//app.get("/",funA)=========>funA(req,res){/*处理并响应本次请求*/}
//app.post("/",funB)=========>funB(req,res){/*处理并响应本次请求*/}
//app.get("/user",funC)=========>funC(req,res){/*处理并响应本次请求*/}
//app.post("/user",funD)=========>funD(req,res){/*处理并响应本次请求*/}
```

#### 路由的简单使用

```js
const express =require("express")
const app=express()
//挂载路由到app这个实例上（实际开发中很少直接挂载路由到app上）
app.get("/",(req,res)=>{
    res.send("有人发送了一个get请求")
})
app.post("/",(req,res)=>{
    res.send("有人发送了一个POST请求")
})
app.listen(9777,()=>{
    console.log("running......")
})
```

#### 模块化路由

为了方便对路由进行模块化管理，Express不建议将路由直接挂载到app上，因为这会导致代码量大不方便管理，因此实际开发过程中推荐将路由抽离为单独的模块。

实现步骤：

- 创建路由模块对应的.js文件
- 调用express.Router()函数创建路由对象
- 向路由对象上挂载具体的路由
- 使用module.exports向外共享路由对象
- 使用app.use()函数注册路由模块

```js
//创建路由模块router.js
const express = require("express")//引入express框架
const router = express.Router()//创建路由容器
router.get("/login", (req, res) => {//挂载路由
    res.send("登录成功~~")
    console.log("有人来访问了~~");
})
router.post("/register", (req, res) => {
    res.send("注册成功~~")
    console.log("有人来访问了~~");
})
module.exports = router;//向外暴露
```

```js
//user.js
const express=require("express")
const app=express()
const userRouter=require("./router")//引入路由模块
app.use(userRouter)//注册路由模块
app.listen("7171",()=>{
    console.log("server is running");
})
```

类似于托管静态资源，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也很简单：

```js

const express=require("express")
const app=express()
const userRouter=require("./router")//引入路由模块
app.use("/user",userRouter)//注册路由模块,并添加访问前缀,
app.listen("7171",()=>{
    console.log("server is running");
})
```

### 中间件

特指业务流程的中间处理环节。

当一个请求到达Express的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理

node中间件本质上就是在进入具体的业务处理之前，先让特定过滤器处理。如下图所示:

![img](https://img-blog.csdnimg.cn/20190729162044195.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMzg3NjMx,size_16,color_FFFFFF,t_70)

#### 中间件的格式

Express的中间件，本质上就是一个function处理函数，Express中间件格式如下：

```js
var express = require("express")
var app = express()
app.get("/",function(req,res,next){
  
})
app.listen(3000)
```

注意：中间件函数的形参列表中，必须包含next参数。而路由处理函数中只包含req和res。

#### next()函数的作用

next()函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

#### 定义中间件函数

通过如下的方式定义一个最简单的中间件函数：

```js
//常量mw所指向的就是一个中间件函数
const mw=function(req,res,next){
    console.log("这是一个最简单的中间件函数")
    //注意：在当前中间件的业务处理完毕后必须调用next()函数
    //表示把流转关系转交给下一个中间件或路由
    next()//这个必须调用
}
```

#### 全局生效的中间件

客户端发起的任何请求，到达服务器后，都会触发的中间件，叫做全局生效的中间件。通过调用app.use(中间件函数)，即可定义一个全局生效的中间件，示例代码如下：

```js
const express=require("express")
const app=express()
//注册一个中间件
const mw=function(req,res,next) {
    console.log("这里是中间件函数");
    next();
}
app.use(mw)//注册为全局生效的中间件
app.get("/index",(req,res)=>{
    res.send("首页")
    console.log("这里是首页");
})
//启动服务器
app.listen("4321",()=>{
    console.log("server is running...");
})
```

#### 定义全局生效中间件的简化形式

```js
//全局生效的中间件
app.use(function(req,res,next){
    console.log("这是中间件函数的简化写法")
    next()
})
```

#### 中间件在实际开发中的作用

多个中间件之间共享同一份req和res。基于这种特性，我们可以在上游的中间件中统一为req和res对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

```js
//体验中间件的作用
const express = require("express");
const moment = require("moment");
const app = express()
app.use(function (req, res, next) {
    //获取请求到达服务器的事件
    const time = new Date;
    //为req对象挂载自定义的时间属性，从而把属性共享给后面的所有路由
    req.startTime = moment(time).format("YYYY-MM-DD HH:mm:ss");
    next()
})
app.get("/login", (req, res) => {
    res.send("hahaha" + req.startTime)
})
app.listen(7071, () => {
    console.log("Server is running...");
})
```

#### 定义多个全局中间件

可以使用app.use()连续定义多个全局中间件，客户端请求到达服务器后，会按照中间件定义的先后顺序依次进行调用，示例代码如下

```js
const express=require("express")
const app = express()
app.listen(9102,()=>{
    console.log("端口9102监听成功~");
})
app.use(function(req,res,next) {
    console.log("我是中间件1号");
    next()
})
app.use(function(req,res,next) {
    console.log("我是中间件2号");
    next()//next()必须要有否则不会往下执行
})
app.use(function(req,res,next) {
    console.log("我是中间件3号");
    next()
})
app.get("/index",(req,res)=>{
    res.send("这里是index页面")
})
```

#### 局部生效的中间件

不使用app.use()定义的中间件就叫做局部生效的中间件，示例代码如下：

```js
const express =require("express")
const app=express()
const mw=function(req,res,next) {
    res.c="呜呜"
    next()
}
app.get("/index",mw,function(req,res) {
    console.log(res.c);//"呜呜"
    res.send("这里是index页面")
})
app.get("/login",function(req,res) {
    console.log(res.c);//undefined
    res.send("这里是login页面")
})
app.listen(1112,function() {
    console.log("服务器启动成功~");
})
```

#### 定义多个局部中间件

可以在路由中通过如下两种等价的方式使用多个局部中间件

```js
//以下两种写法是完全等价的，通过这两种方式可以定义多个中间件
const express = require("express")
const app = express()
app.listen(4119, () => {
    console.log("服务器启动成功~");
})
const mw1 = function (req, res, next) {
    console.log("这里是中间件1");
    next()
}
const mw2 = function (req, res, next) {
    console.log("这里是中间件2");
    next()
}
const mw3 = function (req, res, next) {
    console.log("这里是中间件3");
    next()
}
/*app.get("/index",mw1,mw2,mw3,(req,res)=>{ //方式一
    res.send("这里是index页面")
    console.log("这里是index页面");
})*/
app.get("/index",[mw1,mw2,mw3],(req,res)=>{//方式二
    res.send("这里是index页面")
})
```

#### 了解中间件的5个使用注意事项

- 一定要在路由之前注册中间件（错误级别的中间件除外，必须放在路由之后）
- 客户端发送过来的请求，可以连续调用多个中间件进行处理
- 执行完中间件的业务代码后，不要忘记调用next()函数
- 为了防止代码逻辑混乱，调用next()函数后不要再写额外的代码
- 连续调用多个中间件后，多个中间件之间共享req和res对象

#### 中间件的分类

为了方便大家理解和记忆中间件的使用，Express官方把常见的中间件用法分为5大类，分别是

- 应用级别的中间件

  - 通过app.use()或者app.get()或app.post()绑定到app实例上的中间件叫做应用级别的中间件，代码示例如下：

    ```js
    //应用级别中间件(全局中间件)
    app.use((req,res,next)=>{
        next()
    })
    //应用级别的中间件(局部中间件)
    app.get("/",mw,(req,res)=>{
        res.send("HOME PAGE")
    })
    ```

- 路由级别的中间件

  - 绑定到express.Router()实例上的中间件，叫做路由级别的中间件。它的用法和应用级别的中间件没有任何区别。只不过应用级别的中间件是绑定到app实例上，路由级别的中间件是绑定到router实例上，代码示例如下：

    ```js
    const app=express()
    const router=express.Router()
    //路由级别的中间件
    router.get("/index",function(req,res,next){
        console.log("time:",Date.now())
        next()
    })
    ```

- 错误级别的中间件

  - 作用是专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题

  - 错误级别的中间件是发生错误才会被执行，跟前面提到的中间件不一样，区别在于多了个err参数

    ```js
    const express=require("express")
    const app=express()
    app.listen(2001,()=>{
        console.log("服务器启动成功~");
    })
    
    app.get("/",(req,res)=>{
        throw new Error("服务器发生错误")
        res.send("首页")
    })
    //代码内部发生错误，错误级别的中间件才会被执行，否则不会被执行，需要放再路由后面
    app.use((err,req,res,next)=>{
        console.log(err.message);
        res.send(err.message)
        console.log("哈哈");
        next()
    })
    ```

- Express内置的中间件

  - exprss.static快速托管静态资源的内置中间件，例如：HTML文件、图片、CSS样式等(无兼容性)

    ```js
    //该方法的易错点
    //这里需要请求的路径是public下面的/stylesheets/reset.css，express.static开放的是public里面的资源不包括public这个文件夹本身
     <link rel="stylesheet" type="text/css" href="../public/stylesheets/reset.css" />
    //因此，要这样写就包括了public文件夹本身，前面这个public不能漏掉，f
     app.use("/public",express.static(path.join(__dirname,"./public")));
    ```

    

  - express.json解析JSON格式的请求体数据（有兼容性，仅在4.16.0+版本中可用）

  - express.urlencoded解析URL-encoded格式的请求体数据（有兼容性，仅在4.16.0+版本中可用）

    ```js
    const express=require("express")
    const app=express()
    app.listen(3211,()=>{
        console.log("服务器启动成功~");
    })
    //配置解析application/json格式数据的内置中间件
    app.use(express.json())
    //配置解析application/x-www-form-urlencoded格式数据的内置中间件
    app.use(express.urlencoded({extended:true}))//如果extended设置为false，那么对URL-encoded的数据的解析采用queryString库;如果设置为true，那么采用qs库，允许将富对象和数组编码为url编码格式，允许使用url编码的json体验
    如果设置为true，那么采用qs库，允许将富对象和数组编码为url编码格式，允许使用url编码的json体验。有关更多信息，请参阅qs库。
    app.post("/login",(req,res)=>{
        console.log(req.body);
        res.send(req.body)//如果不配置，默认返回一个undefined
    })
    //注意：表单提交的格式都是urlencoded格式的数据，如果强制设置编码格式为json，返回的是一个这个：{}
    ```

  ![img](https://img2018.cnblogs.com/i-beta/1291869/202002/1291869-20200227193046749-399966259.png)

- 第三方的中间件

  - 非Express官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。再项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率

  - 例如：再express@4.16.0之前的版本中，经常使用body-parser这个第三方中间件，来解析请求体数据。使用步骤如下

    - 运行npm install body-parser安装中间件

    - 使用require导入中间件

    - 调用app.use()注册并使用中间件 

    - 注意：Express内置的express.urlencoded中间件就是基于body-parser这个第三方中间件进一步封装出来的，用法跟express.urlencoded类似

      ```js
      //导入中间件
      const bodyParser=require("body-parser")
      //注册中间件
      app.use(bodyParser.urlencoded({extend:false}))
      app.post("/user",(req,res)=>{
          //如果没有配置任何解析表单数据的中间件，则req.body默认等于u'n'dei
          console.log(req.body)
      })
      ```

  - 使用第三方的serve-favicon中间件来生成网页图标

    ```js
    const express = require("express")
    const serveFavicon = require("serve-favicon")
    const app = express()
    const path=require("path")
    app.listen(8071, () => {
        console.log("服务器启动成功~~");
    })
    app.use(serveFavicon(path.join(__dirname, "./favicon.ico")))
    app.use("/index", (req, res) => {
        res.send("这里是首页");
    })
    ```

  - 使用第三方中间件svg-captcha来生成验证码

    ```js
    app.use("/login",(req,res)=>{
        let svg = svgCaptcha.create(
            {
                size:4,
                noise:7,
                ignoreChars:"0oil",
                color:true,
                background:"#ccc",
                fontSize:50,
            }
        )
        res.type("svg")
        res.send(svg.data)
    })
    ```
    
  - 第三方中间件formidable实现文件上传
  
    ```js
    //upload.js
    const express = require('express')
    const app = express()
    const formidable = require("formidable")
    const path = require("path")
    const fs = require("fs")
    const time = require("time-stamp")
    app.listen(1038, () => {
        console.log("服务器启动成功");
    })
    app.post("/upload", (req, res) => {
        let form = formidable({
            uploadDir: path.join(__dirname, "./temp")
        })
        form.parse(req, (err, fields, files) => {
            const oldname = files.photo.name
            console.log(oldname);
            const newname = time("YYYYMMDDHHmmss") + (Math.random() + "").substring(2, 7) + path.extname(files.photo.name)
            const oldpath = files.photo.path
            const newpath = path.join(__dirname, "./uploads", newname)
            fs.renameSync(oldpath, newpath)
        })
        res.send("上传成功~")
    })
    ```
  
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <form action="http://localhost:1038/upload" method="post" enctype="multipart/form-data">
            <input type="text" name="username" id="">
            <input type="password" name="password" id="">
            <input type="file" name="photo">
            <input type="submit" value="上传">
        </form>
    </body>
    </html>
    ```

### 接口

#### GET接口

```js
//router.js
const { query } = require("express");
const express=require("express")
const router=express.Router()
router.get("/index",(req,res)=>{
    res.send({
        status:0,//0表示成功 1表示失败
        msg:"GET请求成功",
        data:req.query
    })
    console.log(req.query);
})
module.exports=router;
//app.js
const express=require('express')
const app=express()
const router=require("./router")
app.listen(10258,()=>{
    console.log("服务器启动成功~~");
})
app.use(router)
```

#### POST接口

```js
//router接口
const express=require("express")
const router=express.Router()
router.use(express.urlencoded({extended:false}))
router.use(express.json())
router.post("/login",(req,res)=>{
    res.send({
        status:0,
        msg:"登录成功",
        data:req.body
    })
})
router.post("/register",(req,res)=>{
    res.send({
        status:0,
        msg:"注册成功",
        data:req.body
    })
})
module.exports=router
//app.js
const express=require("express");
const router = require("./router");
const app=express()
app.listen(1011,()=>{
    console.log("服务器启动成功~~");
})
app.use(router)
```

#### 接口的跨域问题

## Cookie

### cookie简介

HTTP协议本身是无状态的。什么是无状态呢，即服务器无法判断用户身份。Cookie实际上是一小段的文本信息（key-value格式）。客户端向服务器发起请求，如果服务器需要记录该用户状态，就使用response向客户端浏览器颁发一个Cookie。客户端浏览器会把Cookie保存起来。当浏览器再请求该网站时，浏览器把请求的网址连同该Cookie一同提交给服务器。服务器检查该Cookie，以此来辨认用户状态。

打个比方，我们去银行办理储蓄业务，第一次给你办了张银行卡，里面存放了身份证、密码、手机等个人信息。当你下次再来这个银行时，银行机器能识别你的卡，从而能够直接办理业务。	

### cookie分类

会话cookie：保存在内存中，当浏览器的会话关闭后自动消失

持久cookie：保存在硬盘中，只有当时间到期了才会自动消失		

### cookie机制

当用户第一次访问并登陆一个网站的时候，cookie的设置以及发送会经历以下4个步骤：

客户端发送一个请求到服务器 => 服务器发送一个HttpResponse响应到客户端，其中包含Set-Cookie的头部 => 客户端保存cookie，之后向服务器发送请求时，HttpRequest请求中会包含一个Cookie的头部=>服务器返回响应数据

![https://upload-images.jianshu.io/upload_images/13949989-dcf024be2733e725.png](https://upload-images.jianshu.io/upload_images/13949989-dcf024be2733e725.png)

![img](https://img-blog.csdnimg.cn/20200122095237258.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjk5MTc5,size_16,color_FFFFFF,t_70)

### cookie的特点

- 不可跨域名
- 存储在浏览器里面，只要不过期关闭浏览器也会存在。
- 正常情况下cookie不加密，用户可轻松看到
- 用户可以删除或者禁用cookie
- 有数量和大小的限制，数量50左右，大小4kb左右
- Cookie 只能存储字符串 
- 不同的浏览器和项目之间不共享 Cookie 
- 存储 Cookie 后在整个项目中有效（页面之间共享）
- 存储时间非常灵活
- 不光可以服务器设置(set-cookie),客户端也可以设置(document.cookie)

### cookie的应用场景

- 在我们关闭一个登录过的网址并重新打开它后，我们的登录信息依然没有丢失
- 当我们浏览了商品后历史记录里出现了我们点击过的商品
- 当我们推回到首页后，推荐商品也为我们选出了相似物品

### NodeJs中cookie的基本使用

#### 安装cookie-parser中间件

```js
npm install cookie-parser --save
```

#### 引入

```js
const cookieParser = require("cookie-parser")
```

#### 注册中间件

```js
app.use(cookieParser())
```

#### 设置cookie

```js
res.cookie("name","马明明",{maxAge:90000,httpOnly:true})//res.cookie(名称，值，配置信息)
```

#### 关于cookie的参数的说明

- domin:域名
- name=value:键值对，可以设置要保存的 Key/Value，注意这里的 name 不能和其他属性项的名字一样
- Expires:过期时间（秒），在设置的某个时间点后该 Cookie 就会失效，如 expires=Wednesday, 09-Nov-99 23:12:40 GMT
- maxAge:最大失效时间（毫秒），设置在多少后失效 
- secure:当 secure 值为 true 时，cookie 在 HTTP 中是无效，在 HTTPS 中才有效 
- Path:表示 在那个路由下可以访问到cookie
- httpOnly:是微软对cookie做的扩展。如果在cookie中设置了"httpOnly"属性，则通过程序（JS 脚本、applet 等）将无法读取到cookie信息，防止 XSS 攻击的产生 
- singed:表示是否签名cookie, 设为true 会对这个 cookie 签名,这样就需要用 res.signedCookies 而不是 res.cookies 访问它。被篡改的签名cookie会被服务器拒绝,并且 cookie 值会重置为它的原始值。

#### 获取cookie

```js
req.cookies.name
```

#### 代码示例

```js
//cookie的基本使用.js
const express = require("express")
const app = express()
const path = require("path")
app.listen(9090, () => {
    console.log("服务器启动成功~~");
})
const cookieParser = require("cookie-parser")
//注册cookie中间件
app.use(cookieParser())
//解析post参数的中间件
app.use(express.urlencoded({extended:false}))
app.use(express.json())
//监听POST请求
app.get("/login.html", (req, res) => {
    let fPath = path.join(__dirname, "./cookie的基本使用.html")
    res.sendFile(fPath)
})
app.post("/login", (req, res) => {
    let { username, password } = req.body
    console.log(username,password);
    res.cookie("username", username, { maxAge: 86400000 ,httpOnly:true,domain:"ccc.com"})
    res.cookie("password", password, { maxAge: 86400000})
    res.send("<h1>登录成功</h1>")
})
app.get("/index", (req, res) => {
    let { username } = req.cookies
    if (!username) {
        res.send("请登录")
    } else {
        res.send(`<h1>${username},欢迎您</h1>`)
    }
})
```

```html
<!--cookie的基本使用.html-->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <form action="http://localhost:9090/login" method="post">
        <input type="text" name="username">
        <input type="password" name="password">
        <input type="submit" value="提交">
    </form>
</body>

</html>
```

## Session

### 诞生背景

其实设计Cookie之初，它并不是仅仅保存了一个key值，而是直接保存用户的信息，但是由于cookie是存在客户端的，而且本身存储的尺寸大小也是有限的，最关键的是用户是可见的，并且可以随意地修改，这相当地不安全。为了既安全又方便的读取全局信息，于是诞生了Session这种新的存储会话机制。

### 什么是Session

Session翻译为会话，服务器为每个浏览器创建一个会话对象，浏览器在第一次请求服务器时，服务器便会为该浏览器生成一个Seesion对象，保存在服务端，并且把Session的Id以cookie的形式发送给客户端浏览器，最终以用户显示结束或session超时为结束。session的生命周期默认为30分钟。

### 工作原理

- 当某个用户向服务器发送第一个请求时，服务器为其建立一个session，并为此session创建一个标识号(sessionID)
- 这个用户随后的所有请求都应包括这个标识号(sessionID)，服务器会校对这个标识号以判断请求是属于哪个session的
- sessionID标识号有两种实现方式：Cookie和URL重写
- Cookie是将数据直接保存在客户端，而Session是将数据保存在服务端，所以Session的安全性更佳

![https://upload-images.jianshu.io/upload_images/79702-5660ac4cb51f6257.jpg](https://upload-images.jianshu.io/upload_images/79702-5660ac4cb51f6257.jpg)

![img](https://images2015.cnblogs.com/blog/1104082/201702/1104082-20170210214818072-725308163.png)

### Cookie和Session的关系

- 二者都是为实现客户端与服务端交互而服务的
- Cookie是保存在客户端，缺点易伪造、不安全
- Session是保存在服务端，会消耗服务器资源
- Session实现有两种方式：Cookie和URL重写

### Session的应用场景

Session主要是服务器端存储，用来描述一些用户信息或者相关的其他数据，还可以是其他类型的数据，只要是你的业务觉得可以绑定到用户或客户端的相关数据都可以放到session中；最基本的场景就是存储登录用户信息。

### NodeJs中Session的基本使用

#### 安装cookie-session

```js
npm i cookie-session
```

#### 引入并开启session功能

```js
const cookieSession=require("cookie-session")//引入cookie-session中间件
//使用cookie-session中间件
app.use(cookieSession({
  name: 'sessionids',//sessionid的名称，默认可以省略
  keys: ['secret1','secret2','secret3'], //密钥锁,这把钥匙要加密,随意写的字符
  // Cookie Options
  //maxAge: 24 * 60 * 60 * 1000 // 24 hours , session的有效期
}))
```

#### 操作Session数据的方法

```js
//设置值
req.session.key=value
req.session[key]=value
//获取值
req.session.key //给值就是设值 不给值就是获取
//删除值
delete req.session.key或req.session.key=null
```

#### 代码案例

````js
//js后台部分
const express = require("express")
const app = express()
const cookieSession = require("cookie-session")
const path = require("path")
app.listen(1234, () => {
    console.log("服务器启动成功~");
})
app.use(express.urlencoded({ extended: false }))
app.use(express.json())
app.get("/login.html", (req, res) => {
    let fPath = path.join(__dirname, './session的基本使用.html')
    res.sendFile(fPath)
})
app.use(cookieSession({
    name: "mmm",
    keys: ["asad", "aQREWERWER", "23424334"],
    maxAge: 1000 * 60 * 60 * 24
}))
app.post("/login", (req, res) => {
    let { username } = req.body
    let { password } = req.body
    req.session.username = username
    req.session.password = password
    res.send("登录成功~~")
})
//个人中心
app.get("/userInfo", (req, res) => {
    if (req.session.username) {
        res.send(`${req.session.username},欢迎您~~`)
    } else {
        res.redirect("http://localhost:1234/login.html")
    }
})
````

````html
<!--前端部分-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>请登录</h1>
    <form action="http://localhost:1234/login" method="post">
    <input type="text" name="username">
    <input type="password" name="password">
    <input type="submit" value="提交">
    </form>
</body>
</html>
````

#### 关于Session的一些配置参数

```js
/*name:[String]，要设置的Cookie的名称，默认为express:sess。
keys:[Array]，是个数组，用于签名和验证Cookie值的键列表。设置Cookie时始终使用签名keys[0]，验证时使用其它密钥。
secret:[String]，如果没有设置keys，将使用secret作为单一密钥。
maxAge:[Number]，设置有效时间，为毫秒数。*/
app.use(cookieSession({
  name:"sess",
  keys:["aaa","bbb","ccc"],
  maxAge:24*60*60*1000, //有效时间为24小时
}))
```

## Token

## EJS模板引擎

HTML中的标签要和真实的数据进行拼接然后渲染在页面上，模板引擎帮我们很好地解决了拼接问题。我们学习的是EJS模板引擎。

### 使用步骤

安装ejs

```sh
npm i ejs
```

在项目中设置ejs模板引擎

```js
/*在项目的根目录下创建views文件夹
在views文件夹下创建模板文件，必须以.ejs为后缀名*/
const app = express()
app.set("view engine","ejs") //view engine视图引擎，页面在后端叫做视图
//设置模板文件位置 => 项目根路径下views目录为模板文件存放目录
app.set('views', __dirname + '/views');
```

### ejs语法

#### 渲染语法

```js
//render函数
在express框架中使用ejs.render(dataAndOptions)就可以由一个模板文件生成静态html文件，并将数据嵌入到html文件中，这个函数有如下参数:
    ejs模板文件名
    动态数据
    渲染个性化参数 -例如模板文件缓存，函数执行环境，打开debug模式等
app.get('/',function(req,res) {
    res.render('index',{
        //index 表示模板目录下的index.ejs文件
        //html中的css什么的，都不需要关心，静态页面是什么样，在index.ejs中还是什么样
        name:'ejs case'
    }) ;
});
res.render("模板名称"[,data])
//参数1为模板名称不需要添加后缀，会自动寻找对应的ejs文件
//参数2为可选参数，向模板中传递数据，必须是一个对象
```

#### 模板语法

```ejs
<!--数据渲染>
<% = 变量名 %>
<!--分支-->
<% if(条件){ %>
<% }else{ %>
<% } %>
<!--循环-->
<% for(let i=0;i<5;i++){ %>
    循环体
<% } %>
<!--包含文件-->
<!--包含文件也是.ejs文件，无需携带后缀名-->
<%- include("公共文件路径") %> <!--路径相对于当前文件-->
```

#### 代码案例

```ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>首页</h1>
    <p>
        大家好,我叫<%=name%>,今年<%=age%>岁,我的爱好是<%=hobby%>,期末考试考了<%=score%>分,
        <%if(score>=60){%>
            及格了
            <%}else{%>
                没及格
            <%}%>
    </p>
    <script src="./14.ejs模板引擎.js"></script>
</body>
</html>
```

```js
//14.ejs模板引擎.js
const express=require("express")
const app=express()
app.listen(1212,()=>{
    console.log("服务器启动成功~");
})
app.set("view engine","ejs")
app.get("/index",(req,res)=>{
    let data={
        name:"马明明",
        age:18,
        hobby:["学习","吃饭","工作"],
        score:59
    }
    res.render("index",data)
})
```

## Express脚手架

### 全局安装express-generator(安装一次就行)

```sh
npm i -g express-generator
```

### 命令行参数

```sh
#express -h可以列出所有可用的命令行参数
$ express -h

  Usage: express [options] [dir]

  Options:

    -h, --help          输出使用方法
        --version       输出版本号
    -e, --ejs           添加对 ejs 模板引擎的支持
        --hbs           添加对 handlebars 模板引擎的支持
        --pug           添加对 pug 模板引擎的支持
    -H, --hogan         添加对 hogan.js 模板引擎的支持
        --no-view       创建不带视图引擎的项目
    -v, --view <engine> 添加对视图引擎（view） <engine> 的支持 (ejs|hbs|hjs|jade|pug|twig|vash) （默认是 jade 模板引擎）
    -c, --css <engine>  添加样式表引擎 <engine> 的支持 (less|stylus|compass|sass) （默认是普通的 css 文件）
        --git           添加 .gitignore
    -f, --force         强制在非空目录下创建
```

### 搭建项目框架

```js
express -e 项目名    //参数 -e 就是说用ejs引擎,以下写法都可以：

// EJS模板需要显示指定
express --ejs 项目名

express --view=ejs 项目名 （官方推荐写法）
//注: express -ejs nodeEjs 或 express -view=ejs nodeEjs 都是错误写法，尽管Jade支持-view这种写法。。。
//所以建议使用最简单的写法或者官方推荐的 "--view=** " 写法
```

### 下载所有依赖包

```sh
cd 项目名
npm install
```

### 启动项目

```sh
npm start 或 npm run start
//使用以下命令也可以的
node ./bin/www 或 node /bin/www
```

### package.json

```json
// package.json 中 scripts属性来配置一些命令：

//【npm  run   属性名】      来代替 某些命令

// npm run start  可以把run省略掉，其他的不可以
{
  "scripts": {
    "start": "node ./bin/www",
      "dev":"nodemon ./bin/www"
      属性名: "代替的运行的命令"
  }
}
```

## MySql数据库

### SQL查询语言

SQL是结构化查询语言，专门用来访问和处理数据的编程语言，能够让我们以编程的形式操作数据库里面的数据

### 特点

- SQL是一门数据库编程语言
- SQL在MySql、Oracle、SQL Server等数据库中是通用的
- SQL语言不分大小写，官方建议关键字用大写，变量名小写

### 主要内容

主句：SELECT 查询  INSERT INTO 增加 UPDATE修改 DELETE删除

子句：where(and和or)、order by、limit、join...on

### 添加数据

```sql
# insert into 表名 (字段名1，字段名2，字段名3) values (值1,值2,值3)
# 如果值是字符串则必须加引号
#插入3行数据
INSERT INTO Persons 
VALUES 
('Gates', 'Bill', 'Xuanwumen 10', 'Beijing')
('Carter', 'Thomas', 'Changan Street', 'Beijing')
('Bush', 'George', 'Fifth Avenue', 'New York')
#也可以这样写
INSERT INTO Persons VALUES ('Gates', 'Bill', 'Xuanwumen 10', 'Beijing')
INSERT INTO Persons VALUES ('Carter', 'Thomas', 'Changan Street', 'Beijing')
INSERT INTO Persons VALUES ('Bush', 'George', 'Fifth Avenue', 'New York')
#指定字段添加
INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
```

### 删除数据

```sql
#DELETE FROM表名 --清空表，不加条件全部删除，很危险
#DELETE FROM 表名 WHERE 条件 --删除符合条件的数据
DELETE FROM Persons WHERE Address="New York" #把表里面Adderss为New York的数据删除
```

物理删除：使用delete删除了就没有了，不可逆

逻辑删除：一般使用逻辑删除，使用一个状态来表示是否删除(status:0删除 1存在)

### 更新数据

```sql
#语法：where后面是条件，要把 字段名3=值3 的这行数据中的字段名1的值改为值1，字段名2的值改为值2
UPDATE Person set 字段名1=值1，字段名2=值2，字段名3=值3,...
UPDATE Person set 字段名1 = 值1,字段名2 = 值2,...WHERE 字段名3=值3
#修改（更新）也是不可逆的
UPDATE student set  age=10;
UPDATE student set  age=20 WHERE grade="大专";
UPDATE student set  age=30 WHERE grade="博士";
UPDATE student set  age=12,tidcard=10001,pro="南沙小学"  WHERE grade="小学";
```

### 查询数据

```sql
# SELECT * FROM 表名   -- *代表所有的列信息都展示
# SELECT  字段1,字段2,...  FROM  表名  -- 只展示某些列信息
SELECT  uname,sex  FROM  student
SELECT  uname,sex,tidcard  FROM  student
SELECT  *  FROM  student   
SELECT  *  FROM  student    WHERE  age=10;   -- 从student表里查询 age=10 的这几条数据
SELECT  uname,sex,pro  FROM  student    WHERE  age=10;    -- 从student表里查询 age=10 的这几条数据,把相对应的字段展示出来
```

### 练习

```sql
--1：查询学生的学号与姓名。
--2：查询全体学生的记录。
--3：查询全体学生的姓名及出生年份。
--4：查询计算机系全体学生的姓名。
--5：查询所有学生年龄在20岁以下的学生的姓名和年龄。
--6：查询年龄在20~23之间的学生的姓名、所在系、和年龄。
--7：查询年龄不在20~23之间的学生的姓名、所在系、和年龄。
--8：查询姓“张”的学生的详细信息。
--9：查询学生表中姓“张”，“李”，“刘”的学生的情况。
--10：查询学生表中不姓“刘”的学生的情况。
--11：将学生按年龄升序排序。
--12：查询选修了课程“C02”的学生的学号及其成绩，查询结果按成绩降序排列。
--13：查询全体学生的信息，查询结果按所在系的的系名升序排序,同一个系的学生按年龄降序排列。
SELECT xh,xm from xsb
SELECT * from xsb 
SELECT xm,2021-age FROM xsb
SELECT xm from xsb WHERE szx="计算机系"
SELECT xm,age FROM xsb WHERE age<20
SELECT xm,szx,age FROM xsb WHERE age BETWEEN 20 and 23
SELECT xm,szx,age FROM xsb WHERE age not BETWEEN 20 and 23
SELECT * FROM xsb WHERE xm like "张%"
SELECT * FROM xsb WHERE xm like "张%" or xm like "李%" or xm like "刘%"
SELECT * FROM xsb WHERE xm not like "张%"
SELECT * FROM xsb ORDER BY age ASC
SELECT xh,cj FROM cjb WHERE kch="c02" ORDER BY cj DESC
SELECT * FROM xsb ORDER BY szx ASC,age DESC
```

## Node操作MySql

### 下载mysql模块

```shell
npm i mysql
```

### 引入mysql模块

```js
const mysql = require("mysql")
```

### 创建mysql数据库配置连接

```js
//使用mysql的createConnection()方法去创建一个连接，返回一个连接对象
//需要传递一个JSON作为参数，配置host主机，port端口，user数据库账号，password数据库密码，database数据库名称
let connectObj=mysql.createConnection({
    host:"主机名",
    user:"用户名",
    password:"密码",
    port:"端口号",
    database:"要操作的数据库名称"
})
```

### 使用连接对象的connect()方法连接数据库

```js
connectObj.connect()
```

### 使用query方法执行sql语句，并得到结果

```js
connectObj.query(sqlStr,(err,result)=>{
    
})
```

## HTTP协议

### HTTP协议简介

HTTP协议是Hyper Text Transfer Protocol（超文本传输协议）的缩写,是用于从万维网服务器传输超文本到本地浏览器的传送协议。

### HTTP协议的特点

- 简单快速：客户向服务器请求服务时，只需传送请求方法和路径。请求方法常用的有GET、HEAD、POST。每种方法规定了客户与服务器联系的类型不同。由于HTTP协议简单，使得HTTP服务器的程序规模小，因而通信速度很快。
- 灵活：HTTP允许传输任意类型的数据对象。正在传输的类型由Content-Type加以标记。这意味着，只要客户端和服务器知道如何处理的数据内容，任何类型的数据都可以通过HTTP发送。客户端以及服务器指定使用适合的MIME-type内容类型。
- 无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。
- 无状态：HTTP协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。

### HTTP协议交互原理

浏览器作为HTTP客户端通过URL向HTTP服务端即WEB服务器发送所有请求。Web服务器有：Apache服务器，IIS服务器（Internet Information Services）等。Web服务器根据接收到的请求后，向客户端发送响应信息。HTTP默认端口号为80，但是你也可以改为8080或者其他端口。

![cgiarch](https://atts.w3cschool.cn/attachments/image/20160225/1456372014816657.gif)

### HTTP报文

- 请求报文：

  - 请求行：包括请求方法、请求的url、http协议及版本。

  - 请求头：一大堆的键值对。

    ![image-20211030164246737](C:/Users/Shining/AppData/Roaming/Typora/typora-user-images/image-20211030164246737.png)

  - 空行指的是：当服务器在解析请求头的时候，如果遇到了空行，则表明，后面的内容是请求体。最后一个请求头之后是一个空行，发送回车符和换行符，通知服务器以下不再有请求头。（现在浏览器改版了，请求体单独列开来了）

  - 请求体：数据部分。

    ![image-20211030163024488](C:/Users/Shining/AppData/Roaming/Typora/typora-user-images/image-20211030163024488.png)

- 响应报文

  - 响应行：协议版本、响应的状态

    ![image-20211030163833679](C:/Users/Shining/AppData/Roaming/Typora/typora-user-images/image-20211030163833679.png)

  - 响应头

  - 空行：最后一个响应头之后是一个空行，发送回车符和换行符，通知服务器以下不再有响应头。（现在浏览器改版了，响应体单独列开来了）

  - 响应体：响应的数据

    ![image-20211030165012098](C:/Users/Shining/AppData/Roaming/Typora/typora-user-images/image-20211030165012098.png)

### 常见的HTTP状态码

| 状态码 | 重要程度 | 含义                                           |
| ------ | -------- | ---------------------------------------------- |
| 200    | 高       | 一切正常                                       |
| 304    | 高       | 重复请求相同的资源，浪费宽带                   |
| 400    | 高       | 客户端出现问题，服务器收到了请求内容但是看不懂 |
| 404    | 高       | 找不到资源                                     |
| 500    | 高       | 服务器错误                                     |

## Ajax

### 传统网站中存在的问题

- 网速慢的情况下，页面加载事件长，用户只能等待
- 表单提交后，如果一项内容不合适，需要重新填写所有表单内容，用户体验非常不好
- 页面跳转，重新加载页面，造成资源浪费，增加用户等待时间

### Ajax概述

Ajax不是一个独立的语言，而是将一种现有的标准组合在一起使用的新方式。它是Js中的一个知识点。全称为Asynchronous JavaScript And XML，就是异步的JS和XML。通过Ajax可以在浏览器中向服务器发送异步请求，最大的优势是无刷新获取数据。

### XML简介

XML可扩展标记语言。XML被设计用来传输和存储数据。XML和HTML类似，不同的是HTML中都是预定义标签，而XML中没有预定义标签全都是自定义标签，用来表示一些数据。

```xml
<!--比如说我有一些学生数据-->
<!--name="孙悟空"; age=19; gender="男" 用XML表示如下-->
<student>
	<name>孙悟空</name>
    <age>19</age>
    <gender>男</gender>
</student>
```

### Ajax的优缺点

- 优点：
  - 可以无需刷新页面而与服务器端进行通信
  - 允许你根据用户事件来更新部分页面内容
- 缺点：
  - 没有浏览历史，不能回退
  - 存在跨域问题（同源）
  - SEO不友好

### Ajax的应用场景

- 页面上拉加载更多数据
- 列表数据无刷新分页
- 表单项离开焦点数据验证
- 搜索框提示文字下拉列表

### Ajax运行原理

Ajax必须要运行在网站环境下才能生效，我们用NodeJs来搭建web服务器。Ajax相当于浏览器发送请求与接收响应的代理人，以实现在不影响用户浏览页面的情况下，局部更新页面数据，从而提高用户体验。

<img src="https://images2018.cnblogs.com/blog/1383488/201805/1383488-20180513230401155-1932432083.png" alt="img" style="zoom:50%;" />

### Ajax的实现步骤

- 创建Ajax对象（创建发送请求的代理人）

  ```js
  let xhr = new XMLHttpRequest()
  ```

- 告诉Ajax请求地址以及请求的方式

  ```js
  xhr.open("GET","http://localhost:3000/index")
  ```

- 发送请求

  ```js
  xhr.send()
  ```

- 获取服务器端给客户端的响应数据

  ```js
  //有两种写法
  //第一种
  xhr.onload=function(){
      console.log(xhr.responseText)
  }//响应的数据全部加载完毕才会触发onload事件
  //第二种
  xhr.onreadystatechange=function(){
      if(xhr.readyState==4){//当xhr.readyState的值为4时数据全部加载完毕
          console.log(xhr.resopnseText)
      }
  }
  ```

### 服务器端响应的数据格式

在真实的项目中，服务器端大多数情况下会以JSON对象作为响应数据的格式。当客户端拿到响应数据时，要将JSON数据和HTML字符串进行拼接，然后将拼接的结果展示在页面中。

在http请求与响应过程中，无论是请求参数还是响应内容，如果时对象类型，最终都会被转换为对象字符串进行传输

```js
JSON.parse()//将json字符串转换为json对象
```

### 请求参数传递

- GET请求传参

  ```js
  xhr.open("GET","http://localhost:3000/index?name=马明明&age=18")
  ```

- POST请求传参

  ```js
  xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded")
  xhr.send("name=马明明&age=18")
  ```

### 请求参数的格式

- application/x-www-form-urlencoded

  ```js
  name=马明明&age=18&sex=男
  ```

- application/json

  ```json
  {"name":"马明明","age":18}
  ```

在请求头中指定Content-Type属性值时application/json，告诉服务器端当前请求的参数格式时json

```js
JSON.stringify()//将json对象转换为json字符串
```

注意：GET请求时不能提交json对象数据格式的，传统网站的表单提交也不支持json对象数据格式的

### 获取服务器端的响应

#### Ajax状态码

在创建Ajax对象，配置Ajax对象、发送请求以及接收完服务器端响应的数据，这个过程中的每一个步骤都会对应一个数值这个数值就是Ajax状态码

| 状态码 |                       含义                       |
| :----: | :----------------------------------------------: |
|   0    |          请求未初始化（还没有调用open）          |
|   1    | 请求已经建立，但是还没有发送（还没有调用send()） |
|   2    |                   请求已经发送                   |
|   3    |  请求正在处理,通常响应中已经有部分数据可以用了   |
|   4    |    响应已经完成，可以获取并使用服务器的响应了    |

```js
//获取ajax的状态码
xhr.readyState
```

#### 两种获取服务器端响应方式的区别

|        区别描述        | onload事件(推荐使用) | onreadystatechange事件(兼容IE才使用) |
| :--------------------: | :------------------: | :----------------------------------: |
|    是否兼容IE低版本    |        不兼容        |                 兼容                 |
| 是否需要判断Ajax状态码 |        不需要        |                 需要                 |
|      被调用的次数      |         一次         |                 多次                 |

### Ajax错误处理

- 网络畅通，服务器端能接收到请求，服务器端返回的结果不是预期结果
  - 可以判断服务器端返回的状态码，分别进行处理。xhr.status获取http状态码
- 网络畅通，服务器端没有接收到请求，返回404状态码
  - 检查请求地址是否出错
- 网络畅通，服务器端能接收到请求，服务器端返回500状态码
  - 服务器错误，找后端程序员进行沟通
- 网络中断，请求无法发送到服务器
  - 会触发xhr下面的onerror事件，而不会触发nonload事件，在onerror事件处理函数中输出提示信息

## Promise 

### 同步和异步编程

同步：代码一行一行执行，如果其中一行代码没有运行完，或者报错了，那么后续代码就不会再执行了，会等待前面的代码执行完毕才会继续执行

```js
//alert和错误会阻塞代码执行
alert("哈哈哈")//点击了确定后面的代码才会执行
console.lo("我会报错")//这段代码报错了，后续代码不会再继续执行了
console.log("呵呵呵")
```

```js
//使用函数计算两个数的和，调用后可以用变量接收
//同步编程的特点：结果可以通过return返回值得到
function fn(a,b){
    return a+b
}
console.log(fn(5,6))//输出11
//回顾：同步读取文件
let data = fs.readFileSync()//data是函数的返回值
//异步读取文件：结果只能在回调函数中得到
fs.readFile(path,(err,result)=>{
    console.log(result)
})
```

异步：一段代码的执行需要一定的时间，或者出错了不会影响后续代码的执行，后续的代码会直接执行，不会等待这一段代码，无法通过返回值的形式获取函数结果。如果想要操作这个结果，必须在回调函数内部进行。

```js
let s=5
setTimeout(function(){
    s=6+7
    console.log(s);//13
},1000)
console.log(s);//5
```

回调地狱：

```js
//异步计算1-100的和 会产生回调地狱问题
        let s = 1;
        setTimeout(function () {
            s = s + 1
            console.log(s)
            setTimeout(function () {
               	...
                s = s + 99
                console.log(s);
                setTimeout(function () {
                    s = s + 100
                    console.log(s);
                }, 200)
            }, 200)
        }, 200)
```

### Promise简介

Promise是异步编程的一种解决方案，比传统的解决方案（回调函数和事件）更合理。ES6将其写进了语言标准，统一了语法。

简单的说Promise就是一个构造函数，里面保存着某个未来才会结束的事情（通常是一个异步操作）的结果。Promise提供统一的API，各种异步操作都可以用同样的方法进行处理。

作用：Promise代表了某个未来将要发生的事件，有了Promise对象，可以将异步操作以同步的流程表达出来，避免了层层嵌套的回调函数。

### Promise语法

基本语法

```js
/*new Promise((resolve,reject)=>{
    resolve()//异步操作执行成功的时候调用
    reject()//异步操作执行失败的时候调用
})*/
let p = new Promise((resolve,reject)=>{
    //异步操作 未来才会结束的事情
    //resolve 这个形参，期待传递一个函数，当未来才会结束的事情成功时，我们就去执行这个resolve
    //reject 这个形参，期待传递一个函数，当未来才会结束的事情失败时，我们就去执行这个reject
})
console.log(p)//Promise { <state>: "pending" }
```

### Promise的状态

promise有三个状态,它一定处于三个状态中的一种状态

- pending 异步操作正在进行中
- fulfilled 异步操作已经成功了
- rejected 已经失败了

状态转换原理:

- 调用resolve函数,则转换未fullfilled状态
- 调用reject函数,则转换程rejected状态
- 状态只能从pending变为fullfilled或者rejected,不可能从rejected变为fullfilled或者从fullfilled变为rejected,不存在既成功又失败

<img src="https://img-blog.csdnimg.cn/20191101143126460.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MDAxMzgxNw==,size_16,color_FFFFFF,t_70" alt="img"  />

<img src="https://pics0.baidu.com/feed/a8ec8a13632762d0168ad1aff06bb3f2503dc6fe.png?token=74467fc35d3562fc986b4f3f28c5e7ac" alt="img"  />

### Promise对象的方法

- **then** 方法(承诺):允许你指定实现承诺时要完成的工作

  - then()方法是异步执行:就是当.then前的方法执行完毕后再执行then()内部的程序,这样就避免了数据没获取到的问题
  - **语法**:

  ```js
  promise对象.then((resolve传递过来的正确结果)=>{
      //必须的参数
     //承诺成功完成时要运行的成功处理函数
  },(reject传递过来的错误结果)=>{
      //可选参数
      //承诺失败时要运行的错误处理函数
  })
  ```
  - **备注**:承诺必须完成(返回一个值)或者被拒绝(返回一个原因),承诺完成或被拒绝时(无论哪一个先发生),Promise对象的then方法都会执行.如果承诺成功完成，则将运行 **then** 方法的履行处理程序函数。如果承诺被拒绝，则将运行 **then** 方法（或 **catch** 方法）的错误处理程序函数。但是,如果**then**方法的第一个参数函数报错,**then**的第二个参数函数无法捕获.

    <img src="https://upload-images.jianshu.io/upload_images/2323089-7f6ecb5daa312950.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200" alt="img" style="zoom: 50%;" />

  - **代码示例**

    ```js
    function eat(duration) {
                return new Promise((resolve, reject) => {
                    setTimeout(resolve, duration)
                })
            }
    eat(1000).then(() => {
        console.log("牛肉面已经做好了~~");//会执行这个:牛肉面已经做好了
    }, () => {
        console.log("打烊了，明天再过来吧~~");
    })
    //如果Promise中的异步操作出错,promise.then(res=>{},err=>{})中的第二个函数将会捕获错误
    function eat(duration) {
                return new Promise((resolve, reject) => {
                    setTimeout(resolv, duration)//这里故意错写成resolv
                })
            }
    eat(1000).then(() => {
        console.log("牛肉面已经做好了~~");
    }, (err) => {
        console.log(err);//打印输出错误:"resolv" is not defined 
    })
    ```

- **catch**方法

  Promise.prototype.catch()方法用于指定发生错误时的回调函数。catch方法接受一个参数，该参数是一个函数，拥有一个参数reason，参数的含义是Promise失败的原因。
  
  ```js
  p.catch(reason=>{});
  //这个方法等价于
  p.then(undefined,reason=>{})
  ```
  
  - 代码示例
  
    ```js
    var p = new Promise(function (resolve, reject) {
        reject(new Error('error'));
    });
    var c = p.then(function (value) {
        console.log('will never run into here');
    }).catch(function (value) {
        console.log('catch error');
        console.log(value.message);
    });
    //上面的代码等同于
    var p = new Promise(function (resolve, reject) {
        reject(new Error('error'));
    });
    var c = p.then(function (value) {
        console.log('will never run into here');
    }).then(undefined, function (value) {
        console.log('catch error');//输出catch error
        console.log(value.message);//输出error
    });
    ```
  
    在实际开发中，一般不会在then方法中定义rejected状态的回调函数（就是第二个参数），而是使用catch方法，这样更接近于同步的写法：try...catch
  
  ### 链式调用
  
  
  
  
  
  
  
  













