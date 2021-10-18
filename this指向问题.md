## this 指向问题
牢记 7 个特殊点, 箭头函数, new, bind, call, apply, (obj.), 直接调用

### 箭头函数
箭头函数排在第一个是因为它的 this 不会被改变，所以只要当前函数是箭头函数，那么就不用再看其他规则了。
箭头函数的 this 是在创建它时外层 this 的指向。这里的重点有两个：

1. 创建箭头函数时，就已经确定了它的 this 指向。
2. 箭头函数内的 this 指向外层的 this。

所以要知道箭头函数的 this 就得先知道外层 this 的指向，需要继续在外层应用七步口诀。

### new
当使用 new 关键字调用函数时，函数中的 this 一定是 JS 创建的新对象。

> Q: “如果使用 new 关键调用箭头函数，是不是箭头函数的 this 就会被修改呢？”。
A: 箭头函数不能当构造函数

### bind
bind 是指 Function.prototype.bind()。多次 bind 时只认第一次 bind 的值

**箭头函数中 this 不会被修改**

> bind 与 new

```javascript
function func() {
console.log(this, this.__proto__ === func.prototype)
}

boundFunc = func.bind(1)
new boundFunc() // Object true，new 优先
```

### apply && call
apply() 和 call() 的第一个参数都是 this
1. apply 调用时实参是放到数组中的
2. call 调用时实参是逗号分隔的。

**箭头函数中 this 不会被修改**
**bind 函数中 this 不会被修改**

### obj.
```javascript
function func() {
  console.log(this.x)
}

obj = { x: 1 }
obj.func = func
obj.func() // 1
```

**这里就不用代码例证箭头函数和 bind 函数的优先级更高了，有兴趣可自行尝试吧。**

### 直接调用
直接调用时，this 将指向全局对象。在浏览器环境中全局对象是 Window，在 Node.js 环境中是 Global。

先来个简单的例子。

### 不在函数里
不在函数中的场景，可分为浏览器的 <script /> 标签里，或 Node.js 的模块文件里。

1、在 <script /> 标签里，this 指向 Window。

2、在 Node.js 的模块文件里，this 指向 Module 的默认导出对象，也就是 module.exports。

### 非严格模式
严格模式是在 ES5 提出的。在 ES5 规范之前，也就是非严格模式下，this 不能是 undefined 或 null。
所以在非严格模式下，通过上面七步口诀，如果得出 this 指向是 undefined 或 null，那么 this 会指向全局对象。
在浏览器环境中全局对象是 Window,在 Node.js 环境中是 Global。
例如下面的代码，在非严格模式下，this 都指向全局对象。

```javascript
function a() {
    console.log("function a:", this)
    ;(() => {
        console.log("arrow function: ", this)
    })()
}
a() // window, window
a.bind(null)() // window, window
a.bind(undefined)() // window, window
a.bind().bind(2)() // window, window
a.apply() // window, window

"use strict"
function a() {
  console.log("function a:", this)
  ;(() => {
    console.log("arrow function: ", this)
  })()
}
a() // undefinedund, undefined
a.bind(null)() // null, null
a.bind(undefined)() // undefined, undefined
a.bind().bind(2)() // undefined, undefined
a.apply() // undefined, undefined
```

### 测试
```javascript
obj = {
  func() {
    const arrowFunc = () => {
      console.log(this._name)
    }
    return arrowFunc
  },
  _name: "obj",
}
obj.func()() // obj
func = obj.func
func()() // undefined
obj.func.bind({ _name: "newObj" })()() // newObj
obj.func.bind()()() // undefined
obj.func.bind({ _name: "bindObj" }).apply({ _name: "applyObj" })() // // bindObj
```