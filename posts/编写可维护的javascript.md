1.命名

驼峰式大小写，变量和函数区分开

```
var count=10;

function getName(){
    return count;
}

var MAX_COUNT=10；
```

函数命名开头，can,has,is返回布尔值，get返回非布尔值，set保存一个值

2.null（当做对象的占位符）

null是一个特殊值，常与undefined搞混，应用场景：

- 用来初始化一个变量，这个变量可能赋值为一个对象
- 用来和一个已经初始化的变量比较，这个变量可以是一个对象也可以不是
- 当函数的参数期望是对象时，用作参数传入
- 当函数的返回值期望是对象时，用作返回值传出

不应当使用null:

- 不要使用null来检测是否传入了某个参数
- 不要用null来检测一个未初始化的变量

```
//好的用法，用来初始化一个变量，这个变量可能赋值为一个对象
var person=null;
//好的用法，当函数的返回值期望是对象时，用作返回值传出
function getPerson(){
    if(condition){
        return new Person("zzz")
    }else{
        return null;
    }
}
//好的用法，用来和一个已经初始化的变量比较，这个变量可以是一个对象也可以不是
var person=getPerson()
if(person!==null){
    dosomething();
}
//不好的用法，和未初始化变量比较
var person;
if(person!=null){
    dosomething()
}
//不好的用法，检测是否传入了参数
function doSomething(a,b,c,d){
    if(d!==null){
        dosomething()
    }
}
```
3.undefined

undefined是一个特殊值，我们经常和null搞混，null==undefined结果是true,然而他俩用处各不相同，那些未初始化的变量，都有一个初始值，即undefined,表示这个变量等待赋值。
```
//不好的写法
var person;
console.log(person====undefined)//true
```
不建议使用undefined!!!

不管是值为undefined的变量，还是未声明的变量，typeof的结果都是undefined

```
//foo未声明
var person;
console.log(typeof person) //undefined
console.log(typeof foo)  //undefined

```
在语句中使用foo,会报错，而person不会
通过禁止使用undefined，确保只有未声明的时候才会undefined,将变量初始值赋值为null,表明可能为对象，typeof nulll返回object,与undefined区分

```
var person=null
```
4.判断数组是否是数组

es5中Array.isArray() 用于确定传递的值是否是一个 Array。

Object.prototype.toString.call(o)=='[object Array]'

5.检测对象中是否有某个属性

1）使用in关键字。

该方法可以判断对象的自有属性和继承来的属性是否存在。

2）使用对象的hasOwnProperty()方法。

该方法只能判断自有属性是否存在，对于继承属性会返回false。