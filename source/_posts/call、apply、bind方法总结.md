---
title: call、apply、bind方法总结
date: 2019-6-3 07:47:53
tags: ES5数组方法
keywords:
description:
summary:  ES5中数组的方法都不会修改他们调用的原始数组,而传递给这些方法的函数是可以修改这些数组的
categories: JavaScript
---





> 语法:function.call(thisArg, arg1, arg2, ...)

```js
 //@ thisArg this指向
 * @arg 指定的参数 arg1, arg2.....argN
```

call是属于所有Function的方法,也就是Funtion.prototype.call<br>

call 方法的 length 属性是 1。

`**call()**` 方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数。

注意:与 [`apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) 方法类似，只有一个区别，就是 `call()` 方法接受的是**一个参数列表**，而 `apply()` 方法接受的是**一个包含多个参数的数组**。

<br>

示例:

```js
function fun() {
    console.log(this.name, arguments)
}
let obj = {
    name: 'cheng',
    age: 20
}
fun.call(obj, 'cai', 'cai','24','18')
//cheng [Arguments] { '0': 'cai', '1': 'cai', '2': '24', '3': '18' }
```



`apply` 与 [`call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call) 非常相似，不同之处在于提供参数的方式。`apply` 使用参数数组而不是一组参数列表。`apply` 可以使用数组字面量（array literal），如 `fun.apply(this, ['eat', 'bananas'])`，或数组对象， 

如  `fun.apply(this, new Array('eat', 'bananas'))`。

你也可以使用 [`arguments`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)对象作为 `argsArray` 参数。 `arguments` 是一个函数的局部变量。 它可以被用作被调用对象的所有未指定的参数。 这样，你在使用apply函数的时候就不需要知道被调用对象的所有参数。 你***可以使用arguments来把所有的参数传递给被调用对象***。 被调用对象接下来就负责处理这些参数。

<br>

从 ECMAScript 第5版开始，可以使用任何种类的类数组对象，就是说只要有一个 `length` 属性和`(0..length-1)`范围的整数属性。例如现在可以使用 [`NodeList`](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList) 或一个自己定义的类似 `{'length': 2, '0': 'eat', '1': 'bananas'}` 形式的对象。

<br>

通过语法就可以看出 call 和 apply 的在参数上的一个区别：

> 1. call 的参数是一个列表，将每个参数一个个列出来
> 2. apply 的参数是一个数组，将每个参数放到一个数组中

<br>

> **语法**:func.apply(thisArg, [argsArray]);

```js
apply() 方法调用一个函数, 其具有一个指定的this值，以及作为一个数组（或类似数组的对象）提供的参数。
 @param thisArg this指向
 @param argsArray 参数数组
```

```js
thisArg
```

必选的。在 *func* 函数运行时使用的 `this` 值。请注意，`this`可能不是该方法看到的实际值：如果这个函数处于[非严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)下，则指定为 `null` 或 `undefined` 时会自动替换为指向全局对象，原始值会被包装。

```js
argsArray
```

可选的。一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 `func` 函数。如果该参数的值为 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 或  [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)，则表示不需要传入任何参数。从ECMAScript 5 开始可以使用类数组对象

示例:

```js
var array = ['a', 'b'];
var elements = [0, 1, 2];
array.push.apply(array, elements);
console.info(array); // ["a", "b", 0, 1, 2]
//[ 'a', 'b', 0, 1, 2 ]
```

<br>

> ```js
> 语法:function.bind(thisArg[, arg1[, arg2[, ...]]])
> ```