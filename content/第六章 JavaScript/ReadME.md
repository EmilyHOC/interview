### 6.1数据类型
* 基本类型：undefined,number,null,boolean,string,symbol
* 引用类型： Object,function(一种可以执行的对象)，Array(数值下标，内部数据有序)
* typeof(返回数据类型的字符串表达)
* instanceof(判断对象的具体类型)
* ===(可以判断undefined,null)
```var a;
console.log(a,typeof(a));//undefined,"undefined"
```
* 判断a是不是undeined:
```javascript
console.log(typeof a==="undefined")
console.log(typeof a===undefined)
```
* typeof 数组是Object
* typeof可以判断：undefined/数值/字符串/布尔值/function
* 不能判断：null与Object
* 面试题
 > 严格模式？
 * 所有变量先声明
 * 函数中this的默认值是undefined,不是window
 * 禁止使用with语句
 * 不能将eval和arguments用作变量，函数或参数的名称
 > undefined和null的区别
 * undefined代表定义了未赋值
 * null代表定义了并赋值，值为null
 > 什么时候变量赋值为null? 
 * 初始赋值，表明将要赋值的对象
 * 结束前，让对象变成垃圾对象
 ### 6.2引用变量赋值问题
 * 2个引用变量指向同一个对象，通过一个变量修改对象内部的数据，另一个变量看到的是修改之后的数据
    ![](https://user-gold-cdn.xitu.io/2019/1/4/168170342eb1d568?w=395&h=207&f=png&s=19338)
 * 2个引用变量指向同一个对象，让其中一个变量指向另一个对象，另一个引用变量依然指向前一个对象 
    ![](https://user-gold-cdn.xitu.io/2019/1/4/1681707eb08efc95?w=477&h=208&f=png&s=20978)
 ### 6.3关于数据传递的问题
 * 在js调用函数的是值传递还是引用传递
 * 理解一：都是值传递
 * 理解二：可能是值传递，也可能是引用传递(地址值)
 ```javascript
var a=3;
function fn(a){
    a=a+1;
}
fn(a)
console.log(a)//3
function fn2(obj) {//传到obj的是值，只不过这个值是地址
  console.log(obj.name)
}
var obj={name:'Tom'};//obj的内容是地址
fn2(obj)//Tom
```
### 6.4JS引擎如何管理内存
* 释放内存
* 局部变量：函数执行完自动释放
* 对象：成为垃圾对象=>垃圾回收器回收
### 6.5 如何执行函数
* test()直接调用
* obj.test()通过对象调用
* new test()new调用
* test.call/apply(obj) :临时让test称为obj的方法进行调用
```javascript
var obj={};
function test2(){
    this.xxx="yes"
}
test2.call(obj)//让一个函数成为指定任意对象的方法调用，不能obj.test2()调用
```
* 什么是回调函数
> 你定义的，你没有调但是最终执行了
* 常见的回调函数
> dom事件回调函数，定时器回调函数(window),ajax请求回调函数，生命周期回调函数
> IIFE(立即执行)
* 作用：隐藏实现，不会污染外部命名空间，用它来编码js模块
> this是什么？
* 任何函数的本质都是通过某个对象来调用的，如果没有直接指定就是window,所有函数内部都有一个变量this,它的值是调用函数的当前对象
> 如何确定this的值
* test() :window
* p.test() ：p
* new test() :新创建的对象
* p.call(obj):obj
### 6.6 函数高级
#### 1）原型与原型链
* 所有函数都有一个特别的属性: `prototype:显式原型属性` 
* 所有实例对象都有一个特别的属性：`__prpto__:隐式原型`
* 显式原型与隐式原型的关系
   ```
    函数的prototype:定义函数自动赋值，默认为{}=>this.prototype={}
    实例对象的proto:在创建实例对象时自动添加，并赋值为构造函数的prototype值(this.__proto__=Function.prototype)
    ```
* 显式原型和隐式原型图
![](https://user-gold-cdn.xitu.io/2019/1/4/1681739017b91ebd?w=1138&h=596&f=png&s=33959)

* 原型链属性问题
```
    读取对象的属性值时: 会自动到原型链中查找
    设置对象的属性值时: 不会查找原型链, 如果当前对象中没有此属性, 直接添加此属性并设置其值
    方法一般定义在原型中, 属性一般通过构造函数定义在对象本身上
    code:/public/6.6test1原型链——属性问题.html
```
> 面试题
```javascript
 var A = function() {

  }
  A.prototype.n = 1

  var b = new A()

  A.prototype = {
    n: 2,
    m: 3
  }

  var c = new A()
  console.log(b.n, b.m, c.n, c.m)

  /*
   2
   */
  var F = function(){};
  Object.prototype.a = function(){
    console.log('a()')
  };
  Function.prototype.b = function(){
    console.log('b()')
  };
  var f = new F();
  f.a()//a()
  f.b()//报错
  F.a()//a()
  F.b()//b()

```
![](https://user-gold-cdn.xitu.io/2019/1/4/16817459b7d920b7?w=351&h=113&f=png&s=5184)
#### 2）执行上下文与执行上下文栈
* 变量提升与函数提升
  * 变量提升: 在变量定义语句之前, 就可以访问到这个变量(undefined)
  * 函数提升: 在函数定义语句之前, 就执行该函数
  * 先有变量提升, 再有函数提升
* 理解
  * 执行上下文: 由js引擎自动创建的对象, 包含对应作用域中的所有变量属性
  * 执行上下文栈: 用来管理产生的多个执行上下文
* 分类:
  * 全局: window
  * 函数: 对程序员来说是透明的
* 生命周期
  * 全局 : 准备执行全局代码前产生, 当页面刷新/关闭页面时死亡
  * 函数 : 调用函数时产生, 函数执行完时死亡
* 包含哪些属性:
  * 全局 : 
    * 用var定义的全局变量  ==>undefined
    * 使用function声明的函数   ===>function
    * this   ===>window
  * 函数
    * 用var定义的局部变量  ==>undefined
    * 使用function声明的函数   ===>function
    * this   ===> 调用函数的对象, 如果没有指定就是window 
    * 形参变量   ===>对应实参值
    * arguments ===>实参列表的伪数组
* 执行上下文创建和初始化的过程
  * 全局:
    * 在全局代码执行前最先创建一个全局执行上下文(window)
    * 收集一些全局变量, 并初始化
    * 将这些变量设置为window的属性
  * 函数:
    * 在调用函数时, 在执行函数体之前先创建一个函数执行上下文
    * 收集一些局部变量, 并初始化
    * 将这些变量设置为执行上下文的属性
> 面试题
```javascript
var c=1;
function c(c){
    console.log(c)
    var  c=3;
}
c(2)//报错c is not a function
```
#### 3）闭包 
* 理解:
  * 当嵌套的内部函数引用了外部函数的变量时就产生了闭包
  * 通过chrome工具得知: 闭包本质是内部函数中的一个对象, 这个对象中包含引用的变量属性
* 作用:
  * 延长局部变量的生命周期
  * 让函数外部能操作内部的局部变量
* 写一个闭包程序
  ```
  function fn1() {
    var a = 2;
    function fn2() {
      a++;
      console.log(a);
    }
    return fn2;
  }
  var f = fn1();
  f();
  f();
  ```
* 闭包应用:
  * 模块化: 封装一些数据以及操作数据的函数, 向外暴露一些行为
  * 循环遍历加监听
  * JS框架(jQuery)大量使用了闭包
* 缺点:
  * 变量占用内存的时间可能会过长
  * 可能导致内存泄露
  * 解决:
    * 及时释放 : f = null; //让内部函数对象成为垃圾对象
    
* 闭包的生命周期
```
1. 产生: 在嵌套内部函数定义执行完时就产生了(不是在调用)

2. 死亡: 在嵌套的内部函数成为垃圾对象时

<script type="text/javascript">

  function fun1() {

    //问题2: 此时闭包产生了吗? 

    var a = 3;

    function fun2() {

      a++;

      console.log(a);

    }

    return fun2;

  }

  //问题1: 此时闭包产生了吗?   

  var f = fun1();

  //问题3: 此时闭包释放了吗?  

  f();

  f();

  //问题4: 此时闭包释放回收了吗?   

  //问题5: 如何让闭包释放回收呢?

</script>
```
> 面试题
```javascript
var x=10;
function fn(){
    console.log(x)
}
function show(f) {
  var x=20;
  f();
}
show(fn);//10
```
```javascript
var obj={
    fn2:function(){
        console.log(fn2)
    }
}
obj.fn2()//报错
```
```javascript

//代码片段一

var name = "The Window";

var object = {

    name : "My Object",

    getNameFunc : function(){

        return function(){

            return this.name;

        };

    }

};

alert(object.getNameFunc()());  //?

//代码片段二

var name2 = "The Window";

var object2 = {

    name2 : "My Object",

    getNameFunc : function(){

        var that = this;

        return function(){

            return that.name2;

        };

    }

};

alert(object2.getNameFunc()()); //?

```
> 对象的isPrototypeOf()方法和instanceof运算符有哪些区别
```
isProtypeOf()方法检测调用此方法的对象是否存在于指定对象的原型链中，instanceof运算符
用于检测构造函数的原型是否存在于指定对象的原型链，所以最大的区别是检测的目标不同
function child(){};
function ancestor(){};
child.prototype=ancestor;
var obj=new child();
ancestor.isPrototypeOf(obj);//true
obj instanceof ancestor;//false

```
> instanceof运算符的常规用法
```
function child(){};
function ancestor(){};
var obj1=new child();
obj1 instanceof child;//true
obj1 instanceof ancestor;//false
child.prototype={};
var obj2=new child();
obj2 instanceof child;//true
obj1 instanceof child;//false
```
    
