# ECMAScript6

## ES6中的变量声明

ES5 中，使用 `var` 定义**全局变量**（ var 是 variable 的简写）。

ES6 中，新增了 let 和 const 来定义变量：

-   `let`：定义**局部变量**，替代 var。
-   `const`：定义**常量**（定义后，不可修改）。

### var定义全局变量

看下面的代码

```js
{
    var a = 1;
}
console.log(a); //这里的 a，指的是 区块 里的 a
```

上方代码是可以输出结果的，输出结果为 1。因为 var 是全局声明的，所以，即使是在区块里声明，但仍然在全局起作用。

也就是说：**使用 var 声明的变量不具备块级作用域特性**。

再来看下面这段代码：

```js
var a = 1;
{
    var a = 2;
}
console.log(a); //这里的 a，指的是 区块 里的 a
```

上方代码的输出结果为 2 ，因为 var 是全局声明的。

**总结：**

用 var 定义的全部变量，有时候会污染整个 js 的作用域。我们在如今的实战中，基本都是用的 ES6 语法，所以请**尽量避免**使用 var 定义变量。

### let定义局部变量

代码1：

```js
{
    let a = 'hello';
}
console.log(a); // 打印结果报错：Uncaught ReferenceError: a is not defined
```

代码2：

```js
var a = 2;
{
    let a = 3;
}
console.log(a); // 打印结果：2
```

通过上面两个例子可以看出，**用 let 声明的变量，只在局部（块级作用域内）起作用**。

**经典面试题**：

let 可以防止数据污染，我们来看下面这个 **for 循环**的经典面试题。

用var声明变量：

```js
for (var i = 0; i < 10; i++) {
    console.log('循环体中:' + i);
}
console.log('循环体外:' + i);
```

上方代码可以正常打印结果，且最后一行的打印结果是 10。说明**循环体外**定义的变量 i，是**全局作用域**下的 i。

用let声明变量：

```js
for (let i = 0; i < 10; i++) {
    console.log('循环体中:' + i); // // 每循环一次，就会在 { } 所在的块级作用域中，重新定义一个新的变量 i
}
console.log('循环体外:' + i);//这行代码报错
```

上方代码的关键在于：**每次循环都会产生一个块级作用域，每个块级作用域中会重新定义一个新的变量 i**。

另外，上方代码的最后一行会报错。因为用 let 定义的变量 i，只在`{ }`这个**块级作用域**里生效。

**总结：**我们要习惯用 let 声明，减少 var 声明带来的**污染全局空间**。

为了进一步说明 let 不会带来污染，需要说明的是：当我们定义了`let a = 1`时，如果我们在同一个作用域内继续定义`let a = 2`，是会报错的。

### for循环举例（经典案例）

**代码1：首先用var声明变量**

```html
<!DOCTYPE html>
<html lang="">
    <head>
        <meta />
        <meta />
        <meta />
        <title>Document</title>
    </head>
    <body>
        <input type="button" value="aa" />
        <input type="button" value="bb" />
        <input type="button" value="cc" />
        <input type="button" value="dd" />

        <script>
            var myBtn = document.getElementsByTagName('input');

            for (var i = 0; i < myBtn.length; i++) {
                myBtn[i].onclick = function () {
                    alert(i);
                };
            }
        </script>
    </body>
</html>
```

运行效果如下

