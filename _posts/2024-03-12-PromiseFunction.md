---
title: Promise 使用方法
date: 2024-02-11 08:52:00 +0800
categories: [Notes, Front-end]
tags: [promise function]
pin: false
author: jo
toc: true
commments: true
typora-root-url: ../../Jo-CRuiSe.github.io/
math: false
mermaid: false
---

## `Promise`的基本使用

`Promise`是一个构造函数，通过`new`关键字实例化对象

### 语法

```js
new Promise((resolve, reject) => {})
```

- 接受一个函数作为参数
- 在参数函数中接受两个参数
  - resolve
  - reject

### `Promise`实例

`Promise`实例有两个属性

- state
- result

### `Promise`的状态

 - pending
 -  fulfilled
 - rejected

### `Promise`状态的改变

通过调用`resolve()`和`reject()`改变当前Promise对象的状态

```js
const p = new Promise((resolve, reject) => {
  // resolve(); 调用函数，使当前Promise对象的状态改为fulfilled
  // reject(); 调用函数，使当前Promise对象的状态改为rejected
})
console.dir(p); //fulfilled
```

>Promise状态的改变是一次性的
{: .prompt-info}

### `Promise`的结果

```js
const p = new Promise((resolve, reject) => {
  // 调用函数，传递参数，改变丹铅Promise对象的结果
	// resolve('success result');
  // reject('fail result');
})
console.dir(p); 
```

## `Promise`的方法

### `then`方法

返回值是一个`Promise`对象

```js
const p = new Promise((resolve, reject) => {
  resolve('success');
})

p.then((value) => {
  console.log('成功时调用', value);
}), (reason) => {
  console.log('失败时调用', reason);
}
console.dir(p); 
```

>`Promise`状态不改变不会执行`then`方法
{: .prompt-info}

使用`return`可以将实例的状态改为`fulfilled`，`return`的值会作为下一个`then`的参数。在前一个实例中出错则状态改为`rejected`

```js
const p = new Promise((resolve, reject) => {
  resolve('success');
})

p.then((value) => {
  console.log('成功时调用', value);
  return 1;
}), (reason) => {
  console.log('失败时调用', reason);
  return -1;
}.then((value) => {
  console.log('成功时调用', value);
}), (reason) => {
  console.log('失败时调用', reason);
}
```

### `catch`方法

```js
const p = new Promise((resolve, reject) => {
  throw new Error('Error occured');
}).catch ((reason) => {
  console.log('Failed', reason)
})
```

当`Promise`的状态改为`rejected`或`Promise`执行体中出现代码错误时，`catch`方法被执行