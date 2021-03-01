API  说明  版本前端相关知识整理9——API

## 字符串

### String

#### String 方法

| API                   | 说明                          |
| --------------------- | ----------------------------- |
| String.fromCharCode() | 通过一串 Unicode 创建字符串。 |

#### String  实例属性

| 属性                         | 说明                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| String.prototype.constructor | 用于创造对象的原型对象的特定的函数                           |
| String.prototype.length      | 返回了字符串的长度                                           |
| N                            | 用于访问第N个位置的字符，其中N是小于 `length` 和 0之间的正整数。这些属性都是“只读”性质，不能编辑 |

#### String 实例方法

| API                                                          | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| String.prototype.charAt(index)                               | 返回特定位置的字符。                                         |
| String.prototype.charCodeAt(index)                           | 返回表示给定索引的字符的Unicode的值。                        |
| String.prototype.concat(str2, [, ...strN])                   | 连接两个字符串文本，并返回一个新的字符串。                   |
| String.prototype.includes(searchString[, fromIndex])         | 判断一个字符串里是否包含其他字符串。                         |
| String.prototype.endsWith(searchString[, length])            | 判断一个字符串的是否以给定字符串结尾，结果返回布尔值。       |
| String.prototype.indexOf(searchValue [, fromIndex])          | 从字符串对象中返回首个被发现的给定值的索引值，如果没有找到则返回-1。 |
| String.prototype.lastIndexOf(searchValue [, fromIndex])      | 从字符串对象中返回最后一个被发现的给定值的索引值，如果没有找到则返回-1。 |
| String.prototype.match(regexp)                               | 使用正则表达式与字符串相比较。                               |
| String.prototype.padEnd(targetLength [, padString])          | 在当前字符串尾部填充指定的字符串， 直到达到指定的长度。 返回一个新的字符串。 |
| String.prototype.padStart(targetLength [, padString])        | 在当前字符串头部填充指定的字符串， 直到达到指定的长度。 返回一个新的字符串。 |
| String.prototype.repeat(count)                               | 返回指定重复次数的由元素组成的字符串对象。                   |
| String.prototype.replace(regexp\|substr, newSubStr\|function) | 被用来在正则表达式和字符串直接比较，然后用新的子串来替换被匹配的子串。 |
| String.prototype.search(regexp)                              | 对正则表达式和指定字符串进行匹配搜索，返回第一个出现的匹配项的下标。 |
| String.prototype.slice(beginIndex[, endIndex])               | 摘取一个字符串区域，返回一个新的字符串。                     |
| String.prototype.split([separator[, limit]])                 | 通过分离字符串成字串，将字符串对象分割成字符串数组。         |
| String.prototype.startsWith(searchString[, position])        | 判断字符串的起始位置是否匹配其他字符串中的字符。             |
| String.prototype.substr(start[, length])<br />String.prototype.substring(indexStart[, indexEnd]) | 通过指定字符数返回在指定位置开始的字符串中的字符。           |
| String.prototype.toUpperCase()                               | 将字符串转换成大写并返回。                                   |
| String.prototype.toLowerCase()                               | 将字符串转换成小写并返回。                                   |
| String.prototype.toString()                                  | 返回用字符串表示的特定对象。重写 Object.prototype.toString 方法。 |
| String.prototype.trim()                                      | 从字符串的开始和结尾去除空格。参照部分 ECMAScript 5 标准。   |
| String.prototype.trimStart()<br />String.prototype.trimLeft() | 从字符串的左侧去除空格。                                     |
| String.prototype.trimEnd()<br />String.prototype.trimRight() | 从字符串的右侧去除空格。                                     |
| String.prototype.valueOf()                                   | 返回特定对象的原始值。重写 Object.prototype.valueOf 方法。   |

#### String 转义字符

|           Code           |       Output        |
| :----------------------: | :-----------------: |
|           `\0`           |       空字符        |
|           `\'`           |       单引号        |
|           `\"`           |      `双引号`       |
|           `\\`           |       反斜杠        |
|           `\n`           |        换行         |
|           `\r`           |       `回车`        |
|           `\v`           |     垂直制表符      |
|           `\t`           |     水平制表符      |
|           `\b`           |        退格         |
|           `\f`           |        换页         |
|         `\uXXXX`         |     unicode 码      |
| `\u{X}` ... `\u{XXXXXX}` |  unicode codepoint  |
|          `\xXX`          | Latin-1 字符(x小写) |

### RegExp

#### RegExp 静态属性

| 属性               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| RegExp.lastIndex() | 是正则表达式的一个可读可写的整型属性，用来指定下一次匹配的起始索引 |

> 只有正则表达式使用了表示全局检索的 "`g`" 标志时，该属性才会起作用。此时应用下面的规则：
>
> + 如果 `lastIndex` 大于字符串的长度，则 `regexp.test` 和 `regexp.exec` 将会匹配失败，然后 `lastIndex` 被设置为 0。
> + 如果 `lastIndex` 等于字符串的长度，且该正则表达式匹配空字符串，则该正则表达式匹配从 `lastIndex` 开始的字符串。（then the regular expression matches input starting at `lastIndex`.）
> + 如果 `lastIndex` 等于字符串的长度，且该正则表达式不匹配空字符串 ，则该正则表达式不匹配字符串，`lastIndex` 被设置为 0.。
> + 否则，`lastIndex` 被设置为紧随最近一次成功匹配的下一个位置。

#### RegExp 实例方法

| API                                                          | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| RegExp.prototype.exec(str)                                   | 在一个指定字符串中执行一个搜索匹配。返回一个结果数组或 `null` |
| RegExp.prototype.test(str)                                   | 执行一个检索，用来查看正则表达式与指定的字符串是否匹配。返回 `true` 或 `false`。 |
| RegExp.prototype\[@@match]()<br/>regexp\[Symbol.match](str)  | 对正则表达式匹配字符串时，**`[@@match]()`**方法用于获取匹配结果。<br/>match 方法会返回一个数组，它包括整个匹配结果，和通过捕获组匹配到的结果，如果没有匹配到则返回null |
| RegExp.prototype\[@@matchAll]()<br/>regexp\[Symbol.matchAll](str) | **`[@@matchAll]`**方法返回对字符串使用正则表达式的所有匹配项。<br />返回一个迭代器 |
| RegExp.prototype\[@@replace]()<br /> regexp\[Symbol.replace](str, newSubStr\|function) | **`[@@replace]()`** 方法会在一个字符串中用给定的替换器，替换所有符合正则模式的匹配项，并返回替换后的新字符串结果。用来替换的参数可以是一个字符串或是一个针对每次匹配的回调函数。<br />返回用替换器替换相应匹配项后的新字符串 |
| RegExp.prototype\[@@search]()<br />regexp\[Symbol.search](str) | **`[@@search]()`** 方法执行了一个在给定字符串中的一个搜索以取得匹配正则模式的项。<br />返回**整数**，如果成功的话，`[@@search]()` 返回该正则模式的第一个匹配项的在字符串中的位置索引。否则将返回-1。 |
| RegExp.prototype\[@@split]()<br />regexp\[Symbol.split](str[, limit]) | **`[@@split]()`** 方法切割 `String` 对象为一个其子字符串的数组 。<br />返回 包含其子字符串的Array |
| RegExp.prototype.toString()                                  | **`toString()`** 返回一个表示该正则表达式的字符串。          |

## 数字和日期

###  Number

#### Number 属性

