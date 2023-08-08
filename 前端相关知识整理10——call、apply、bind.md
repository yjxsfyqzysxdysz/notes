# call、apply、bind



### call

**`Function.prototype.call()`**

**`call()`** 方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数。

#### 语法

```
function.call(thisArg, arg1, arg2, ...)
```

#### 参数

+ `thisArg`

  可选的。在 *`function`* 函数运行时使用的 `this` 值。请注意，`this`可能不是该方法看到的实际值：如果这个函数处于非严格模式下，则指定为 `null` 或 `undefined` 时会自动替换为指向全局对象，原始值会被包装。

+ `arg1, arg2, ...`

  指定的参数列表。

#### 返回值

使用调用者提供的 `this` 值和参数调用该函数的返回值。若该方法没有返回值，则返回 `undefined`。



### apply

**`Function.prototype.apply()`**

`apply()` 方法调用一个具有给定 `this` 值的函数，以及以一个数组（或一个类数组对象）的形式提供的参数。

#### 语法


```
apply(thisArg)
apply(thisArg, argsArray)
```

#### 参数

+ `thisArg`

  在 `func` 函数运行时使用的 `this` 值。请注意，`this` 可能不是该方法看到的实际值：如果这个函数处于非严格模式下，则指定为 `null` 或 `undefined` 时会自动替换为指向全局对象，原始值会被包装。

+ `argsArray` 可选

  一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 `func` 函数。如果该参数的值为 `null`或 `undefined`，则表示不需要传入任何参数。从 ECMAScript 5 开始可以使用类数组对象。浏览器兼容性请参阅本文底部内容。

#### 返回值

调用有指定 **`this`** 值和参数的函数的结果。

> 当第一个参数为 `null` 或 `undefined`时，可以使用数组展开语法实现类似的结果。


### bind

**`Function.prototype.bind()`**

**`bind()`** 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

#### 语法

```
function.bind(thisArg[, arg1[, arg2[, ...]]])
```

#### 参数

+ `thisArg`

  调用绑定函数时作为 `this` 参数传递给目标函数的值。如果使用`new`运算符构造绑定函数，则忽略该值。当使用 `bind` 在 `setTimeout` 中创建一个函数（作为回调提供）时，作为 `thisArg` 传递的任何原始值都将转换为 `object`。如果 `bind` 函数的参数列表为空，或者`thisArg`是`null`或`undefined`，执行作用域的 `this` 将被视为新函数的 `thisArg`。

+ `arg1, arg2, ...`

  当目标函数被调用时，被预置入绑定函数的参数列表中的参数。

#### 返回值

返回一个原函数的拷贝，并拥有指定的 **`this`** 值和初始参数。



### 手写

#### call

```javascript
/**
 *  自定义call实现
 *  @param context   上下文this对象
 *  @param args      动态参数
 */
Function.prototype._call = function (context, ...args) {
  if (!context) {
    context = typeof window === 'undefined' ? global : window
  }
  // context = context || globalThis
  // 防止覆盖掉原有属性
  const key = Symbol()
  // 这里的this为需要执行的方法
  context[key] = this
  // 方法执行
  const result = context[key](...args)
  delete context[key]
  return result
}
```

> 将执行 `function` 挂载 到 `this` 下，`function` 内的 `this` 会指向 `this` 的作用域，从而达到修改 `this` 的效果
>
> ```javascript
> { // 期望的作用域
> 	[symbol]: function(val) {
> 		this.xxx = val
> 	}
> }
> ```

#### apply

```javascript
/**
 * 自定义Apply实现
 *
 * @param context   上下文this对象
 * @param args{[]}      参数数组
 */
Function.prototype._apply = function (context, args) {
  return this.call(context, ...args)
}
```



#### bind

```javascript
/**
 * 自定义bind实现
 *
 * @param context   上下文this对象
 * @returns {Function}
 */
Function.prototype._bind = function (context) {
  return (...args) => {
    this.call(context, ...args)
  }
}
```



------

### 参考资料

+ [MDN call](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
+ [MDN apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
+ [MDN bind](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)