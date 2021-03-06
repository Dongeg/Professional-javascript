<h3>js的数据类型：(6种)</h3>

```
  原始类型（5）：number string boolean null undefined
  object类型（1）: Function Array Date .....
```

<h3>js隐式转换</h3>

example1

```
var a='9'+6 //96
var b='9'-6//3
所以可以用这种方法来转换数据类型
var a='num'-0 //字符串转数字
var b=num+''  //数字转字符串
```
example2
```
//严格等于必须类型内容完全相同
'666'!===666
//非严格等于
'1.23'==1.23
0==false
null==undefind

NaN不等于NaN
[1,2]不等于[1,2]
```

example3
```
/*

当我们没有重新定义toString与valueOf时，函数的隐式转换会调用默认的toString方法，它会将函数的定义内容作为字符串返回。
而当我们主动定义了toString/vauleOf方法时，那么隐式转换的返回结果则由我们自己控制了。其中valueOf会比toString后执行

*/
>function fn() {
      return 20;
  }
<undefined
>console.log(fn)
<function fn() {
      return 20;
  }
<undefined
>fn.toString = function() {
     return 10;
 }
<function () {
    return 10;
 }
>console.log(fn)
 10
<undefined
```

<h3>js包装对象</h3>
number string boolean都对应的包装类型
example
```js
var str="deg"

var strobj= new String("deg");

console.log(str)
deg

console.log(strobj)
String0: "d"1: "e"2: "g"length: 3__proto__: String[[PrimitiveValue]]: "deg"

```
```
str
"deg"
console.log(str.length)
VM1782:1 3

str.t=3
3
console
Object {}
console.log(str.t)
VM1825:1 undefined

```
当尝试把基本类型的str当做包装对象一样使用时，例如：str.length; 

解释器会创建一个临时的包装对象，伪代码：

[[tempObj]] = new String(str);

[[tempObj]].length; // 返回具体的length;

delete [[tempObj]]; // 销毁临时对象

重复访问str.length会重复创建这个临时对象。

所以str.t赋值可以成功，但再次访问str.t返回undefined，因为每次创建的临时包装对象都是不同的。

<h3>js类型检测</h3>
1. typeof（多用于判断对象类型）
```js
typeof 100
"number"
typeof true
"boolean"
typeof function(){}
"function"
typeof(undefined)
"undefined"
typeof undefined
"undefined"
typeof new Object()
"object"
typeof [1,2]
"object"
typeof NaN
"number"
typeof null
"object"//历史原因
```
2. obj instanceof Object(判断对象类型)

原理判断左边操作书的原型链上是否有右操作数的prototype
```js
[1,2] instanceof Array//true
```
example2
```js
function Person(){}
function Student(){}

Student.prototype=new Person()

Student.prototype.constructor=Student

var deg=new Student()

console.log(deg instanceof Student)//true
console.log(deg instanceof Person)//true

var loli=new Person()

console.log(loli instanceof Person )//true
console.log(loli instanceof Student )//false
```
3.
```Object.prototype.toString.apply()
console.log(Object.prototype.toString.apply([]))                  //[object Array]
console.log(Object.prototype.toString.apply(function(){}))        //[object Function]
console.log(Object.prototype.toString.apply(null))                //[object Null]
console.log(Object.prototype.toString.apply(undefined))           //[object Undefined]
```
1.type of适合基本类型及function检测，但不适合null，遇到会失效。

2.Class，通过{}.toString拿到，适合内置对象和基元类型，遇到null和undefined失效；

3.instanceof适合自定义对象，也可以用来检测原生对象，在不同iframe和widow间检测时失效

<h3>数组对象函数表达式</h3>

初始化表达式
```
数组      [1,2]         new Array(1,2)

          [1,,,4]       [1,undefined,undefined,4]
对象      {x:1,y:2}     var o.x=1;o.y=2;
```
属性访问表达式
```
var o={x:1}

o.x

o['x']
```
<h4>特殊运算符</h4>

三目运算符
```
var a=true?1:2  //1
```
逗号运算符
```
var a=(1,2,3); //a=3
```
delete运算符
```
var obj={x:1};
obj.x;    //1
delete obj.x;
obj.x;  //undefined
```
```
var obj={};
Object.defineProperty(obj,'x',{
    configurable:false,   //设为false则不可配置
    value:1
});
delete obj.x; //false
obj.x;   //1
```
in 运算符

window.x=1;

'x' in window;  //true

new 运算符 创建实例


var 运算符
```js
(function(){
    var a=b=1;
})()
console.log(b)   //1
console.log(a)   //ht ReferenceError: a is not defined(…)
```
<h3>try-catch语句</h3>
```
    try{
        throw 'my error';
    }
    catch(ex){
        console.log(ex);
    }
    finally{
        console.log('finally')
    }
```
<h3>函数声明和函数表达式</h3>
函数声明
```js
funcction fd(){
//do sth
}
```
函数表达式
```js
var fe=function(){
//do sth
}
```
区别：函数声明会被提升至顶部，函数表达式不会

<h3>for ...in...</h3>
便利结果顺序不定

