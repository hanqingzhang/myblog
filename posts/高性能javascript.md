## 1.Dom编程
用脚本进程dom操作的代价昂贵，是web应用中最常见的性能瓶颈

原因：

天生就慢，浏览器中通常会把dom和js独立实现，两个相互独立的功能，通过接口彼此连接，就会产生消耗。有个贴切的比喻，dom和js各自想象成一个岛屿，之间用收费桥连接。js每次访问dom,都途经这个桥，缴纳费用，次数越多，费用越多。

###  dom访问与修改

#### 1. innerHtml优于dom

innerHtml优于document.createElement(),单就性能而言，innerHTML都要比createElement创建元素在append进dom中快一些

##### 2. 节点克隆

element.cloneNode()代替document.createElement()，先创建需要重复的节点，在重复拷贝

##### 3. html集合


##### 4. 遍历html

**1）获取dom元素**

从某个dom元素开始，操作周围的元素，或者递归查找所有子节点，使用childNodes得到元素集合或nextSibling获取每个相邻元素。

nextSibling 属性可返回某个元素之后紧跟的节点（处于同一树层级中）

老版本ie推荐nextSibling

**2)children代替childNodes**

使用children代替childNodes，因为childNodes会包含文本节点（空格）和注释节点，还需要自己额外过滤这些节点，children已经帮我们过滤掉这些节点了，而且使用的过滤方法效率很高。

**3）querySelectorAll()更有效率,代替getElement**


querySelectorAll() 方法返回文档中匹配指定 CSS 选择器的所有元素

注：与querySelector区别表示文档中与指定的一组CSS选择器匹配的第一个元素的 html元素Element对象。

原因：query选择符选出来的元素及元素数组是静态的，而getElement这种方法选出的元素是动态的。
什么叫静态的？意思是指选出的所有元素的数组，不会随着文档操作而改变。

eg:
```
<ul>
        <li>111</li>
        <li>222</li>
        <li>333</li>
    </ul>

```

querySelector
```
var ul=document.querySelector('ul');
        var list=ul.querySelectorAll('li');
        for(var i=0;i<list.length;i++){
            ul.appendChild(document.createElement('li'));
        }//这个时候就创建了3个新的li，添加在ul列表上。
        console.log(list.length) //输出的结果仍然是3，不是此时li的数量6


```
getElements
```
var ul=document.getElementsByTagName('ul')[0];
        var list=ul.getElementsByTagName('li');
        for(var i=0;i<5;i++){
            ul.appendChild(document.createElement('li'));
        }   
        console.log(list.length)//此时输出的结果就是3+5=8


```

###  重排与重绘

浏览器下载完页面所有组件，html,css,js,images,生成两个内部数据结构

dom树-----表示页面结构

渲染树----表示dom节点如何显示

dom树中的节点对应渲染树中的节点，
渲染树的节点称为盒，一旦dom树和渲染树构建完成，浏览器开始绘制页面。

dom的变化影响了元素的几何变化（宽和高），浏览器会使渲染树中受到影响的部分失效，重新构造渲染树，这个过程是==重排==。

完成重排后，浏览器重新绘制受影响的部分到屏幕，是==重绘==


引起重排

- 页面首次渲染。

- 浏览器窗口大小发生改变。

- 元素尺寸或位置发生改变。

- 元素内容变化（文字数量或图片大小等等）。

- 元素字体大小变化。

- 添加或者删除可见的DOM元素。

- 激活CSS伪类（例如：:hover）。

- 设置style属性

- 查询某些属性或调用某些方法。



###  事件委托

## 2.算法和流程控制

-  for,while和do-while性能相当
- 避免使用for-in循环，==除非遍历一个属性量未知的对象==

es5:for-in 遍历的对象便不局限于数组，还可以遍历对象。

原因：for-in每次迭代操作会同时搜索实例或者原型属性， for-in 循环的每次迭代都会产生更多开销，因此要比其他循环类型慢，一般速度为其他类型循环的 1/7。因此，除非明确需要迭代一个属性数量未知的对象，否则应避免使用 for-in 循环。如果需要遍历一个数量有限的已知属性列表，使用其他循环会更快

-  foreach没有for性能好

不能中断循环（使用break或者return）

在 for 循环中可以使用 continue，break 来控制循环和跳出循环，这个是 forEach 所不具备的。【在这种情况下，从性能的角度考虑，for 是要比 forEach 有优势的。（一个长度为100的数据，你for循环到35的时候，实现了功能，达到了目的的话，这个时候可以 break 跳出循环的；使用 forEach 的话，是不能退出循环本身的。）】

- for-of

es6里引入了一种新的循环方法，它就是for-of循环，它既比传统的for循环简洁，同时弥补了forEach和for-in循环的短板。

- switch 与if else 效率比较

使用if-else 或者switch 是基于测试条件的数量：条件数量较大，倾向于使用switch 而不是if-else。这通常归结到代码的易读性，如果条件较少时，if-else 容易阅读，而条件较多时switch更容易阅读。

优化if-else 的目标总是最小化找到正确分支之前所判断条件体的数量。最简单的优化方法是将最常见的条件体放在首位。


- 判断条件多时，使用查找算法，eg,二分查找，优于switch 与if else 

- memoization （常用于递归）

一种优化技术，主要用于通过存储昂贵的函数调用的结果来加速计算机程序，并在再次发生相同的输入时返回缓存的结果。

Memoization是JavaScript中的一种技术，通过缓存结果并在下一个操作中重新使用缓存来加速查找费时的操作。