| 属性                     | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| Number.MAX_SAFE_INTEGER  | JavaScript 中最大的安全整数 (2^53^ - 1)。<br />是一个值为 9007199254740991的常量。<br />因为Javascript的数字存储使用了`IEEE 754中规定的双精度浮点数数据类型，而这一数据类型能够安全存储 `-(2^53^ - 1)` 到 `2^53^ - 1 之间的数值（包含边界值）。<br />这里安全存储的意思是指能够准确区分两个不相同的值 |
| Number.MAX_VALUE         | 能表示的最大正数。最小的负数是 -MAX_VALUE。<br />`MAX_VALUE` 属性值接近于 `1.79E+308`。大于 `MAX_VALUE` 的值代表 "`Infinity`"。<br />因为 `MAX_VALUE` 是 `Number` 对象的一个静态属性，所以你应该直接使用`Number.MAX_VALUE` ，而不是作为一个创建的 `Number` 实例的属性。 |
| Number.MIN_SAFE_INTEGER  | JavaScript 中最小的安全整数 (-(2^53^ - 1)).                  |
| Number.MIN_VALUE         | 能表示的最小正数即最接近 0 的正数 (实际上不会变成 0)。最大的负数是 -MIN_VALUE。 |
| Number.NaN               | 特殊的“非数字”值。和`NaN`相同                                |
| Number.NEGATIVE_INFINITY | 特殊的负无穷大值，在溢出时返回该值。                         |
| Number.POSITIVE_INFINITY | 特殊的正无穷大值，在溢出时返回该值。                         |

#### Number 方法

| API                           | 说明                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| Number.isNaN(value)           | 确定传递的值是否是 NaN。                                     |
| Number.isFinite(value)        | 确定传递的值类型及本身是否是有限数。                         |
| Number.isInteger(value)       | 确定传递的值类型是“number”，且是整数。                       |
| Number.isSafeInteger(value)   | 确定传递的值是否为安全整数( -`(253 - 1)` 至 `253 - 1之间`)。 |
| Number.parseFloat(str)        | 和全局对象 parseFloat() 一样<br />给定值被解析成浮点数，如果无法被解析成浮点数，则返回`NaN` |
| Number.parseInt(str[, radix]) | 和全局对象 parseInt() 一样<br />依据指定基数 [ 参数 **radix** 的值]，把字符串 [ 参数 **string** 的值] 解析成整数。<br />将`string`视为`radix`进制的数值转换为 `10进制` 的数值 |

### BigInt

**`BigInt`** 是一种内置对象，它提供了一种方法来表示大于 `253 - 1` 的整数。这原本是 Javascript中可以用 `Number` 表示的最大数字。**`BigInt`** 可以表示任意大的整数。

可以用在一个整数字面量后面加 `n` 的方式定义一个 `BigInt` ，如：`10n`，或者调用函数`BigInt()`。

+ 与 `Number` 的不同点：
  + 不能用于 `Math` 对象中的方法；
  + 不能和任何 `Number` 实例混合运算，两者必须转换成同一种类型。
  + 在两种类型来回转换时要小心，因为 `BigInt` 变量在转换成 `Number` 变量时可能会丢失精度。

+ 类信息

  + 使用 `typeof` 测试时， `BigInt` 对象返回 "bigint" 。

+ 运算

  可以和 `BigInt` 一起使用：
  + `+`、``*``、``-``、``**``、``%`` 。
  + 除 `>>>` （无符号右移）之外的 位操作 也可以支持。
  + `BigInt` 不支持单目 (`+`) 运算符。
  + `/` 操作符对于整数的运算也没问题。可是因为这些变量是 `BigInt` 而不是 `BigDecimal` ，该操作符结果会向零取整，也就是说不会返回小数部分。

  当使用 `BigInt` 时，带小数的运算会被取整。

+ 比较

  + `BigInt` 和 `Number` 不是严格相等的，但是宽松相等的。
  + `Number` 和 `BigInt` 可以进行比较。
  + 两者也可以混在一个数组内并排序。
  + 注意被 `Object` 包装的 `BigInt`s 使用 object 的比较规则进行比较，只用同一个对象在比较时才会相等。

+ 条件

  + BigInt 在需要转换成 `Boolean `的时表现跟 `Number `类似：如通过 `Boolean `函数转换；用于 `Logical Operators`  `||`, `&&`, 和 `!` 的操作数；或者用于在像 `if statement` 这样的条件语句中。

  基本同 `Number` 无区别。

#### 静态方法

| API                           | 说明                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| BigInt.asIntN(width, bigint)  | 将 BigInt 值转换为一个 -2^width-1^ 与 2^width-1^-1 之间的有符号整数。 |
| BigInt.asUintN(width, bigint) | 将一个 BigInt 值转换为 0 与 2^width-1^ 之间的无符号整数。    |

用于限定最大值范围，设定上限。

#### 实例方法

| API                                | 说明                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| BigInt.prototype.toString([radix]) | 返回以指定基数(base)表示指定数字的字符串。覆盖 Object.prototype.toString() 方法。<br />`radix` 可选，介于 2 到 36 之间的整数，指定用于表示数值的基数。 |
| BigInt.prototype.valueOf()         | 返回指定对象的基元值。 覆盖 Object.prototype.valueOf() 方法。 |

+ 在 JSON 中使用

  对任何 `BigInt` 值使用 `JSON.stringify()` 都会引发 `TypeError`，因为默认情况下 `BigInt` 值不会在 `JSON` 中序列化。但是，如果需要，可以实现 `toJSON` 方法。

  ```javascript
  BigInt.prototype.toJSON = function() { return this.toString(); }
  ```

### Math

#### Math 属性

| 属性         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| Math.E       | 欧拉常数，也是自然对数的底数，约等于 2.718。                 |
| Math.LN2     | 2 的自然对数，约等于 0.693。ln2                              |
| Math.LOG2E   | 以 2 为底的 E 的对数，约等于 1.443。log2(e) = 1/ln2          |
| Math.LN10    | 10 的自然对数，约等于 2.303。ln10                            |
| Math.LOG10E  | 以 10 为底的 E 的对数，约等于 0.434。log10(e) = 1/ln10       |
| Math.PI      | 圆周率，一个圆的周长和直径之比，约等于 3.14159。             |
| Math.SQRT1_2 | 二分之一 ½ 的平方根，同时也是 2 的平方根的倒数 ，约等于 0.707。 |
| Math.SQRT2   | 2 的平方根，约等于 1.414。                                   |

#### Math 方法

