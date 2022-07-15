##  js中 ?.、??、??= 的用法和含义
#### 1. 可选链式操作符 (?.)
可选链操作符 ( ?. ) 允许读取位于连接对象链深处的属性的值，而不必明确验证链中的每个引用是否有效。?. 操作符的功能类似于 . 链式操作符，不同之处在于，在引用为空 (nullish ) (null 或者 undefined) 的情况下不会引起错误，该表达式短路返回值是 undefined。与函数调用一起使用时，如果给定的函数不存在，则返回 undefined。


1.通过连接的对象的引用或函数可能是 undefined 或 null 时，可选链操作符提供了一种方法来简化被连接对象的值访问。

```c
const obj = {
	info: {
		name: 'zhangsan',
		age: 20
	},
	details: {}
}

let someBody = obj.info?.name // zhangsan
let otherInfo = obj.infos?.name // 返回 undefined 而没有报错，保证程序继续执行，而不是中断
```
2.可选链与函数调用

```c
// 函数调用时如果被调用的方法不存在，
// 使用可选链可以使表达式自动返回 undefined 而不是抛出一个异常
let data = someInterface.someMethod?.()
```

3.可选链不能用于赋值语句：
```c
const someObj = {}
someObj?.name = "zhangsan" 
// Uncaught SyntaxError: Invalid left-hand side in assignment
```
4.使用空值合并操作符 和 | 是一个效果

```c
// 空值合并操作符可以在使用可选链时设置一个默认值
let person = {
  name: "zhangsan",
  details: { age: 20 }
}
let add = person?.city ?? '默认值';
console.log(add) // '默认值'
```
#### 2 空值合并运算符 ( ?? )

```c
let b;
let a = 0;
let c = { name:'buzhimingqianduan' }
b = a ?? c;
consile.log(b) // 0
```
##### 上面的例子,当a除了undefined、或者null之外的任何值,b都会等于a,否则就等于c

#### 3 空值赋值运算符 ( ??= )

```c
let b = '你好';
let a = 0
let c = null;
let d = ’123‘
b ??= a;  // b = “你好”
c ??= d  // c = '123'
```
##### 当??=左侧的值为null、undefined的时候,才会将右侧变量的值赋值给左侧变量.其他所有值都不会进行赋值.同样在一些场景下,可以省略很多代码.
[链接1](https://blog.csdn.net/yun_master/article/details/115015113)
[链接2](https://blog.csdn.net/qyl_0316/article/details/118151051)
