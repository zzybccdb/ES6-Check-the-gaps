# var VS let vs const

#### 三者区别
- var 是 ES6 之前的变量声明的符号.
    - 具有变量提升的特性 (Function 同样具备, 等级更高)
    - 不存在块级作用域的概念 (只有全局作用域和函数作用域)
    - 全局作用域下会默认挂载到 globalThis 下, 浏览器中就是 window 下
- let && const 是 ES6 之后的变量声明符
    - 拥有块级作用域
    - 不存在变量提升, 因此变量名只能在宣告后使用, 提前使用 Reference Error
    - 不会挂载到 globalThis 下
    - const 已经宣告就不可修改(Object, Array 除外)
    - const 实际确保不变的是指向的内存地址内的数据不发生改变.对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。

> ES6 规定暂时性死区和let、const语句不出现变量提升，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。

#### 实例讲解
```javascript
// 对于 for 循环来说, 循环体内部是子作用域, 设置循环变量的是父作用域
for(let i = 0; i < 3; i++) {
    let i = 'abc'
    console.log(i)
}
// 'abc'
// 'abc'
// 'abc'
```

```javascript
// 暂时性死区的概念（temporal dead zone，简称 TDZ）
// 只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}

//  typeof 不在是安全的操作
console.log(typeof undefiendValue) // undifined
{
    console.log(typeof undefiendValue) // Reference Error
    let undefiendValue = 0
}

// ES6 的块级作用域必须有大括号，如果没有大括号，JavaScript 引擎就认为不存在块级作用域。
if (true) let a = 10 // Syntax Error 

if (true) {
  let x = 1; // 正确
}
```