| API                       | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| Math.abs(x)               | 返回一个数的绝对值。                                         |
| Math.sign(x)              | 返回一个数的符号，得知一个数是正数、负数还是 0。<br />此函数共有5种返回值, 分别是 **1, -1, 0, -0, NaN.** 代表的各是**正数, 负数, 正零, 负零, NaN**。<br />传入该函数的参数会被**隐式转换**成数字类型。 |
| Math.pow(x, y)            | 返回一个数 x 的 y 次幂。                                     |
| Math.sqrt(x)              | 返回一个数的平方根。                                         |
| Math.hypot([x[, y[, …]]]) | 返回其所有参数平方和的平方根。                               |
| Math.max([x[, y[, …]]])   | 返回零到多个数值中最大值。                                   |
| Math.min([x[, y[, …]]])   | 返回零到多个数值中最小值。                                   |
| Math.random()             | 返回一个 0 到 1 之间的伪随机数。[0,1)                        |
| Math.toSource()           | 返回字符串 "Math"。                                          |
| Math.ceil(x)              | 返回大于一个数的最小整数，即一个数向上取整后的值。           |
| Math.floor(x)             | 返回小于一个数的最大整数，即一个数向下取整后的值。           |
| Math.round(x)             | 返回四舍五入后的整数。                                       |
| Math.trunc(x)             | 返回将数字的小数部分去掉，只保留整数部分。<br />仅仅是**删除**掉数字的小数部分和小数点，不管参数是正数还是负数。<br />传入该方法的参数会被隐式转换成数字类型。 |
| Math.acos(x)              | 返回一个数的反余弦值。                                       |
| Math.acosh(x)             | 返回一个数的反双曲余弦值。                                   |
| Math.asin(x)              | 返回一个数的反正弦值。                                       |
| Math.asinh(x)             | 返回一个数的反双曲正弦值。                                   |
| Math.atan(x)              | 返回一个数的反正切值。                                       |
| Math.atanh(x)             | 返回一个数的反双曲正切值。                                   |
| Math.atan2(y, x)          | 返回 y/x 的反正切值。                                        |
| Math.cos(x)               | 返回一个数的余弦值。                                         |
| Math.cosh(x)              | 返回一个数的双曲余弦值。                                     |
| Math.sin(x)               | 返回一个数的正弦值。                                         |
| Math.sinh(x)              | 返回一个数的双曲正弦值。                                     |
| Math.tan(x)               | 返回一个数的正切值。                                         |
| Math.tanh(x)              | 返回一个数的双曲正切值。                                     |
| Math.cbrt(x)              | 返回一个数的立方根。                                         |
| Math.exp(x)               | 返回欧拉常数的参数次方，Ex，其中 x 为参数，E 是欧拉常数（2.718...，自然对数的底数）。 |
| Math.expm1(x)             | 返回 exp(x) - 1 的值。                                       |
| Math.log(x)               | 返回一个数的自然对数（㏒e，即 ㏑）。                         |
| Math.log1p(x)             | 返回一个数加 1 的和的自然对数（㏒e，即 ㏑）。                |
| Math.log10(x)             | 返回一个数以 10 为底数的对数。                               |
| Math.log2(x)              | 返回一个数以 2 为底数的对数。                                |
| Math.fround(x)            | 返回最接近一个数的单精度浮点型表示。                         |
| Math.clz32(x)             | 返回一个 32 位整数的前导零的数量。                           |
| Math.imul(x, y)           | 返回 32 位整数乘法的结果。                                   |

### Date

`Date` 对象则基于 `Unix Time Stamp`，即自1970年1月1日（UTC）起经过的毫秒数。

+ 如果没有输入任何参数，则Date的构造器会依据系统设置的当前时间来创建一个Date对象。
+ 如果提供了至少两个参数，其余的参数均会默认设置为 1（如果没有指定 day 参数）或者 0（如果没有指定 day 以外的参数）。
+ JavaScript的时间由世界标准时间（UTC）1970年1月1日开始，用毫秒计时，一天由 86,400,000 毫秒组成。`Date` 对象的范围是 -100,000,000 天至 100,000,000 天（等效的毫秒值）。
+ `Date` 对象为跨平台提供了统一的行为。时间属性可以在不同的系统中表示相同的时刻，而如果使用了本地时间对象，则反映当地的时间。
+ `Date` 对象支持多个处理 UTC 时间的方法，也相应地提供了应对当地时间的方法。UTC，也就是我们所说的格林威治时间，指的是time中的世界时间标准。而当地时间则是指执行JavaScript的客户端电脑所设置的时间。
+ 以一个函数的形式来调用 `Date` 对象（即不使用 `new` 操作符）会返回一个代表当前日期和时间的字符串。

#### Date 方法

| 方法                                               | 说明                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| Date.now()                                         | 返回自 1970-1-1 00:00:00  UTC（世界标准时间）至今所经过的毫秒数。 |
| Date.UTC(year,month[,date[,hrs[,min[,sec[,ms]]]]]) | 接受和构造函数最长形式的参数相同的参数（从2到7），并返回从 1970-01-01 00:00:00 UTC 开始所经过的毫秒数。 |

#### Date 实例方法

##### 常用API

| API                                                          | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Date.prototype.getTime()<br />Date.prototype.valueOf()       | 返回从1970-1-1 00:00:00 UTC（协调世界时）到该日期经过的毫秒数，对于1970-1-1 00:00:00 UTC之前的时间返回负值。 |
| Date.prototype.getDate()                                     | 根据本地时间返回指定日期对象的月份中的第几天（1-31）。       |
| Date.prototype.getDay()                                      | 根据本地时间返回指定日期对象的星期中的第几天（0-6，0 代表星期日）。 |
| Date.prototype.getFullYear()                                 | 根据本地时间返回指定日期对象的年份（四位数年份时返回四位数字），最小可以显示100，小于100的如99，返回1999。 |
| Date.prototype.getHours()                                    | 根据本地时间返回指定日期对象的小时（0-23）。                 |
| Date.prototype.getMilliseconds()                             | 根据本地时间返回指定日期对象的毫秒（0-999）。                |
| Date.prototype.getMinutes()                                  | 根据本地时间返回指定日期对象的分钟（0-59）。                 |
| Date.prototype.getMonth()                                    | 根据本地时间返回指定日期对象的月份（0-11）。                 |
| Date.prototype.getSeconds()                                  | 根据本地时间返回指定日期对象的秒数（0-59）。                 |
| Date.prototype.setDate(dayValue)                             | 根据本地时间为指定的日期对象设置月份中的第几天。(如果为 `dayValue` 指定0，那么日期就会被设置为上个月的最后一天) |
| Date.prototype.setFullYear(yearValue[, monthValue[, dayValue]]) | 根据本地时间为指定日期对象设置完整年份（四位数年份是四个数字）。 |
| Date.prototype.setHours(hoursValue[, minutesValue[, secondsValue[, msValue]]]) | 根据本地时间为指定日期对象设置小时数。                       |
| Date.prototype.setMilliseconds(millisecondsValue)            | 根据本地时间为指定日期对象设置毫秒数。                       |
| Date.prototype.setMinutes(minutesValue[, secondsValue[, msValue]]) | 根据本地时间为指定日期对象设置分钟数。                       |
| Date.prototype.setMonth(monthValue[, dayValue])              | 根据本地时间为指定日期对象设置月份。                         |
| Date.prototype.setSeconds(secondsValue[, msValue])           | 根据本地时间为指定日期对象设置秒数。                         |
| Date.prototype.setTime(timeValue)                            | 通过指定从 1970-1-1 00:00:00 UTC 开始经过的毫秒数来设置日期对象的时间，对于早于 1970-1-1 00:00:00 UTC的时间可使用负值。 |
| Date.prototype.toJSON()                                      | 使用 toISOString() 返回一个表示该日期的字符串。为了在 JSON.stringify() 方法中使用。 |
| Date.prototype.toDateString()                                | 以美式英语和人类易读的形式返回一个日期对象日期部分的字符串   |
| Date.prototype.toISOString()                                 | 返回一个 ISO格式的字符串： **YYYY-MM-DDTHH:mm:ss.sssZ**。时区总是UTC（协调世界时），加一个后缀“Z”标识 |
| Date.prototype.toLocaleDateString([locales [, options]])     | 返回一个表示该日期对象日期部分的字符串，该字符串格式与系统设置的地区关联。<br />`new Date().toLocaleDateString('zh', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })` (2020年11月26日星期四)<br />**每个日期时间组件的默认值都是undefined**, 但是如果 `weekday`, `year`, `month`, `day`, `hour`, `minute`, `second` 属性都是 **`undefined`**, 那么 `year`, `month`, `day`, `hour`, `minute` 和 `second` 的值都被认为是 "**numeric**" |
| Date.prototype.toLocaleString([locales [, options]])         | 返回一个表示该日期对象的字符串，该字符串与系统设置的地区关联。覆盖了 Object.prototype.toLocaleString() 方法。<br />`new Date().toLocaleString('zh', { timeZone: 'UTC',weekday: "long", year: "numeric", month: "long", day: "numeric",hour:'numeric',minute: 'numeric', second: 'numeric' })` (2020年11月26日星期四 上午8:22:58)<br />`new Date().toLocaleString('zh',{hour12: false})` (2020/11/26 16:22:58)<br />**每个日期时间组件的默认值都是undefined**, 但是如果 `weekday`, `year`, `month`, `day`, `hour`, `minute`, `second` 属性都是 **`undefined`**, 那么 `year`, `month`, `day`, `hour`, `minute` 和 `second` 的值都被认为是 "**numeric**" |
| Date.prototype.toLocaleTimeString([locales [, options]])     | 返回一个表示该日期对象时间部分的字符串，该字符串格式与系统设置的地区关联。<br />**每个日期时间组件的默认值都是undefined**, 但是如果 `weekday`, `year`, `month`, `day`, `hour`, `minute`, `second` 属性都是 **`undefined`**, 那么 `year`, `month`, `day`, `hour`, `minute` 和 `second` 的值都被认为是 "**numeric**" |
| Date.prototype.toString()                                    | 返回一个表示该日期对象的字符串。覆盖了Object.prototype.toString() 方法。 |
| Date.prototype.toTimeString()                                | 以美式英语和人类易读的形式返回一个日期对象的时间部分的字符串。 |

