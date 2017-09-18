1. [元素浮动后display的值为？](#)
2. [可继承的样式有哪些？](#)
3. [解释一下浏览器如何解析css的](#)
4. [css选择器的权重](#)
5. [写一个闭包函数，并解释其原理,如何解决闭包带来的问题](#)
6. [将arguments转换为数组](#)
7.
```
<div id="wrapper"></div>
```
 [写一段代码给这个元素添加100个p元素](#/)
8.
```
var array = new Array(30);
array.forEach(function(v){
    console.log(v)
})
```
[解释上面代码的输出，如何改正？](#)
9. [ data-属性是什么，如何获得js和jq？](#)
10. [reflow（重排）和repaint（重绘）的区别是什么，应怎么避免？](#)？
11. [css优化方法有哪些？](#)
12. [.call和.apply,bind和proxy的作用和区别](#)？
13. v-if和v-show的区别？


---
### 1.元素浮动后display的值为？
 block
 
### 2.可继承的样式有哪些
* 可继承的样式：
1. 关于文字排版的属性如：font,word-break,letter-spacing,text-align,text-rendering,
		word-spacing,white-space,text-indent,text-transform,text-shadow
2. line-height
3. color
4. visibility
5. cursor

* 不可继承的样式：border padding margin width height ;

### 3.解释一下浏览器如何解析css的

### 4.css选择器的权重
*	优先级就近原则,同权重情况下样式定义最近者为准;
	!important > 内联 >  id > class > tag

### 5.写一个闭包函数，并解释其原理，如何解决闭包带来的问题
    
```
for(var i=0;i<2;i++){
      setTimeout(function(){
              console.log(i);
        },0);
}
上面这段代码的执行结果是2,2而不是0,1，因为等for循环出来后，执行setTimeout中的函数时，
i的值已经变成了2，这就是没有隔离作用域所造成的，请看下面代码：
for(var i=0;i<2;i++){
      (function(i){
             setTimeout(function(){
              console.log(i);
        },0)
    })(i);
}
这样就会输出0,1，我们的立即执行函数创建了一个作用域，隔离了外界的作用域。

```
### 6.将arguments转换为数组
1. arguments这个类数组

* 它将实参以数组的形式保存着,还可以像数组一样访问实参,如arguments[0];
* 它也有自己独特的属性，如：callee，
* 它的长度是实参的个数。补充：那arguments.callee.length又是什么呢？arguments.callee是当前正在执行的函数的引用，类似function.length，那就是形参的个数。
2. 将arguments转换为真正的数组的方法
 * Array.prototype.slice.apply(arguments)这是运行效率比较快的方法（看别人资料说的）,为什么不是数组也可以，因为arguments对象有length属性，而这个方法会根据length属性,返回一个具有length长度的数组。若length属性不为number，则数组长度返回0;所以其他对象只要有length属性也是可以的哟，如对象中有属性0,对应的就是arr[0],即属性为自然数的number就是对应的数组的下标，若该值大于长度，当然要割舍啦。
* Array.prototype.concat.apply(thisArg,arguments)。,thisArg是新的空数组，apply方法将函数this指向thisArg，arguments做为类数组传参给apply。根据apply的方法的作用,即将Array.prototype.slice方法在指定的this为thisArg内调用，并将参数传给它。用此方法注意:若数组内有数组，会被拼接成一个数组。原因是apply传参的特性。
* 用循环，因为arguments类似数组可以使用arguments[0]来访问实参，那么将每项赋值给新的数组每项，直接复制比push要快，若实参有函数或者对象，就要深拷贝。

### 7.写一段代码给这个元素添加100个p元素

```
<div id="wrapper"></div>
```

```
function addP(id,e){
        var wrap = document.getElementById(id);
        for(var i=0;i<100;i++){
            var ele = document.createElement(e);
            wrap.appendChild(ele);
        }
    }
    addP("wrapper","p");
```


### 8.解释上面代码的输出，如何改正
```
var array = new Array(30);
array.forEach(function(v){
    console.log(v)
})
```
输出undefined，因为array是一个有30个子元素undefined 的数组没有具体值，所以遍历输出也只有undefined
### 9. data-属性是什么，如何获得js和jq？
**定义和用法：**

data-* 属性用于存储页面或应用程序的私有自定义数据。
data-* 属性赋予我们在所有 HTML 元素上嵌入自定义 data 属性的能力。
存储的（自定义）数据能够被页面的 JavaScript 中利用，以创建更好的用户体验（不进行 Ajax 调用或服务器端数据库查询）。
data-* 属性包括两部分：
属性名不应该包含任何大写字母，并且在前缀 "data-" 之后必须有至少一个字符
属性值可以是任意字符串
注释：用户代理会完全忽略前缀为 "data-" 的自定义属性。
### 10.reflow（重排）和repaint（重绘）的区别是什么，应怎么避免？
**明确概念：**

首先我们要明确页面在文档加载完成之后到完全显示中间的过程是1.根据文档生成DOM树（包括display:none的节点）2.在DOM树基础上根据节点的几何属性（margin/padding/width/height等)生成render树（不包括display:none、head节点但会包含visibility:hidden节点）3.在render树基础上进行进一步渲染包括color,outline等样式

* reflow:当render树中的一部分或者全部因为大小边距等问题发生改变而需要重建的过程叫做回流

* repaint:当元素的一部分属性发生变化，如外观背景色不会引起布局变化而需要重新渲染的过程叫做重绘
* 
**避免：**
1. 将那些改变样式的操作集合在一次完事，直接改变className或者cssText

2. 让要操作的元素进行离线处理，处理完事以后再一起更新

（1）使用DocumentFragment进行缓存操作，引发一次回流和重绘

课外延伸：

DocumentFragment 节点不属于文档树，继承的 parentNode 属性总是 null。

不过它有一种特殊的行为，该行为使得它非常有用，即当请求把一个 DocumentFragment 节点插入文档树时，插入的不是 DocumentFragment 自身，而是它的所有子孙节点。这使得 DocumentFragment 成了有用的占位符，暂时存放那些一次插入文档的节点。它还有利于实现文档的剪切、复制和粘贴操作。

其实他就是一个游离在DOM树外面的容器，所以你在把它插入文档节点之前，随便给他增删节点都不会引起回流

（2）使用display:none,只引发两次回流和重绘。道理跟上面的一样。因为display:none的元素不会出现在render树

（3）使用cloneNode和replaceChild技术，引发一次回流和重绘（这条其实没太明白）

3. 不要经常访问会引起浏览器flush队列的属性，非要高频访问的话建议缓存到变量；

4. 将需要多次重排的元素，position属性设为absolute或fixed，这样此元素就脱离了文档流，它的变化不会影响到其他元素。例如有动画效果的元素就最好设置为绝对定位；

5. 尽量不要使用表格布局，如果没有定宽表格一列的宽度由最宽的一列决定，那么很可能在最后一行的宽度超出之前的列宽，引起整体回流造成table可能需要多次计算才能确定好其在渲染树中节点的属性，通常要花3倍于同等元素的时间。


### 11.css优化方法有哪些？

### 12..call和.apply,bind和$.proxy的作用和区别
1. **作用**

在 javascript 中，call 和 apply 都是为了改变某个函数运行时的上下文（context）而存在的，换句话说，就是为了改变函数体内部 this 的指向。
2.  **apply、call 的区别**

其中 this 是你想指定的上下文，他可以是任何一个 JavaScript 对象(JavaScript 中一切皆对象)，call 需要把参数按顺序传递进去，而 apply 则是把参数放在数组里。　　

JavaScript 中，某个函数的参数数量是不固定的，因此要说适用条件的话，当你的参数是明确知道数量时用 call 。
而不确定的时候用 apply，然后把参数 push 进数组传递进去。当参数数量不确定时，函数内部也可以通过 arguments 这个数组来遍历所有的参数。
3. **常用方法**

1）数组之间追加

```
var array1 = [12 , "foo" , {name "Joe"} , -2458]; 
var array2 = ["Doe" , 555 , 100]; 
Array.prototype.push.apply(array1, array2); 
/* array1 值为  [12 , "foo" , {name "Joe"} , -2458 , "Doe" , 555 , 100] */
```

2）获取数组中的最大值和最小值

```
var  numbers = [5, 458 , 120 , -215 ]; 
var maxInNumbers = Math.max.apply(Math, numbers),   //458
    maxInNumbers = Math.max.call(Math,5, 458 , 120 , -215); //458
```
number 本身没有 max 方法，

但是 Math 有，我们就可以借助 call 或者 apply 使用其方法。

3）验证是否是数组（前提是toString()方法没有被重写过）


```
functionisArray(obj){ 
    return Object.prototype.toString.call(obj) === '[object Array]' ;
}
```

4）类（伪）数组使用数组方法


```
var domNodes = Array.prototype.slice.call(document.getElementsByTagName("*"));
```

Javascript中存在一种名为伪数组的对象结构。比较特别的是 arguments 对象，还有像调用 getElementsByTagName , document.childNodes 之类的，它们返回NodeList对象都属于伪数组。不能应用 Array下的 push , pop 等方法。
但是我们能通过 Array.prototype.slice.call 转换为真正的数组的带有 length 属性的对象，这样 domNodes 就可以应用 Array 下的所有方法了。
4. **面试题**（定义一个log方法，使其替代console.log方法）

```
function log(){
  var args = Array.prototype.slice.call(arguments);
  args.unshift('(app)');
 
  console.log.apply(console, args);
};
log(1,2);  //(app) 1 2
```
5. **bind**

bind() 方法与 apply 和 call 很相似，也是可以改变函数体内 this 的指向。

MDN的解释是：bind()方法会创建一个新函数，称为绑定函数，当调用这个绑 定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为 this，传入 bind() 方法的第二个以及以后的参数加上绑定函数运行时 本身的参数按照顺序作为原函数的参数来调用原函数。

* 例子

```
var foo = {
    bar : 1,
    eventBind: function(){
        $('.someClass').on('click',function(event) {
            /* Act on the event */
            console.log(this.bar);      //1
        }.bind(this));
    }
}
```
在上述代码里，bind() 创建了一个函数，当这个click事件绑定在被调用的时候，它的 this 关键词会被设置成被传入的值（这里指调用bind()时传入的参数）。因此，这里我们传入想要的上下文 this(其实就是 foo )，到 bind() 函数中。然后，当回调函数被执行的时候， this 便指向 foo 对象。
```
var bar = function(){
console.log(this.x);
}
var foo = {
x:3
}
bar(); // undefined
var func = bar.bind(foo);
func(); // 3
```
这里我们创建了一个新的函数 func，当使用 bind() 创建一个绑定函数之后，它被执行的时候，它的 this 会被设置成 foo ， 而不是像我们调用 bar() 时的全局作用域。

**注意：在Javascript中，多次 bind() 是无效的。**


 6. **apply、call、bind比较**

```
var obj = {
    x: 81,
};
 
var foo = {
    getX: function() {
        return this.x;
    }
}
 
console.log(foo.getX.bind(obj)());  //81
console.log(foo.getX.call(obj));    //81
console.log(foo.getX.apply(obj));   //81
```

三个输出的都是81，但是注意看使用 bind() 方法的，他后面多了对括号。

也就是说，区别是，当你希望改变上下文环境之后并非立即执行，而是回调执行的时候，使用 bind() 方法。而 apply/call 则会立即执行函数。

 

再总结一下：

==apply 、 call 、bind 三者都是用来改变函数的this对象的指向的；
apply 、 call 、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文；
apply 、 call 、bind 三者都可以利用后续参数传参；
bind 是返回对应函数，便于稍后调用；apply 、call 则是立即调用 。==

7. **$proxy()定义和用法**

$.proxy 方法接受一个已有的函数，并返回一个带特定上下文的新的函数。
该方法通常用于向上下文指向不同对象的元素添加事件。
提示：如果您绑定从 $.proxy 返回的函数，jQuery 仍然可以通过传递的原先的函数取消绑定正确的函数。

```
语法 1
$(selector).proxy(function,context)
```
```
语法 2
$(selector).proxy(context,name)
```

```
<script>
$(document).ready(function(){
  var objPerson = {
    name: "John Doe",
    age: 32,
    test: function(){
      $("p").after("Name: " + this.name + "<br> Age: " + this.age);
    }
  };
  $("button").click($.proxy(objPerson,"test"));
});
</script>
</head>
<body>

<button>执行 test 函数</button>
<p></p>

</body>
```

### 13.v-if和v-show的区别