在这里，memoization通常会缩短执行时间并影响我们应用程序的性能。当我们知道一组输入将产生某个输出时，memoization最有效。
遵循最佳实践，应该在纯函数上实现memoization。纯函数输入什么就返回什么，不存在副作用。
记住这个是==以空间换速度==，所以最好确定你是否值得那么做，有些场景很有必要使用。
==在处理递归函数时，Memoization最有效，递归函数用于执行诸如GUI渲染，Sprite和动画物理等繁重操作。==


## 3.编程实践


#### - setTimeout()和settimeInterval()传递函数而不是字符串作为参数

引申：
用setTimeout()方法来模拟setInterval()与setInterval()之间的什么区别？

精确度问题？

微任务和宏任务问题？

macro-task(宏任务)：包括整体代码script，setTimeout，setInterval

micro-task(微任务)：Promise，process.nextTick，类似node.js版的"setTimeout"，在事件循环的下一次循环中调用 callback 回调函数。

同步>异步

主任务>微任务>宏任务

```
console.log('script start');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

Promise.resolve().then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});

console.log('script end');

```
结果：script start, script end, promise1, promise2, setTimeout 

```
console.log('1');

setTimeout(function() {
    console.log('2');
    process.nextTick(function() {
        console.log('3');
    })
    new Promise(function(resolve) {
        console.log('4');
        resolve();
    }).then(function() {
        console.log('5')
    })
})
process.nextTick(function() {
    console.log('6');
})
new Promise(function(resolve) {
    console.log('7');
    resolve();
}).then(function() {
    console.log('8')
})

setTimeout(function() {
    console.log('9');
    process.nextTick(function() {
        console.log('10');
    })
    new Promise(function(resolve) {
        console.log('11');
        resolve();
    }).then(function() {
        console.log('12')
    })
})

```
结果：同步任务1，7，微任务nextTick和promise.then()6,8,宏任务setTimeout，里面作为一个新的内容2，4，3，5，9，11，10，12

#### - 尽量使用直接量创建对象和数组

```
// 使用直接量
var obj = {
  name: 'zzz',
  age: 24,
};
var arr = ["nicholas", 50, true];

// 不使用直接量
var obj = new Object();
obj.name = 'zzz';
obj.age = 24;

var arr = new Array();
arr[0] = "nicholas";
arr[1] = 50;
arr[2] = true;
```

#### - 避免做重复的工作，当需要检测浏览器的时候，可使用延迟加载或条件预加载

最常见的重复工作就是浏览器探测，基于浏览器的功能作分支判断导致产生大量代码。

一个页面假如有多次调用 addHandler 函数添加事件，那么每次浏览器都会做判断，来执行哪一个方法。事实上每次的判断结果都是一样的。有几种方法可以避免。

```
function addHandler(target, eventType, handler) { 
  if (target.addEventListener) {  // DOM2 Events
    target.addEventListener(eventType, handler, false);
  } else {  // IE
    target.attachEvent('on' + eventType, handler);
  }
}   

addHandler(document, 'click', function() {
  console.log('hello world');
});
```

方法一：延迟加载

延迟加载，也称惰性加载，惰性载入等。延迟加载意味着在信息被使用前不会做任何操作：

```
function addHandler(target, eventType, handler) { 
  if (target.addEventListener) {  // DOM2 Events
    addHandler = function(target, eventType, handler) {
      target.addEventListener(eventType, handler, false);
    };
  } else {  // IE
    addHandler = function(target, eventType, handler) {
      target.attachEvent('on' + eventType, handler);
    };
  }
  addHandler(target, eventType, handler);
}    

addHandler(document, 'click', function() {
  console.log('hello world');
});

addHandler(window, 'keydown', function() {
  console.log('key down');
});
//方法在第一个调用的时候，会做一次判断决定使用哪种方法去绑定时间处理器，然后原始addHandler会被新的addHandler函数覆盖，最后一步调用新的函数，并传入原始参数。随后每次调用addHandler()都不会再做检测，因为检测代码已经被新的函数覆盖。

//第一次总会消耗较长的时间，因为需先检测再调用完成任务。之后会变快。
```
方法二：条件预加载

条件预加载会在脚本加载期间提前检测，而不会等到函数被调用：

```
var addHandler = document.addEventListener ? 
  function(target, eventType, handler) {
    target.addEventListener(eventType, handler, false);
  }:
  function(target, eventType, handler) {
    target.attachEvent('on' + eventType, handler);
  };    

addHandler(document, 'click', function() {
  console.log('hello world');
});
//这个例子就是先检查 addEventListener()是否存在，然后根据结果指定函数。

//条件预加载确保所有函数调用消耗的时间相同，代价是需要在脚本加载时就检测。适用于一个函数马上就要被用到，并且在整个页面的生命周期中频繁出现的场景。
```




#### - 在做数学计数时，考虑使用直接操作数字的二进制形式的位运算

i&1可以判断奇偶，奇时返回true，偶时返回false
#### - js的原始方法比你写的任何代码都快，尽量使用原生方法。

特别是数学运算。内置Math对象的方法。dom运算，querySelector()和querySelectorAll()

Math 对象用于执行数学任务。

使用 Math 的属性和方法的语法：
```
var pi_value=Math.PI;
var sqrt_value=Math.sqrt(15);
```
Math 对象并不像 Date 和 String 那样是对象的类，因此没有构造函数 Math()，像 Math.sin() 这样的函数只是函数，不是某个对象的方法。您无需创建它，通过把 Math 作为对象使用就可以调用其所有属性和方法。
https://www.w3school.com.cn/jsref/jsref_obj_math.asp