##### UTC API

| API                                                          | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Date.prototype.getTimezoneOffset()                           | 返回当前时区的时区偏移。(相对于当前时区的时间差值，单位为分钟。) |
| Date.prototype.getUTCDate()                                  | 根据世界时返回特定日期对象一个月的第几天（1-31）.            |
| Date.prototype.getUTCDay()                                   | 根据世界时返回特定日期对象一个星期的第几天（0-6，0 代表星期日）. |
| Date.prototype.getUTCFullYear()                              | 根据世界时返回特定日期对象所在的年份（4位数）.               |
| Date.prototype.getUTCHours()                                 | 根据世界时返回特定日期对象当前的小时（0-23）.                |
| Date.prototype.getUTCMilliseconds()                          | 根据世界时返回特定日期对象的毫秒数（0-999）.                 |
| Date.prototype.getUTCMinutes()                               | 根据世界时返回特定日期对象的分钟数（0-59）.                  |
| Date.prototype.getUTCMonth()                                 | 根据世界时返回特定日期对象的月份（0-11）.                    |
| Date.prototype.getUTCSeconds()                               | 根据世界时返回特定日期对象的秒数（0-59）.                    |
| Date.prototype.setUTCDate(dayValue)                          | 根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。              |
| Date.prototype.setUTCFullYear(yearValue[, monthValue[, dayValue]]) | 根据世界时设置 Date 对象中的年份（四位数字）。               |
| Date.prototype.setUTCHours(hoursValue[, minutesValue[, secondsValue[, msValue]]]) | 根据世界时设置 Date 对象中的小时 (0 ~ 23)。                  |
| Date.prototype.setUTCMilliseconds(millisecondsValue)         | 根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。                 |
| Date.prototype.setUTCMinutes(minutesValue[, secondsValue[, msValue]]) | 根据世界时设置 Date 对象中的分钟 (0 ~ 59)。                  |
| Date.prototype.setUTCMonth(monthValue[, dayValue])           | 根据世界时设置 Date 对象中的月份 (0 ~ 11)。                  |
| Date.prototype.setUTCSeconds(secondsValue[, msValue])        | 根据世界时设置 Date 对象中的秒钟 (0 ~ 59)。                  |
| Date.prototype.toUTCString()                                 | 把一个日期对象转换为一个以UTC时区计时的字符串。              |

## 基本对象

### Object

#### Object 构造函数的方法

| API                                          | 说明                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| Object.assign(target, ...sources)            | 将所有可枚举属性的值从一个或多个源对象分配到目标对象。它将返回目标对象。<br />为了将属性定义（包括其可枚举性）复制到原型，应使用`Object.getOwnPropertyDescriptor()`和`Object.defineProperty()` 。<br />`String`类型和 `Symbol` 类型的属性都会被拷贝。 |
| Object.create(proto，[propertiesObject])     | 使用指定的原型对象和属性创建一个新对象。使用现有的对象来提供新创建的对象的\__proto__。 |
| Object.defineProperty(obj, prop, descriptor) | 会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象<br />`configurable`、 `enumerable`、 `value`、 `writable`、 `get`、 `set` |
| Object.defineProperties(obj, props)          | 给对象添加多个属性并分别指定它们的配置。<br />**`configurable`**, `true` 当且仅当该属性描述符的类型可以被改变并且该属性可以从对应对象中删除。默认为 `false` <br />**`enumerable`**, `true` 当且仅当在枚举相应对象上的属性时该属性显现。默认为 `false`<br />**`value`**, 与属性关联的值。可以是任何有效的JavaScript值（数字，对象，函数等）。默认为 `undefined`。<br />**`writable`**, `true` 当且仅当与该属性相关联的值可以用assignment operator改变时。默认为 `false`<br />**`get`**, 作为该属性的 getter 函数，如果没有 getter 则为undefined。函数返回值将被用作属性的值。默认为 `undefined`<br />**`set`**, 作为属性的 setter 函数，如果没有 setter 则为undefined。函数将仅接受参数赋值给该属性的新值。默认为 `undefined` |
| Object.entries(obj)                          | 返回给定对象自身可枚举属性的 [key, value] 数组。<br />方法返回一个给定对象自身可枚举属性的键值对数组，其排列与使用 **for...in** 循环遍历该对象时返回的顺序一致（区别在于 `for-in` 循环还会枚举原型链中的属性）。 |
| Object.freeze(obj)                           | 冻结对象：其他代码不能删除或更改任何属性。此外，冻结一个对象后该对象的原型也不能被修改。`freeze()` 返回和传入的参数相同的对象。 |
| Object.getOwnPropertyDescriptor(obj, prop)   | 返回指定对象上一个自有属性对应的属性描述符。（自有属性指的是直接赋予该对象的属性，不需要从原型链上进行查找的属性） |
| Object.getOwnPropertyNames(obj)              | 返回一个由指定对象的所有自身属性的属性名（包括不可枚举属性但不包括Symbol值作为名称的属性）组成的数组。 |
| Object.getOwnPropertySymbols(obj)            | 返回一个给定对象自身的所有 Symbol 属性的数组。<br />除非你在对象上赋值了 Symbol 否则只会返回一个空的数组。 |
| Object.getPrototypeOf(obj)                   | 返回指定对象的原型对象。如果没有继承属性，则返回 `null` 。   |
| Object.is(value1, value2)                    | 比较两个值是否相同。所有 NaN 值都相等（这与\==和\===不同）。 |
| Object.isExtensible(obj)                     | 判断对象是否可扩展。（是否可以在它上面添加新的属性）返回一个`Boolean`值。 |
| Object.isFrozen(obj)                         | 判断对象是否已经冻结。返回一个`Boolean`值。                  |
| Object.isSealed(obj)                         | 判断对象是否已经密封。返回一个`Boolean`值。密封对象是指那些不可 `扩展` 的，且所有自身属性都不可配置且因此不可删除（但不一定是不可写）的对象。 |
| Object.keys(obj)                             | 返回一个包含所有给定对象自身可枚举属性名称的数组。数组中属性名的排列顺序和正常循环遍历该对象时返回的顺序一致 。 |
| Object.preventExtensions(obj)                | 防止对象的任何扩展。让一个对象变的不可扩展，也就是永远不能再添加新的属性。一般来说，不可扩展对象的属性可能仍然可被**删除** |
| Object.seal(obj)                             | 封闭一个对象，阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要原来是可写的就可以改变。 |
| Object.setPrototypeOf(obj, prototype)        | 设置对象的原型（即内部 [[Prototype]] 属性）。                |
| Object.values(obj)                           | 返回给定对象自身可枚举值的数组。值的顺序与使用`for...in`循环的顺序相同 ( 区别在于 for-in 循环枚举原型链中的属性 )。 |