enumerable为false时不会出现

for in对象属性受原型链影响


```
var obj={x:1,y:2}
for(p in obj){
}
```
<h3>严格模式</h3>
进入严格模式
```
'use strict'
```
严格模式的特性

1.不使用with语句

2.变量必须声明后才能使用

3 arguments
//一般模式下
```js
(function(a){
    arguments[0]=100;
    console.log(a);//100 a和arguments相互影响
})(1)

(function(a){
    arguments[0]=100;
    console.log(a);//undefined
})()
```
//严格模式下
```
'use strict'
(function(a){
  arguments[0]=100;
  console.log(a);//1
})(1)


(function(a){
  arguments[0].x=100;
  console.log(a.x);//100
})(x:1)
```
delete 参数，函数名及不可配置变量会报错 
```
(function(){
  'use strict'
  delete a;//报错
})(1)
```
```
var obj={};
Object.defineProperty(obj,'x',{
    configurable:false,   //设为false则不可配置
    value:1
});
delete obj.x; //报错
```
对象字面量重复属性名报错
```
(function(){
  var obj={x:1,x2};
  console.log(obj.x)//2
})()
```

```
严格模式下
(function(){
'use strict'
  var obj={x:1,x2};
  console.log(obj.x)//报错
})()
```
禁止八进制字面量
```
(function(){
  console.log(0123)//83严格模式下会报错
})()

```
eval函数变为独立作用域

<h3>对象</h3>
```
一个对象有些标签:对对象属性的权限操作 。还有一个原型。如果在对象上找不到属性，就会在原型上查找，在找不到 就沿着原型链 继续往上查找 ，直到原型链末端。还有一个class标签表示对象哪一种类的。还有extensible标签来表示这个对象是否允许继续增加新的属性
对象构造：
除了本身被赋予的值之外，对象还有几个隐藏标签：
proto：对象的对象属性prototype上的赋值，一般是该对象种类的不变属性或方法，例如 new一个猫，猫的颜色和年龄可以作为一般属性，而猫叫，猫吃鱼这种不常变动的属性可以在prototype上赋值，可以节省内存。
class：对象的种类
extensible：是否允许该对象继续增加新的属性

另外对象的值(如 x=1)，也有对应的属性或方法，提供一些访问权限的控制
writable：是否可写
enumerable：是否能够枚举
configurable:是否能被删除
value：值
get/set：获取/设置属性

```
```js
function foo(){}
foo.prototype.z = 3
var obj =new foo();
obj.y = 2;
obj.x = 1;
obj.x; // 1
obj.y; // 2
obj.z; // 3
typeof obj.toString; // ‘function'
'z' in obj; // true
obj.hasOwnProperty('z'); // false

```
创建字面量的方法之一
```
var obj = Object.create({x : 1});
obj.x // 1
typeof obj.toString // "function"
obj.hasOwnProperty('x');// false

```
<h3>js上下文</h3>
```
js有一个抽象的VO对象，来存储函数声明和变量
对于函数对象的VO来讲，分为两个阶段
一.变量初始化阶段
   把一些全局的东西先放进去，以便于在第二个阶段的时候更好的执行
 对于函数
变量初始化阶段会做一些arguments的一些初始化会把一些变量声明和函数声明放进去
VO按照如下顺序填充：
  1.函数参数(若未传入，初始化该参数值为undefined)
  2.函数声明(若发生命名冲突，则会覆盖)（所以才会有函数声明提升）
  3.变量声明(初始化变量值为undefined,若发生命名冲突，则忽略)
函数表达式不会影响VO
二.代码执行阶段
```
<h3>闭包</h3>
```js
var object = { 
   name : '张三', 
   getName : function() { 
       return function() { 
           document.write(this.name);}}} 
object.getName()(); 
请问:执行以上代码，你会看到什么结果？
 正确答案 无结果
```
```
本题的原型是一道经典的闭包思考题。 
如题"return function(){...}"构成了一个明显的闭包，而根据JS的"链式作用域"结构，父对象里面的所有变量，对子对象都是可见的，但是反过来，就不成立。即父对象"看不到"子对象里面的变量。 
现在题目中,假设"getName : function(){...}"是父对象， 
"return function(){...}"就是其子对象，现在子对象需要一个"this.name"，它一定会从父对象"getName()"中寻找，因为父对象里面的变量对它可见，那么请问父对象里面有name吗？很明显，没有。既然没有，this.name怎么取呢？别忘了，有一种变量叫做全局变量，对所有对象都是可见的。因此在这种情况下，"return function(){...}"一定会取全局变量中的name。 
其实取到这个name很简单。 
方法一: 
直接定义全局变量,比如var name = 'blablabla'; 
显示的是全局变量name; 

方法二: 
getName : function() { 
   var that = this;     //加上这句 
   return function() { 
       document.write(that.name); 
   } 
} 
显示的是object里面的name 

方法三: 
getName : function() { 
      var name2 = this.name;    //或者加上这句 
      return function() { 
          document.write(name2); 
     } 
} 
显示的是object里面的name 

方法四:传参 
getName : function(nm){...}
```
















  
