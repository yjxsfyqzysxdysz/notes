# JavaScript 数据类型

准确来说，JavaScript 中的类型应该包括这些：

+ [`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number)（数字）
+ [`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)（字符串）
+ [`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Boolean)（布尔）
+ [`Symbol`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)（符号）（ES2015 新增）
+ `Object`（对象）
  + [`Function`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Function)（函数）
  + [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)（数组）
  + [`Date`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Date)（日期）
  + [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp)（正则表达式）
+ [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null)（空）
+ [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)（未定义）
+ [`Error`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Error)（错误）



最新的 ECMAScript 标准定义了 8 种数据类型:

+ 7 种原始类型:
  + [Boolean](https://developer.mozilla.org/zh-CN/docs/Glossary/Boolean)
  + [Null](https://developer.mozilla.org/zh-CN/docs/Glossary/Null)
  + [Undefined](https://developer.mozilla.org/zh-CN/docs/Glossary/undefined)
  + [Number](https://developer.mozilla.org/zh-CN/docs/Glossary/Number)
  + [BigInt](https://developer.mozilla.org/zh-CN/docs/Glossary/BigInt)
  + [String](https://developer.mozilla.org/zh-CN/docs/Glossary/字符串)
  + [Symbol](https://developer.mozilla.org/zh-CN/docs/Glossary/Symbol) 
+ 和 [Object](https://developer.mozilla.org/zh-CN/docs/Glossary/Object)

## 原始值( primitive values )

除 Object 以外的所有类型都是不可变的（值本身无法被改变）。例如，与 C 语言不同，JavaScript 中字符串是不可变的（译注：如，JavaScript 中对字符串的操作一定返回了一个新字符串，原始字符串并没有被改变）。我们称这些类型的值为“原始值”。

### 布尔类型

布尔表示一个逻辑实体，可以有两个值：`true` 和 `false`。

### Null 类型

Null 类型只有一个值： `null`，更多详情可查看 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 和 [Null](https://developer.mozilla.org/zh-CN/docs/Glossary/Null) 。

### Undefined 类型

一个没有被赋值的变量会有个默认值 `undefined`，更多详情可查看 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined) 和 [Undefined](https://developer.mozilla.org/zh-CN/docs/Glossary/undefined)。

### 数字类型

根据 ECMAScript 标准，JavaScript 中只有一种数字类型：基于 IEEE 754 标准的双精度 64 位二进制格式的值（-(253 -1) 到 253 -1）。**它并没有为整数给出一种特定的类型**。除了能够表示浮点数外，还有一些带符号的值：`+Infinity`，`-Infinity` 和 `NaN` (非数值，Not-a-Number)。

要检查值是否大于或小于 `+/-Infinity`，你可以使用常量 [`Number.MAX_VALUE`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_VALUE) 和 [`Number.MIN_VALUE`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_VALUE)。另外在 ECMAScript 6 中，你也可以通过 [`Number.isSafeInteger()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isSafeInteger) 方法还有 [`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER) 和 [`Number.MIN_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_SAFE_INTEGER) 来检查值是否在双精度浮点数的取值范围内。 超出这个范围，JavaScript 中的数字不再安全了，也就是只有 second mathematical interger 可以在 JavaScript 数字类型中正确表现。

数字类型中只有一个整数有两种表示方法： 0 可表示为 -0 和 +0（"0" 是 +0 的简写）。 在实践中，这也几乎没有影响。 例如 `+0 === -0` 为真。 但是，你可能要注意除以0的时候：

```js
42 / +0; // Infinity
42 / -0; // -Infinity
```

尽管一个数字常常仅代表它本身的值，但JavaScript提供了一些[位运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)。 这些位运算符和一个单一数字通过位操作可以用来表现一些布尔值。然而自从 JavaScript 提供其他的方式来表示一组布尔值（如一个布尔值数组或一个布尔值分配给命名属性的对象）后，这种方式通常被认为是不好的。位操作也容易使代码难以阅读，理解和维护， 在一些非常受限的情况下，可能需要用到这些技术，比如试图应付本地存储的存储限制。 位操作只应该是用来优化尺寸的最后选择。