`Object.is()` 方法判断两个值是否为同一个值：

+ 都是 `undefined`
+ 都是 `null`
+ 都是 `true` 或 `false`
+ 都是相同长度的字符串且相同字符按相同顺序排列
+ 都是相同对象（意味着每个对象有同一个引用）
+ 都是数字且
  + 都是 `+0`
  + 都是 `-0`
  + 都是 `NaN`
  + 或都是非零而且非 `NaN` 且为同一个值

与`==` 运算**不同**。 `==` 运算符在判断相等前对两边的变量(如果它们不是同一类型) 进行强制转换 (这种行为的结果会将 `"" == false` 判断为 `true`)， 而 `Object.is`不会强制转换两边的值。

与`===` 运算也不相同。 `===` 运算符 (也包括 `==` 运算符) 将数字 `-0` 和 `+0` 视为相等，而将`Number.NaN` 与`NaN`视为不相等。

#### Object 实例 及 构造函数 属性

| 属性                           | 说明                                                 |
| ------------------------------ | ---------------------------------------------------- |
| `Object.prototype.constructor` | 特定的函数，用于创建一个对象的原型。                 |
| `Object.prototype.__proto__`   | 指向当对象被实例化的时候，用作原型的对象。**已废弃** |



#### Object 实例 及 构造函数 方法

| API                                         | 说明                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| Object.prototype.hasOwnProperty(prop)       | 返回一个布尔值 ，表示某个对象是否含有指定的属性，而且此属性非原型链继承的。 |
| prototypeObj.isPrototypeOf(object)          | 返回一个布尔值，表示指定的对象是否在本对象的原型链中。       |
| Object.prototype.propertyIsEnumerable(prop) | 判断指定属性是否可枚举，内部属性设置参见 ECMAScript [[Enumerable]] attribute 。 |
| Object.prototype.toString()                 | 返回对象的字符串表示。                                       |
| Object.prototype.valueOf()                  | 返回指定对象的原始值。<br />Math 和 Error 对象没有 valueOf 方法 |

### Function

每个 JavaScript 函数实际上都是一个 `Function` 对象。运行 `(function(){}).constructor === Function // true` 便可以得到这个结论。

#### 属性

| 属性            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| Function.caller | 获取调用函数的具体对象。<br />如果一个函数`f`是在全局作用域内被调用的,则`f.caller为``null`,相反,如果一个函数是在另外一个函数作用域内被调用的,则`f.caller指向调用它的那个函数.` |
| Function.length | 获取函数的接收参数个数。                                     |
| Function.name   | 获取函数的名称                                               |
#### 方法

| API                                                     | 说明                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| Function.prototype.apply(thisArg, [argsArray])          | 在一个对象的上下文中应用另一个对象的方法；参数能够以数组形式传入。 |
| Function.prototype.bind(thisArg[, arg1[, arg2[, ...]]]) | bind()方法会创建一个新函数,称为绑定函数.当调用这个绑定函数时,绑定函数会以创建它时传入 bind()方法的第一个参数作为 this,传入 bind()方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数. |
| Function.prototype.call(thisArg, arg1, arg2, ...)       | 在一个对象的上下文中应用另一个对象的方法；参数能够以列表形式传入。 |
| Function.prototype.toString()                           | 获取函数的实现源码的字符串。                                 |

### Boolean

如果省略或值`0`，`-0`，`null`，`false`，`NaN`，`undefined`，或空字符串（`""`），该对象具有的初始值`false`。所有其他值，包括任何对象，空数组（`[]`）或字符串`"false"`，都会创建一个初始值为`true`的对象。

| API                                                          | 说明                                        |
| ------------------------------------------------------------ | ------------------------------------------- |
| new Boolean(值)	本质上就是将值转为布尔型（强制转为布尔型） |                                             |
| Boolean(值)			（强制转为布尔型）                    |                                             |
| !!值				隐式转为布尔型                           |                                             |
| Boolean.prototype.toString()                                 | 根据对象的值返回字符串`"true"`或`"false"`。 |
| Boolean.prototype.valueOf()                                  | 返回Boolean对象的原始值。                   |

### Symobl

**symbol** 是一种基本数据类型 （primitive data type）。`Symbol()`函数会返回**symbol**类型的值，该类型具有静态属性和静态方法。它的静态属性会暴露几个内建的成员对象；它的静态方法会暴露全局的symbol注册，且类似于内建对象类，但作为构造函数来说它并不完整，因为它不支持语法：**"`new Symbol()`"**。

每个从`Symbol()`返回的symbol值都是唯一的。一个symbol值能**作为对象属性的标识符**；这是该数据类型**仅有的目的**。

Symbol 在 `for...in` 迭代中不可枚举。

Symbol() 函数每次都会返回新的一个 symbol。

#### 全局共享 Symbol

| API                | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| Symbol.for(key)    | 会根据给定的键 `key`，来从运行时的 symbol 注册表中找到对应的 symbol，如果找到了，则返回它，否则，新建一个与该键关联的 symbol，并放入全局 symbol 注册表中。 |
| Symbol.keyFor(sym) | 用来获取全局symbol 注册表中与某个 symbol 关联的键。          |

```javascript
var sym = Symbol("foo");

Symbol.for("foo"); // 创建一个 symbol 并放入 symbol 注册表中，键为 "foo"
									 // 从 symbol 注册表中读取键为"foo"的 symbol

Symbol.for("bar") === Symbol.for("bar"); // true，证明了上面说的
Symbol("bar") === Symbol("bar"); // false，Symbol() 函数每次都会返回新的一个 symbol

var sym = Symbol.for("mario");
sym.toString(); 
// "Symbol(mario)"，mario 既是该 symbol 在 symbol 注册表中的键名，又是该 symbol 自身的描述字符串

// 创建一个全局 Symbol 
var globalSym = Symbol.for("foo"); 
Symbol.keyFor(globalSym); // "foo"
```

## 错误对象

### Error

```javascript
new Error([message[, fileName[,lineNumber]]])
```

## 可索引的集合对象

### Array

#### Array 语法

```
[element0, element1, ..., elementN]
new Array(element0, element1[, ...[, elementN]])
new Array(arrayLength)
```

+ `elementN`

  `Array` 构造器会根据给定的元素创建一个 JavaScript 数组，但是当仅有一个参数且为数字时除外（详见下面的 `arrayLength` 参数）。注意，后面这种情况仅适用于用 `Array` 构造器创建数组，而不适用于用方括号创建的数组字面量。

+ `arrayLength`

  一个范围在 0 到 2^32^-1 之间的整数，此时将返回一个 `length` 的值等于 `arrayLength` 的数组对象（言外之意就是该数组此时并没有包含任何实际的元素，不能理所当然地认为它包含 `arrayLength` 个值为 `undefined` 的元素）。如果传入的参数不是有效值，则会抛出 `RangeError` 异常。

#### Array 属性

| 属性              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| Array.length      | `Array` 构造函数的 length 属性，其值为1（注意该属性为静态属性，不是数组实例的 length 属性）。 |
| `Array.prototype` | 通过数组的原型对象可以为所有数组对象添加属性。               |

#### Array 方法