![](http://img.smyhvae.com/20190904_1030.gif)

你可能会感到诧异，为何点击任何一个按钮，弹出的内容都是 4 呢？这是因为，我们用 var 定义的变量 i，是在全局作用域声明的。整个代码中，自始至终只有一个变量。

for 循环是同步代码，而 onclick 点击事件是异步代码。当我们还没点击按钮之前，同步代码已经执行完了，变量 i 已经循环到 4 了。

也就是说，上面的 for 循环，相当于如下代码：

```js
var i = 0;
myBtn[0].onclick = function () {
    alert(i);
};
i++;

myBtn[1].onclick = function () {
    alert(i);
};
i++;

myBtn[2].onclick = function () {
    alert(i);
};
i++;

myBtn[3].onclick = function () {
    alert(i);
};
i++; // 到这里，i 的值已经是4了。因此，当我们点击按钮时，i的值一直都是4
```

**代码2：用let声明变量**

```html
<!DOCTYPE html>
<html lang="">
    <head>
        <meta />
        <meta />
        <meta />
        <title>Document</title>
    </head>
    <body>
        <input type="button" value="aa" />
        <input type="button" value="bb" />
        <input type="button" value="cc" />
        <input type="button" value="dd" />

        <script>
            var myBtn = document.getElementsByTagName('input');

            for (let i = 0; i < myBtn.length; i++) {
                myBtn[i].onclick = function () {
                    alert(i);
                };
            }
        </script>
    </body>
</html>
```

![](http://img.smyhvae.com/20190904_1040.gif)

上面这个运行结果，才是我们预期的效果。我们用 let 定义变量 i，在循环的过程中，每执行一次循环体，就会诞生一个新的 i。循环体执行 4 次，就会有四个 i。

也就是说，上面的for循环代码相当于：

```js
{
    let i=0
    myBtn.onclick=function(){
        alert(i)
    }
}
{
    let i=1
    myBtn.onclick=function(){
        alert(i)
    }
}
{
    let i=3
    myBtn.onclick=function(){
        alert(i)
    }
}
{
    let i=4
    myBtn.onclick=function(){
        alert(i)
    }
}
```

### const定义常量

在程序开发中，有些变量是希望声明后，在业务层就不再发生变化，此时可以用 const 来定义**常量**。常量就是值（内存地址）不能变化的量。

举例：

```js
const name = 'smyhvae'; //定义常量
```

用 const 声明的常量，只在局部（块级作用域内）起作用；而且，用 const 声明常量时，必须赋值，否则报错。

### 总结

- let声明变量的特点

  - 变量不能重复声明

  - 块级作用域，变量只在代码块里面有效（包括{}里面，for循环，if条件判断，函数等等），代码块外面无效

  - 不存在变量提升（不会被预解析），存在**暂时性死区**

  - 不影响作用域链

    ```js
    {
        let school="清华大学"
        function fn(){
            console.log(school)//清华大学
        }
        fn()
    }
    ```

- const定义常量的特点：
  - 必须要赋初始值，否则会报错
  - 一般声明的常量名使用大写（非语法要求，潜规则而已）
  - 常量的值不能修改，否则报错
  - 块级作用域
  - 对于数组和对象的元素的修改，不算对常量的修改，不会报错

- let和const的共同点
  - 不属于顶层对象 Window

  - 不允许重复声明

  - 不存在变量提升

  - 暂时性死区

  - 支持块级作用域

相反， 用`var`声明的变量：存在变量提升、可以重复声明、**没有块级作用域**。

- var/let/const 的共同点
  - 全局作用域中定义的变量，可以在函数中使用。
  - 函数中声明的变量，只能在函数及其子函数中使用，外部无法使用。

### 补充知识

#### 暂时性死区

ES6 规定：使用 let/const 声明的变量，会使区块形成封闭的作用域。若在声明之前使用变量，就会报错。

也就是说，在使用 let/const 声明变量时，**变量需要先声明，再使用**（声明语句必须放在使用之前）。这在语法上，称为 “暂时性死区”（ temporal dead zone，简称 TDZ）。

DTC 其实是一种保护机制，可以让我们养成良好的编程习惯。

代码举例：

```js
const name = 'qianguyihao';
function foo() {
    console.log(name);
    const name = 'hello';
}
foo(); // 执行函数后，控制台报错：Uncaught ReferenceError: Cannot access 'name' before initialization
```

#### ES5中如何定义常量

ES5中有`Object.defineProperty`这样一个api，可以定义常量。这个API中接收三个参数。

代码举例：

```js
// 定义常量 PI
Object.defineProperty(window, 'PI', {
    value: 3.14,
    writable: false,
});
console.log(PI); // 打印结果：3.14
PI = 6; //尝试修改常量
console.log(PI); //打印结果：3.14，说明修改失败
```

## 变量的解构赋值

ES6允许按照一定的模式从数组或对象中提取值，对变量进行赋值，这被称为解构赋值

### 数组的解构赋值

```js
const f4=["赵本山","小沈阳","刘能","宋小宝"]
let [zhao,xiao,liu,song]=f4
console.log(zhao)//赵本山
console.log(xiao)//小沈阳
console.log(liu)//刘能
console.log(song)//宋小宝
```

#### 完全解构

变量和值一一对应

```js
let arr = [1,2,3,5,6,undefined]
let [a,b,c,d,e,f]=arr
console.log(a,b,c,d,e,f)//1 2 3 5 6 undefined
```

#### 不完全解构

变量比值的数量少

```js
let arr = [1,2,3,5,6,undefined]
//不需要接收的部分原本需要预留位置
let [,,cc,dd,,]=arr//最后这两个预留的位置可以省略，这样写:let [,,cc,dd]=arr //3 5
console.log(cc,dd)//3 5
//由于是按顺序解构，如果要接收的部分是前几个连续的值，以下这种情况可以不用预留位置
let [aa,bb]=arr
console.log(aa,bb)//1 2
```

#### 解构失败

变量比值的数量多导致某个变量的值为undefined，或者这个变量对应的数据本身的值就是undefined，都叫做解构失败

```js
let arr=[2,3,5,undefined]
let [aaa,bbb,ccc,ddd,eee]=arr
console.log(aaa,bbb,ccc,ddd,eee)//2 3 5 undefined undefined
/*变量ddd对应的值本身就是undefined，变量eee解构的结果为undefined，相当于let eee=arr[4],没有arr[4]这个数据所以是undefined*/
//这两种情况都叫做解构失败
```

#### 解构默认值

直接在变量后面赋值默认值,当解构赋值失败或者解构的值严格等于undefined时,解构的默认值才生效

```js
let arr1=["1","2","3"]
let [a1="",a2="",a3="",a4,a5,a6]=arr1
//变量没有默认值时
console.log(a1+a2+a3+a4+a5+a6)//123undefinedundefinedundefined
//给变量添加默认值时
let [a1,a2,a3,a4=2,a5=6,a6=9]=arr1
console.log(a1+a2+a3+a4+a5+a6)//123269
```

#### 数组解构的应用

```js
//作用一:解构数据
//拿到2,4,7,8,10
//方法1:自创
let arr = [1, 2, 3, [4, 5, 6, [7, 8], 9, [10]]]
let [,a,,b]=arr //a=2 b=[4, 5, 6, [7, 8], 9, [10]]
let [c,,,d,,e]=b//c=4 d=[7,8] e=[10]
let [f,g]=d//f=7 g=8
let [h]=e//h=10
console.log(a,c,f,g,h)
//方法2:老师的
let [,a,,[b,,,[c,d],,[e]]]=arr
console.log(a,b,c,d,e)

//作用二:交换数据
//传统方法:
let x=10
let y=20
temp=x
x=y
y=temp
console.log(x,y)//20 10
//数组解构方法
[y,x]=[x,y]
console.log(x,y)//20 10
```

### 对象的解构赋值

对象的解构不是顺序解构,不需要缺省值

语法:

```js
let {key1:变量名1,key2:变量名2,key3:变量名3}={key1:val1,key2:val2,key3:val3}
//key是模式的一部分,对应的是obj里的key
//通常情况下会把变量名和key保持一致,可以简写成
let {key1,key2,key3}={key1:val1,key2:val2,key3:val3}
```

代码示例:

```js
const zhao={
    name:"赵本山",
    age:"不详",
    xiaopin:function(){
        console.log("我会演小品")
    }
}
let {name,age,xiaopin}=zhao
console.log(name)
consloe.log(age)
xiaopin()
```

#### 解构成功

```js
let obj = {
        age: 10,
        sex: "女",
        name: 'zs',
        hobby: ["学习", "工作"],
        weight:undefined
    }
//左边的变量是根据对应的key值来寻找数据的
let {
    age:a,
    sex:b,
    name:c,
    hobby:d,
}=obj
console.log(a,b,c,d)
//因为数组是按照位置去找值的,所以不需要的值要预留出来,给一个缺省值
//而对象是根据key去找值的,所以不要的值,就直接把这一项对应的key去掉就可以了
let {name:a}=obj
console.log(a)//"zs"
```

#### 解构失败

```js
let obj = {
    age: 10,
    sex: "女",
    name: 'zs',
    hobby: ["学习", "工作"],
    weight:undefined
}
// =左边的变量是根据对应的key值来寻找数据的
// 2、解构失败
let {
    age:b,
    name:a,
    sex:c,
    hobby:d,
    height:e
}=obj
console.log(e);//undefined ===> obj.height
```

#### 解构的默认值

```js
let obj = {
    age: 10,
    sex: "女",
    name: 'zs',
    hobby: ["学习", "工作"],
    weight:undefined
}
// =左边的变量是根据对应的key值来寻找数据的

// 3、解构失败的默认值（解构出来的数据为undefined时才生效）
let {
    age: b,
    name: a,
    sex: c,
    hobby: d,
    height: e=180,
    weight: f=180
} = obj
console.log(e);//180
console.log(f);//180 
```

####　解构的简写形式

```js
// 一般我们会把变量名起的和key一样（如果key和变量名一样，则可以简写 ）
let {
    age,
    name,
    sex,
    hobby,
    height=180,
    weight=180
} = obj
console.log(age, name,sex,hobby,height,weight);
```

#### 对象解构的应用

```js
let  obj={p:["hello",{y:"world"}]};
//得到以下结果
// ["hello",{y:"world"}] 
// hello
// world
let {p}=obj
console.log(p)//["hello",{y:"world"}]
let {p:[a,{y:b}]}=obj
console.log(a,b)//hello world
```

###　字符串的解构赋值

字符串也可以解构赋值,这是因为此时,字符串被转换成了一个类似数组的对象

```js
const [a,b,c,d,e]="hello"
console.log(a,b,c,d,e)//h e l l o
```

类似数组的对象都有一个length属性,因此还可以对这个属性解构赋值

```js
let {length:len}="hello"
console.log(len)// 5
```

### 函数参数的解构赋值

```js
function add([x,y]){
    return x+y
}
add([1,2]) //3
```

上述代码中,函数add的参数表面上是一个数组,但在传入参数的那一刻,数组参数就被解构成变量x和y,对于函数内部的代码来说,他们能感受到的就是x和y

### 字符串的遍历器接口

ES6为字符串添加了遍历器接口,使得字符串可以被for...of和for...in循环遍历

```js
for(let a of "大家好"){
    console.log(a)/* 大
    				家
    				好				*/
}
for(let b in "大家好"){	
    console.log(b)/*0 
                    1
           	        2         	        */
}
```

## 字符串扩展

### 模板字符串

### 字符串新增的方法

- **startsWidth(string[,index])**  --判断字符串是否是以某个字符(串)开头

  ```js
  let str="hello world"
  console.log(str.startsWith("h"))//true 
  console.log(str.startsWith("w",6))//true (从索引为6的位置开始查找)
  ```

- **endsWith(string[,length])**  --判断字符串是否是以某个字符结尾

  ```js
  let str="hello world"
  console.log(str.endsWith("d"))//true 
  console.log(str.endsWith("w",6))//false (从开头往后截取长度为6的部分,判断是不是以w结尾)
  console.log(str.endsWith(" ",6))//true
  ```

- **includes(string[,index])**  --判断字符串是否包含某个字符

  ```js
  let str="hello world"
  console.log(str.includes("w"))// true
  console.log(str.includes("w",7))//false (从索引为7的位置开始往后查找看看是否包含w这个字符
  ```

- **padStart(maxlength[,string])**  --先判断字符串的长度是小于指定的长度,小于则在开头填充指定的字符以达到指定的长度  

  ```js
  let str1 = str.padStart(12,"哈哈")
  console.log(str1)//'哈hello world'
  ```

- **padEnd(maxlength[,string])**  --先判断字符串的长度是小于指定的长度,小于则在结尾填充指定的字符以达到指定的长度

  ```js
  let str2 = str.padEnd(12,"哈哈")
  console.log(str2) //'hello world哈'
  ```

- **repeat(num)**  --将字符串重复num次

  ```js
  let str3 = str.repeat(3)
  console.log(str3) //hello worldhello worldhello world
  ```

- **trimStart()** || **trimEnd()**  --消除头部/尾部空格

  ```js
  let str4 = " |hello world|  " 
  console.log(str4.trimStart())  //'|hello world|  '
  console.log(str4.trimEnd()) //' |hello world|'
  ```

## 数组扩展