### BigInt 类型

[`BigInt`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt)类型是 JavaScript 中的一个基础的数值类型，可以用任意精度表示整数。使用 BigInt，您可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。BigInt是通过在整数末尾附加 `n `或调用构造函数来创建的。

通过使用常量[`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)，您可以获得可以用数字递增的最安全的值。通过引入 BigInt，您可以操作超过[`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)的数字。您可以在下面的示例中观察到这一点，其中递增[`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)会返回预期的结果:

```
> const x = 2n ** 53n;
9007199254740992n
> const y = x + 1n; 
9007199254740993n
```

可以对`BigInt`使用运算符`+、``*、``-、``**`和`%`，就像对数字一样。BigInt 严格来说并不等于一个数字，但它是松散的。

在将`BigInt`转换为`Boolean`时，它的行为类似于一个数字：`if、``||、``&&、``Boolean 和``!。`

`BigInt`不能与数字互换操作。否则，将抛出[`TypeError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypeError)。

### 字符串类型

JavaScript的字符串类型用于表示文本数据。它是一组16位的无符号整数值的“元素”。在字符串中的每个元素占据了字符串的位置。第一个元素的索引为0，下一个是索引1，依此类推。字符串的长度是它的元素的数量。

不同于类 C 语言，JavaScript 字符串是不可更改的。这意味着字符串一旦被创建，就不能被修改。但是，可以基于对原始字符串的操作来创建新的字符串。例如：

+ 获取一个字符串的子串可通过选择个别字母或者使用 [`String.substr()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substr).
+ 两个字符串的连接使用连接操作符 (`+`) 或者 [`String.concat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/concat).

#### 注意代码中的“字符串类型”！

可以使用字符串来表达复杂的数据。以下是一些很好的性质：