| API                                               | 说明                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| Array.from(arrayLike[, mapFn[, thisArg]])         | 从类数组对象或者可迭代对象中创建一个新的，浅拷贝的数组实例。 |
| Array.isArray(obj)                                | 用来判断某个变量是否是一个数组对象。                         |
| Array.of(element0[, element1[, ...[, elementN]]]) | 根据一组参数来创建新的数组实例，支持任意的参数数量和类型。<br />**`Array.of()`** 和 **`Array`** 构造函数之间的区别在于处理整数参数：**`Array.of(7)`** 创建一个具有单个元素 **7** 的数组，而 **`Array(7)`** 创建一个长度为7的空数组（**注意：**这是指一个有7个空位(empty)的数组，而不是由7个`undefined`组成的数组）。 |

#### 实例方法

##### 修改器方法

下面的这些方法会改变调用它们的对象自身的值

| 方法                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Array.prototype.copyWithin(target[, start[, end]])           | 在数组内部，将一段元素序列拷贝到另一段元素序列上，覆盖原有的值。<br />并返回它，不会改变原数组的长度。 |
| Array.prototype.fill(value[, start[, end]])                  | 用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。 |
| Array.prototype.reverse()                                    | 颠倒数组中元素的排列顺序，即原先的第一个变为最后一个，原先的最后一个变为第一个。该方法会改变原数组。 |
| Array.prototype.sort([compareFunction])                      | 对数组元素进行排序，并返回当前数组。默认排序顺序是在将元素转换为字符串，然后比较它们的UTF-16代码单元值序列时构建的 |
| Array.prototype.splice(start[, deleteCount[, item1[, item2[, ...]]]]) | 方法通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容。此方法会改变原数组。 |
| Array.prototype.pop()                                        | 删除数组的最后一个元素，并返回这个元素。此方法更改数组的长度。 |
| Array.prototype.push(element1, ..., elementN)                | 在数组的末尾增加一个或多个元素，并返回数组的新长度。         |
| Array.prototype.shift()                                      | 删除数组的第一个元素，并返回这个元素。此方法更改数组的长度。 |
| Array.prototype.unshift(element1, ..., elementN)             | 方法将一个或多个元素添加到数组的**开头**，并返回该数组的**新长度(该**方法修改原有数组**)**。 |

##### 访问方法

下面的这些方法绝对不会改变调用它们的对象的值，只会返回一个新的数组或者返回一个其它的期望值。

| 方法                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Array.prototype.concat()<br />`var new_array = old_array.concat(value1[,value2[,...[,valueN]]])` | 返回一个由当前数组和其它若干个数组或者若干个非数组值组合而成的新数组。<br />`concat`方法不会改变`this`或任何作为参数提供的数组，而是返回一个浅拷贝，它包含与原始数组相结合的相同元素的副本。 原始数组的元素将复制到新数组中 |
| Array.prototype.includes(valueToFind[, fromIndex])           | 判断当前数组是否包含某指定的值，如果是返回 true，否则返回 false。 |
| Array.prototype.join([separator])                            | 将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。如果数组只有一个项目，那么将返回该项目而不使用分隔符。<br />指定一个字符串来分隔数组的每个元素。如果需要，将分隔符转换为字符串。如果缺省该值，数组元素用逗号（`,`）分隔。如果`separator`是空字符串(`""`)，则所有元素之间都没有任何字符。 |
| Array.prototype.slice([begin[, end]])                        | 返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的**浅拷贝**（包括 `begin`，不包括`end`）。原始数组不会被改变。 |
| Array.prototype.toString()                                   | 返回一个由所有数组元素组合而成的字符串。遮蔽了原型链上的 Object.prototype.toString() 方法。 |
| Array.prototype.toLocaleString([locales[,options]])          | 一个字符串表示数组中的元素。数组中的元素将使用各自的 `toLocaleString` 方法转成字符串，这些字符串将使用一个特定语言环境的字符串（例如一个逗号 ","）隔开。 |
| Array.prototype.indexOf(searchElement[, fromIndex])          | 返回数组中第一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1。 |
| Array.prototype.lastIndexOf(searchElement[, fromIndex])      | 返回数组中最后一个（从右边数第一个）与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1。从数组的后面向前查找，从 `fromIndex` 处开始。 |

##### 迭代方法

在下面的众多遍历方法中，有很多方法都需要指定一个回调函数作为参数。在每一个数组元素都分别执行完回调函数之前，数组的length属性会被缓存在某个地方，所以，如果你在回调函数中为当前数组添加了新的元素，那么那些新添加的元素是不会被遍历到的。此外，如果在回调函数中对当前数组进行了其它修改，比如改变某个元素的值或者删掉某个元素，那么随后的遍历操作可能会受到未预期的影响。总之，不要尝试在遍历过程中对原数组进行任何修改，虽然规范对这样的操作进行了详细的定义，但为了可读性和可维护性，请不要这样做。

| 方法                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Array.prototype.forEach(callback(currentValue [, index [, array]])[, thisArg]) | 为数组中的每个元素执行一次回调函数。那些已删除或者未初始化的项将被跳过 |
| Array.prototype.map(callback(currentValue [, index [, array]])[, thisArg]) | 返回一个由回调函数的返回值组成的新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。 |
| Array.prototype.every(callback(element[, index[, array]])[, thisArg]) | 如果数组中的每个元素都满足测试函数，则返回 true，否则返回 false。 |
| Array.prototype.some(callback(element[, index[, array]])[, thisArg]) | 如果数组中至少有一个元素满足测试函数，则返回 true，否则返回 false。 |
| Array.prototype.keys()                                       | 返回一个数组迭代器对象，该迭代器会包含所有数组元素的键。     |
| Array.prototype.values()                                     | 返回一个数组迭代器对象，该迭代器会包含所有数组元素的值。     |
| Array.prototype.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue]) | 从左到右为每个数组元素执行一次回调函数，并把上次回调函数的返回值放在一个暂存器中传给下次回调函数，并返回最后一次回调函数的返回值。<br />如果没有提供 `initialValue`，那么`accumulator`取数组中的第一个值，`currentValue`取数组中的第二个值。 |
| Array.prototype.reduceRight(callback(accumulator, currentValue[, index[, array]])[, initialValue]) | 从右到左为每个数组元素执行一次回调函数，并把上次回调函数的返回值放在一个暂存器中传给下次回调函数，并返回最后一次回调函数的返回值。<br />如果未提供该初始值，则将使用数组中的最后一个元素，并跳过该元素。如果不给出初始值，则需保证数组不为空。 |
| Array.prototype.filter(callback(element[, index[, array]])[, thisArg]) | 将所有在过滤函数中返回 true 的数组元素放进一个新数组中并返回。 |
| Array.prototype.find(callback(element[, index[, array]])[, thisArg])<br />Array.prototype.findIndex(callback(element[, index[, array]])[, thisArg]) | 找到第一个满足测试函数的元素并返回那个元素的值，如果找不到，则返回 undefined。<br />如果找不到，则返回 -1。 |

## 结构化数据

### JSON

| API         | 说明                                                     |
| ----------- | -------------------------------------------------------- |
| parse()     | 以文本字符串形式接受JSON对象作为参数，并返回相应的对象。 |
| stringify() | 接收一个对象作为参数，返回一个对应的JSON字符串。         |

#### parse

```
JSON.parse(text[, reviver])
```

##### 参数

+ `text`

  要被解析成 JavaScript 值的字符串。

+ `reviver` 可选

  转换器, 如果传入该参数(函数)，可以用来修改解析生成的原始值，调用时机在 parse 函数返回之前。

##### 返回值

Object 类型, 对应给定 JSON 文本的对象/值。

#### stringify

