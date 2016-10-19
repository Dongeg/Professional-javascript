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
    configurable:false,   //设为false则不可删除
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
```
(function(){
    var a=b=1;
})()
console.log(b)   //1
console.log(a)   //ht ReferenceError: a is not defined(…)
```






















  