+ 容易连接构造复杂的字串符
+ 字符串容易被调试(你看到的往往在字符串里)
+ 字符串通常是许多APIs的常见标准 ([input fields](https://developer.mozilla.org/en/DOM/HTMLInputElement), [local storage](https://developer.mozilla.org/en/Storage) values, [`XMLHttpRequest`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)当使用`responseText等`的时候回应) 而且他只能与字符串一同使用。

使用约定，字符串一般可以用来表达任何数据结构。这不是一个好主意。例如，使用一个分隔符，可以模拟一个列表（而 JavaScript 数组可能更适合）。不幸的是，当分隔符用于列表中的元素时，列表就会被破坏。 可以选择转义字符，等等。所有这些都需要约定，并造成不必要的维护负担。

表达文本数据和符号数据时候推荐使用字符串。当表达复杂的数据时，使用字符串解析和适当的缩写。

### 符号类型

符号(Symbols)是ECMAScript 第6版新定义的。符号类型是唯一的并且是不可修改的, 并且也可以用来作为Object的key的值(如下). 在某些语言当中也有类似的原子类型(Atoms). 你也可以认为为它们是C里面的枚举类型. 更多细节请看 [Symbol](https://developer.mozilla.org/zh-CN/docs/Glossary/Symbol) 和 [`Symbol`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol) 。

## 对象

在计算机科学中, 对象是指内存中的可以被 [标识符](https://developer.mozilla.org/zh-CN/docs/Glossary/Identifier)引用的一块区域.

### 属性

在 Javascript 里，对象可以被看作是一组属性的集合。用[对象字面量语法](https://developer.mozilla.org/en/JavaScript/Guide/Values,_variables,_and_literals#Object_literals)来定义一个对象时，会自动初始化一组属性。（也就是说，你定义一个var a = "Hello"，那么a本身就会有a.substring这个方法，以及a.length这个属性，以及其它；如果你定义了一个对象，var a = {}，那么a就会自动有a.hasOwnProperty及a.constructor等属性和方法。）而后，这些属性还可以被增减。属性的值可以是任意类型，包括具有复杂数据结构的对象。属性使用键来标识，它的键值可以是一个字符串或者符号值（Symbol）。

ECMAScript定义的对象中有两种属性：数据属性和访问器属性。

#### 数据属性

数据属性是键值对，并且每个数据属性拥有下列特性:

**数据属性的特性(Attributes of a data property)**

| 特性             | 数据类型           | 描述                                                         | 默认值    |
| :--------------- | :----------------- | :----------------------------------------------------------- | :-------- |
| [[Value]]        | 任何Javascript类型 | 包含这个属性的数据值。                                       | undefined |
| [[Writable]]     | Boolean            | 如果该值为 `false，`则该属性的 [[Value]] 特性 不能被改变。   | false     |
| [[Enumerable]]   | Boolean            | 如果该值为 `true，`则该属性可以用 [for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in) 循环来枚举。 | false     |
| [[Configurable]] | Boolean            | 如果该值为 `false，`则该属性不能被删除，并且 除了 [[Value]] 和 [[Writable]] 以外的特性都不能被改变。 | false     |

| 属性       | 类型    | 描述                                          |
| :--------- | :------ | :-------------------------------------------- |
| Read-only  | Boolean | ES5 [[Writable]] 属性的反状态(Reversed state) |
| DontEnum   | Boolean | ES5 [[Enumerable]]  属性的反状态              |
| DontDelete | Boolean | ES5 [[Configurable]] 属性的反状态             |

#### 访问器属性

访问器属性有一个或两个访问器函数 (get 和 set) 来存取数值，并且有以下特性:

| 特性             | 类型                   | 描述                                                         | 默认值    |
| :--------------- | :--------------------- | :----------------------------------------------------------- | :-------- |
| [[Get]]          | 函数对象或者 undefined | 该函数使用一个空的参数列表，能够在有权访问的情况下读取属性值。另见 `get。` | undefined |
| [[Set]]          | 函数对象或者 undefined | 该函数有一个参数，用来写入属性值，另见 `set。`               | undefined |
| [[Enumerable]]   | Boolean                | 如果该值为 `true，则该属性可以用` [for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in) 循环来枚举。 | false     |
| [[Configurable]] | Boolean                | 如果该值为 `false，则该属性不能被删除，并且不能被转变成一个数据属性。` | false     |

注意：这些特性只有 JavaScript 引擎才用到，因此你不能直接访问它们。所以特性被放在两对方括号中，而不是一对。

### "标准的" 对象, 和函数

一个 Javascript 对象就是键和值之间的映射.。键是一个字符串（或者 [`Symbol`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)） ，值可以是任意类型的值。 这使得对象非常符合 [哈希表](http://en.wikipedia.org/wiki/Hash_table)。

函数是一个附带可被调用功能的常规对象。

### 日期

当你想要显示日期时，毋庸置疑，使用内建的 [Date](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Date) 对象。

### 有序集: 数组和类型数组

[数组](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Array)是一种使用整数作为键(integer-key-ed)属性和长度(length)属性之间关联的常规对象。此外，数组对象还继承了 Array.prototype 的一些操作数组的便捷方法。例如, `indexOf` (搜索数组中的一个值) or `push` (向数组中添加一个元素)，等等。 这使得数组是表示列表或集合的最优选择。

[类型数组(Typed Arrays)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays)是ECMAScript Edition 6中新定义的 JavaScript 内建对象，提供了一个基本的二进制数据缓冲区的类数组视图。下面的表格能帮助你找到对等的 C 语言数据类型：

#### TypedArray objects

| Type                                                         | Value Range                     | Size in bytes | Description                                                  | Web IDL type          | Equivalent C type               |
| :----------------------------------------------------------- | :------------------------------ | :------------ | :----------------------------------------------------------- | :-------------------- | :------------------------------ |
| [`Int8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int8Array) | `-128` to `127`                 | 1             | 8-bit two's complement signed integer                        | `byte`                | `int8_t`                        |
| [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array) | `0` to `255`                    | 1             | 8-bit unsigned integer                                       | `octet`               | `uint8_t`                       |
| [`Uint8ClampedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray) | `0` to `255`                    | 1             | 8-bit unsigned integer (clamped)                             | `octet`               | `uint8_t`                       |
| [`Int16Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int16Array) | `-32768` to `32767`             | 2             | 16-bit two's complement signed integer                       | `short`               | `int16_t`                       |
| [`Uint16Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint16Array) | `0` to `65535`                  | 2             | 16-bit unsigned integer                                      | `unsigned short`      | `uint16_t`                      |
| [`Int32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int32Array) | `-2147483648` to `2147483647`   | 4             | 32-bit two's complement signed integer                       | `long`                | `int32_t`                       |
| [`Uint32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint32Array) | `0` to `4294967295`             | 4             | 32-bit unsigned integer                                      | `unsigned long`       | `uint32_t`                      |
| [`Float32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float32Array) | `1.2`×`10-38` to `3.4`×`1038`   | 4             | 32-bit IEEE floating point number (7 significant digits e.g., `1.1234567`) | `unrestricted float`  | `float`                         |
| [`Float64Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array) | `5.0`×`10-324` to `1.8`×`10308` | 8             | 64-bit IEEE floating point number (16 significant digits e.g., `1.123...15`) | `unrestricted double` | `double`                        |
| [`BigInt64Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt64Array) | `-263` to `263-1`               | 8             | 64-bit two's complement signed integer                       | `bigint`              | `int64_t (signed long long)`    |
| [`BigUint64Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigUint64Array) | `0` to `264-1`                  | 8             | 64-bit unsigned integer                                      | `bigint`              | `uint64_t (unsigned long long)` |

### 键控集: Maps, Sets, WeakMaps, WeakSets

这些数据结构把对象的引用当作键，其在ECMAScript第6版中有介绍。当 [`Map`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Map) 和 [`WeakMap`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/WeakMap) 把一个值和对象关联起来的时候， [`Set`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set) 和 [`WeakSet`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WeakSet) 表示一组对象。 Map和WeakMaps之间的差别在于，在前者中，对象键是可枚举的。这允许垃圾收集器优化后面的枚举(This allows garbage collection optimizations in the latter case)。

在纯ECMAScript 5下可以实现Maps和Sets。然而，因为对象并不能进行比较（就对象“小于”示例来讲），所以查询必定是线性的。他们本地实现（包括WeakMaps）查询所花费的时间可能是对数增长。

通常，可以通过直接在对象上设置属性或着使用data-*属性，来绑定数据到DOM节点。然而缺陷是在任何的脚本里，数据都运行在同样的上下文中。Maps和WeakMaps方便将数据私密的绑定到一个对象。 

### 结构化数据: JSON

JSON (JavaScript Object Notation) 是一种轻量级的数据交换格式，来源于 JavaScript 同时也被多种语言所使用。 JSON 用于构建通用的数据结构。参见 [JSON](https://developer.mozilla.org/zh-CN/docs/Glossary/JSON) 以及 [`JSON`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON) 了解更多。

### 标准库中更多的对象

JavaScript 有一个内置对象的标准库。请查看[参考](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)来了解更多对象。

## 数字

根据语言规范，JavaScript 采用“遵循 IEEE 754 标准的双精度 64 位格式”（"double-precision 64-bit format IEEE 754 values"）表示数字。——在JavaScript（除了[`BigInt`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt)）当中，**并不存在整数/整型(Integer)。**因此在处理如下的场景时候，您一定要小心：

```
console.log(3 / 2);             // 1.5,not 1
console.log(Math.floor(3 / 2)); // 1
```

一个看上去是整数的东西，其实都是浮点数。

当然，您也需要小心这种情况：

```js
0.1 + 0.2 = 0.30000000000000004
```

在具体实现时，整数值通常被视为32位整型变量，在个别实现（如某些浏览器）中也以32位整型变量的形式进行存储，直到它被用于执行某些32位整型不支持的操作，这是为了便于进行位操作。

JavaScript 支持标准的[算术运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators)，包括加法、减法、取模（或取余）等等。还有一个之前没有提及的内置对象 [`Math`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)（数学对象），用以处理更多的高级数学函数和常数：

```js
Math.sin(3.5);
var circumference = 2 * Math.PI * r;
```

你可以使用内置函数 [`parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt) 将字符串转换为整型。该函数的第二个可选参数表示字符串所表示数字的基（进制）：

```js
parseInt("123", 10); // 123
parseInt("010", 10); // 10
```

一些老版本的浏览器会将首字符为“0”的字符串当做八进制数字，2013 年以前的 JavaScript 实现会返回一个意外的结果：

```js
parseInt("010");  //  8
parseInt("0x10"); // 16
```

这是因为字符串以数字 0 开头，[`parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)函数会把这样的字符串视作八进制数字；同理，0x开头的字符串则视为十六进制数字。

如果想把一个二进制数字字符串转换成整数值，只要把第二个参数设置为 2 就可以了：

```js
parseInt("11", 2); // 3
```

JavaScript 还有一个类似的内置函数 [`parseFloat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)，用以解析浮点数字符串，与[`parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)不同的地方是，`parseFloat()` 只应用于解析十进制数字。

一元运算符 + 也可以把数字字符串转换成数值：

```js
+ "42";   // 42
+ "010";  // 10
+ "0x10"; // 16
```

如果给定的字符串不存在数值形式，函数会返回一个特殊的值 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)（Not a Number 的缩写）：

```js
parseInt("hello", 10); // NaN
```

要小心NaN：如果把 `NaN` 作为参数进行任何数学运算，结果也会是 `NaN`：

```js
NaN + 5; //NaN
```

可以使用内置函数 [`isNaN()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/isNaN) 来判断一个变量是否为 `NaN`：

```js
isNaN(NaN); // true
```

JavaScript 还有两个特殊值：[`Infinity`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Infinity)（正无穷）和 `-Infinity`（负无穷）：

```js
1 / 0; //  Infinity
-1 / 0; // -Infinity
```

可以使用内置函数 [`isFinite()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/isFinite) 来判断一个变量是否是一个有穷数， 如果类型为`Infinity`, `-Infinity` 或 `NaN则返回false`：

```js
isFinite(1/0); // false
isFinite(Infinity); // false
isFinite(-Infinity); // false
isFinite(NaN); // false

isFinite(0); // true
isFinite(2e64); // true

isFinite("0"); // true
// 如果是纯数值类型的检测，则返回 false：
Number.isFinite("0"); // false
```

**备注：** [`parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt) 和 [`parseFloat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat) 函数会尝试逐个解析字符串中的字符，直到遇上一个无法被解析成数字的字符，然后返回该字符前所有数字字符组成的数字。但是运算符 "+"对字符串的转换方式与之不同， 只要字符串含有无法被解析成数字的字符，该字符串就将被转换成 `NaN`。可分别使用这两种方法解析“10.2abc”这一字符串，并比较得到的结果，来理解这两种方法的区别。

## 字符串

JavaScript 中的字符串是一串[Unicode 字符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Values,_variables,_and_literals#Unicode.E7.BC.96.E7.A0.81)序列。这对于那些需要和多语种网页打交道的开发者来说是个好消息。更准确地说，它们是一串UTF-16编码单元的序列，每一个编码单元由一个 16 位二进制数表示。每一个Unicode字符由一个或两个编码单元来表示。

如果想表示一个单独的字符，只需使用长度为 1 的字符串。

通过访问字符串的 [`length`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/length)（编码单元的个数）属性，可以得到它的长度。

```js
"hello".length; // 5
```

这是我们第一次碰到 JavaScript 对象。我们有没有提过你可以像 [object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object) 一样使用字符串？是的，字符串也有 [methods](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String#Methods)（方法）能让你操作字符串和获取字符串的信息。

```js
"hello".charAt(0); // "h"
"hello, world".replace("world", "mars"); // "hello, mars"
"hello".toUpperCase(); // "HELLO"
```