```
JSON.stringify(value[, replacer [, space]])
```

##### 参数

+ `value`

  将要序列化成 一个 JSON 字符串的值。

+ `replacer` 可选

  如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为 null 或者未提供，则对象所有的属性都会被序列化。

+ `space` 可选

  指定缩进用的空白字符串，用于美化输出（pretty-print）；如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格；如果该参数为字符串（当字符串长度超过10个字母，取其前10个字母），该字符串将被作为空格；如果该参数没有提供（或者为 null），将没有空格。

##### 返回值

  一个表示给定值的JSON字符串。

#### 问题

  `JSON.stringify()`将值转换为相应的JSON格式：

  + 转换值如果有 `toJSON()` 方法，该方法定义什么值将被序列化。
  + 非数组对象的属性不能保证以特定的顺序出现在序列化后的字符串中。
  + 布尔值、数字、字符串的包装对象在序列化过程中会自动转换成对应的原始值。
  + `undefined`、任意的函数以及 `symbol `值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 `null`（出现在数组中时）。函数、`undefined `被单独转换时，会返回 `undefined`，如`JSON.stringify(function(){})` or `JSON.stringify(undefined)`.
  + 对包含循环引用的对象（对象之间相互引用，形成无限循环）执行此方法，会抛出错误。
  + 所有以 `symbol `为属性键的属性都会被完全忽略掉，即便 `replacer` 参数中强制指定包含了它们。
  + `Date `日期调用了 `toJSON()` 将其转换为了 `string `字符串（同`Date.toISOString()`），因此会被当做字符串处理。
  + `BigInt`大整数调用了 `toJSON()` 将其转换为了 `string `字符串（`BigInt.prototype.toJSON = function() { return this.toString();}`），因此会被当做字符串处理。
  + `NaN `和 `Infinity `格式的数值及 `null` 都会被当做 `null`。
  + 其他类型的对象，包括 `Map`/`Set`/`WeakMap`/`WeakSet`，仅会序列化可枚举的属性。

## 使用键的集合对象

### Map

`Objects` 和 `Maps` 类似的是，它们都允许你按键存取一个值、删除键、检测一个键是否绑定了值。因此（并且也没有其他内建的替代方式了）过去我们一直都把对象当成 `Maps` 使用。不过 `Maps` 和 `Objects` 有一些重要的区别，在下列情况里使用 `Map` 会是更好的选择：

|          | Map                                                          | Object                                                       |
| :------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| 意外的键 | `Map` 默认情况不包含任何键。只包含显式插入的键。             | 一个 `Object` 有一个原型, 原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。<br />**注意:** 虽然 ES5 开始可以用 `Object.create(null)` 来创建一个没有原型的对象，但是这种用法不太常见。 |
| 键的类型 | 一个 `Map`的键可以是**任意值**，包括函数、对象或任意基本类型。 | 一个`Object` 的键必须是一个 `String` 或是 `Symbol`           |
| 键的顺序 | `Map` 中的 key 是有序的。因此，当迭代的时候，一个 `Map` 对象以插入的顺序返回键值。 | 一个 `Object` 的键是无序的<br />**注意：**自ECMAScript 2015规范以来，对象*确实*保留了字符串和Symbol键的创建顺序； 因此，在只有字符串键的对象上进行迭代将按插入顺序产生键。 |
| Size     | `Map` 的键值对个数可以轻易地通过`size` 属性获取              | `Object` 的键值对个数只能手动计算                            |
| 迭代     | `Map` 是 `iterable` 的，所以可以直接被迭代。                 | 迭代一个`Object`需要以某种方式获取它的键然后才能迭代。       |
| 性能     | 在**频繁增删键值对**的场景下表现更好。                       | 在频繁添加和删除键值对的场景下未作出优化。                   |

#### 属性

| 属性               | 说明                         |
| ------------------ | ---------------------------- |
| Map.prototype.size | 返回Map对象的键/值对的数量。 |

#### 方法

| API                                                          | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Map.prototype.clear()                                        | 移除Map对象的所有键/值对 。                                  |
| Map.prototype.delete(key)                                    | 如果 Map 对象中存在该元素，则移除它并返回 true；否则如果该元素不存在则返回 false。<br />随后调用 Map.prototype.has(key) 将返回 false 。 |
| Map.prototype.entries()                                      | 返回一个新的 Iterator 对象，它按插入顺序包含了Map对象中每个元素的 [key, value] 数组。 |
| Map.prototype.forEach(callback(\[value]\[,key]\[,map])[, thisArg]) | 按插入顺序，为 Map对象里的每一键值对调用一次callbackFn函数。如果为forEach提供了thisArg，它将在每次回调中作为this值。 |
| Map.prototype.get(key)                                       | 返回键对应的值，如果不存在，则返回undefined。                |
| Map.prototype.has(key)                                       | 返回一个布尔值，表示Map实例是否包含键对应的值。              |
| Map.prototype.set(key, value)                                | 设置Map对象中键的值。返回该Map对象。                         |
| Map.prototype.keys()                                         | 返回一个新的 Iterator对象， 它按插入顺序包含了Map对象中每个元素的键 。 |
| Map.prototype.values()                                       | 返回一个新的Iterator对象，它按插入顺序包含了Map对象中每个元素的值 。 |

```javascript
let kvArray = [["key1", "value1"], ["key2", "value2"]];

// 使用常规的Map构造函数可以将一个二维键值对数组转换成一个Map对象
let myMap = new Map(kvArray);

// 使用Array.from函数可以将一个Map对象转换成一个二维键值对数组
console.log(Array.from(myMap)); // 输出和kvArray相同的数组

// 更简洁的方法来做如上同样的事情，使用展开运算符
console.log([...myMap]);

// 或者在键或者值的迭代器上使用Array.from，进而得到只含有键或者值的数组
console.log(Array.from(myMap.keys())); // 输出 ["key1", "key2"]
```

### Set

**`Set`** 对象允许你存储任何类型的**唯一值**，无论是原始值或者是对象引用。

#### 属性

| 属性               | 说明                      |
| ------------------ | ------------------------- |
| Set.prototype.size | 返回 Set 对象中的值的个数 |

#### 方法

| API                                          | 说明                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| Set.prototype.add(value)                     | 在Set对象尾部添加一个元素。返回该Set对象。                   |
| Set.prototype.clear()                        | 移除Set对象内的所有元素。                                    |
| Set.prototype.delete(value)                  | 移除Set中与这个值相等的元素，返回Set.prototype.has(value)在这个操作前会返回的值（即如果该元素存在，返回true，否则返回false）。Set.prototype.has(value)在此后会返回false。 |
| Set.prototype.entries()                      | 返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值的[value, value]数组。为了使这个方法和Map对象保持相似， 每个值的键和值相等。 |
| Set.prototype.forEach(callbackFn[, thisArg]) | 按照插入顺序，为Set对象中的每一个值调用一次callBackFn。如果提供了thisArg参数，回调中的this会是这个参数。 |
| Set.prototype.has(value)                     | 返回一个布尔值，表示该值在Set中存在与否。                    |
| Set.prototype.keys()                         | 与values()方法相同，返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。 |
| Set.prototype.values()                       | 返回一个新的迭代器对象，该对象包含Set对象中的按插入顺序排列的所有元素的值。 |

### WeakMap

**`WeakMap`** 对象是一组键/值对的集合，其中的键是弱引用的。其键必须是对象，而值可以是任意的。

`WeakMap` 的 key 是不可枚举的 (没有方法能给出所有的 key)

**主要用于，要往对象上添加数据，又不想干扰垃圾回收机制**

#### 属性

| 属性           | 说明                    |
| -------------- | ----------------------- |
| WeakMap.length | `length` 属性的值为 0。 |

#### 方法

| API                               | 说明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| WeakMap.prototype.delete(key)     | 移除key的关联对象。执行后 WeakMap.prototype.has(key)返回false。 |
| WeakMap.prototype.get(key)        | 返回key关联对象, 或者 undefined(没有key关联对象时)。         |
| WeakMap.prototype.has(key)        | 根据是否有key关联对象返回一个Boolean值。                     |
| WeakMap.prototype.set(key, value) | 在WeakMap中设置一组key关联对象，返回这个 WeakMap对象         |

### WeakSet

**`WeakSet`** 对象允许你将*弱保持对象*存储在一个集合中。

和 `Set` 对象的区别有两点:

+ 与`Set`相比，`WeakSet` 只能是**对象的集合**，而不能是任何类型的任意值。
+ `WeakSet`持弱引用：集合中对象的引用为弱引用。 如果没有其他的对`WeakSet`中对象的引用，那么这些对象会被当成垃圾回收掉。 这也意味着WeakSet中没有存储当前对象的列表。 正因为这样，`WeakSet` 是不可枚举的。

#### 属性

| 属性           | 说明                    |
| -------------- | ----------------------- |
| WeakSet.length | `length` 属性的值为 0。 |

#### 方法

| API                             | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| WeakSet.prototype.add(value)    | 在该 WeakSet 对象中添加一个新元素 value.                     |
| WeakSet.prototype.delete(value) | 从该 WeakSet 对象中删除 value 这个元素, 之后 WeakSet.prototype.has(value) 方法便会返回 false. |
| WeakSet.prototype.has(value)    | 返回一个布尔值,  表示给定的值 value 是否存在于这个 WeakSet 中. |
## 控制抽象对象

### Promise

#### 静态方法

| API                          | 说明                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| Promise.all(iterable)        | 这个方法返回一个新的promise对象，该promise对象在iterable参数对象里所有的promise对象都成功的时候才会触发成功，一旦有任何一个iterable里面的promise对象失败则立即触发该promise对象的失败。这个新的promise对象在触发成功状态以后，会把一个包含iterable里所有promise返回值的数组作为成功回调的返回值，顺序跟iterable的顺序保持一致；如果这个新的promise对象触发了失败状态，它会把iterable里第一个触发失败的promise对象的错误信息作为它的失败错误信息。Promise.all方法常被用于处理多个promise对象的状态集合。（可以参考jQuery.when方法---译者注） |
| Promise.allSettled(iterable) | 等到所有promises都已敲定（settled）（每个promise都已兑现（fulfilled）或已拒绝（rejected））。 |
| Promise.any(iterable)        | 返回一个promise，该promise在所有promise完成后完成。并带有一个对象数组，每个对象对应每个promise的结果。 |
| Promise.race(iterable)       | 接收一个Promise对象的集合，当其中的一个 promise 成功，就返回那个成功的promise的值。 |
| Promise.reject(reason)       | 当iterable参数里的任意一个子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象。 |
| Promise.resolve(value)       | 返回一个状态为失败的Promise对象，并将给定的失败信息传递给对应的处理方法 |

#### 原型方法

| API                                             | 说明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| Promise.prototype.catch(onRejected)             | 添加一个拒绝(rejection) 回调到当前 promise, 返回一个新的promise。当这个回调函数被调用，新 promise 将以它的返回值来resolve，否则如果当前promise 进入fulfilled状态，则以当前promise的完成结果作为新promise的完成结果. |
| Promise.prototype.then(onFulfilled, onRejected) | 添加解决(fulfillment)和拒绝(rejection)回调到当前 promise, 返回一个新的 promise, 将以回调的返回值来resolve. |
| Promise.prototype.finally(onFinally)            | 添加一个事件处理回调于当前promise对象，并且在原promise对象解析完毕后，返回一个新的promise对象。回调会在当前promise运行完毕后被调用，无论当前promise的状态是完成(fulfilled)还是失败(rejected) |

```javascript
new Promise((resolve, reject) => {
  // ?做一些异步操作，最终会调用下面两者之一:
  //
  //   resolve(someValue); // fulfilled
  // ?或
  //   reject("failure reason"); // rejected
});
```

### AsyncFunction

`AsyncFunction` 构造函数用来创建新的 `异步函数` 对象，JavaScript 中每个异步函数都是 `AsyncFunction` 的对象。

注意，`AsyncFunction` 并不是一个全局对象，需要通过下面的方法来获取：

```js
Object.getPrototypeOf(async function(){}).constructor
```

```javascript
new AsyncFunction([arg1[, arg2[, ...argN]],] functionBody)
```

## 反射





## Gloabl / Window API

| API                     | 说明                                                         |
| ----------------------- | ------------------------------------------------------------ |
| setTimeout()            | 在指定的时间后执行一段代码                                   |
| setInterval()           | 以固定的时间间隔，重复运行一段代码                           |
| requestAnimationFrame() | setInterval()的现代版本;在浏览器下一次重新绘制显示之前执行指定的代码块，从而允许动画在适当的帧率下运行，而不管它在什么环境中运行 |
| clearInterval()         |                                                              |
| clearTimeout()          |                                                              |
| encodeURI()             | 对一个URI进行编码                                            |
| decodeURI               | 对一个URI进行解码                                            |
| eval                    | 执行字符串表达式                                             |
| parseInt                | 将数据转为整型                                               |
| parseFloat              | 将数据转为浮点型                                             |
| typeof                  | 判断一个数据类型                                             |
| isNaN                   | 检查一个值是否为NaN,如果是->true , 否->false                 |
| isFinite                | 检查一个值是否为有限值，是->true  否->false                  |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |
|                         |                                                              |



## Storage

### Storage API

作为 Web Storage API 的接口，**`Storage`** 提供了访问特定域名下的会话存储或本地存储的功能，例如，可以添加、修改或删除存储的数据项。

如果你想要操作一个域名的会话存储，可以使用 `Window.sessionStorage`；如果想要操作一个域名的本地存储，可以使用 `Window.localStorage`。

`sessionStorage` 属性允许你访问一个，对应当前源的 `sessionStorage` 对象。它与 `localStorage`相似，不同之处在于 `localStorage` 里面存储的数据没有过期时间设置，而存储在 `sessionStorage` 里面的数据在页面会话结束时会被清除。

+ 页面会话在浏览器打开期间一直保持，并且重新加载或恢复页面仍会保持原来的页面会话。
+ **在新标签或窗口打开一个页面时会复制顶级浏览会话的上下文作为新会话的上下文，**这点和 session cookies 的运行方式不同。
+ 打开多个相同的URL的Tabs页面，会创建各自的`sessionStorage`。
+ 关闭对应浏览器窗口（Window）/ tab，会清除对应的`sessionStorage`。 

| API                  | 说明                                                         |
| -------------------- | ------------------------------------------------------------ |
| Storage.key()        | 该方法接受一个数值 n 作为参数，并返回存储中的第 n 个键名。   |
| Storage.getItem()    | 该方法接受一个键名作为参数，返回键名对应的值。               |
| Storage.setItem()    | 该方法接受一个键名和值作为参数，将会把键值对添加到存储中，如果键名存在，则更新其对应的值。 |
| Storage.removeItem() | 该方法接受一个键名作为参数，并把该键名从存储中删除。         |
| Storage.clear()      | 调用该方法会清空存储中的所有键名。                           |

| 属性           | 说明                                                    | 状态 |
| -------------- | ------------------------------------------------------- | ---- |
| Storage.length | 返回一个整数，表示存储在 `Storage` 对象中的数据项数量。 | 只读 |

