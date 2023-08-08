# JSON 相关说明

推荐说明  [JSON](https://www.json.org/json-zh.html)

### JSON说明

+ JSON是一个轻量级的 **数据格式**
+ 是JavaScript语法的子集
+ 可表示对象、数组、字符串、数值、布尔值、null
+ 可以把JSON直接传给`eval()` (由于`eval()`的安全性问题，该方法一般禁止使用)
+ ECMAScript 5 定义了原生的JSON对象，`JSON.parse()`、`JSON.stringify()`

### 语法

JSON的语法可以表示三种类型的值

+ **简单值：**使用与JavaScript相同语法，可以在JSON中表示字符串、数值、布尔值、null。但JSON不支持JavaScript中的特殊值`undefined`
+ **对象：**对象作为一种复杂数据类型，表示的是一组无序的键值对。而每个键值对中的值可以是任意类型的简单值，也可以是复杂数据类型的值
+ **数组：**数组作为一种复杂数据类型，表示一组有序的值的列表，可以通过数值索引来访问其中的值。数组的值也可以是任意类型的简单值，也可以是复杂数据类型的值

JSON不支持变量、函数或对象实例，它就是一种表示结构化数据的格式。

#### 简单值

最简单的JSON数据形式就是简单值

JavaScript字符串与JSON字符串最大的区别在于，JSON字符串必须使用双引号

#### 对象

JSON中的对象要求给属性加双引号

JavaScript中如下：

```javascript
var object = {
  name: "Tom",
  age: 20
}
```

JSON中如下：

```json
{
  "name": "Tom",
  "age": 20
}
```

与JavaScript的不同：

1. 没有声明变量(JSON中没有变量的概念
2. 没有末尾的分号

JSON中**对象的属性必须加双引号**

```json
{
  "name": "Tom",
  "age": 20,
  "family": {
    "father": "Bob",
    "mother": "Anna"
  }
}
```

#### 数组

JSON数组采用的就是JavaScript中的数组字面量形式

在JSON中可以采用同一语法表示同一数组

同样要注意，JSON数组没有变量和分号

JavaScript表示如下：

```javascript
var arr = [20, "hi", true]
```

JSON表示如下

```json
[20, "hi", true]
```

把数组和对象结合起来，可以构成更复杂的数据集合

### 解析与序列化

JSON的优势

+ 拥有与JavaScript类似的语法
+ 可以把JSON数据结构解析为有用的JavaScript对象
+ 与XML数据结构相比，更简单

(XML数据结构要解析成DOM文档从而从中提取数据)

以要获取第三本书的书名为例：

> JSON方式
>
> ```javascript
> books[2].title
> ```
>
> XML方式
>
> ```javascript
> doc.getElementsByTagName("books")[2].getAttribute("title")
> ```

### JSON对象

默认情况下，`JSON.stringify()`输出的JSON字符串不包含任何空字符或缩进

在序列化JavaScript对象时，所有函数及原型成员都会被有意忽略掉，不体现在结果中

此外，值为undefined的任何属性也都会被跳过

结果中最终都是值为有效JSON数据类型的实例属性

将JSON字符串直接传给`JSON.parse()`就可以得到相应的JavaScript值

如果传给`JSON.parse()`的字符串不是有效的JSON，该方法会抛出错误

#### 序列化选项

`JSON.stringify()`共接收3个参数

+ 要序列化的JavaScript对象
+ 过滤器，可以是数组，也可以是一个函数
+ 选项，表示十分在JSON字符串中保留缩进

##### 过滤结果

```javascript
var user = {
  "name": "Tom",
  "age": 20,
  "sex": "man",
  "birthday": "2000-1-1"
}
var jsonText = JSON.stringify(user, ["name", "age"]) // "{"name":"Tom","age":20}"
```

+ 当为数组时，数组中的属性要与要序列化的对象中的属性相对应，在返回结果中，只会包含该属性的值；
+ 当为函数时，传入的函数接收两个参数，属性(键)名和属性值。根据属性(键)名可以知道应该如何处理要序列化的对象中的属性。属性名只能是字符串而在值并非键值对结构的值时，键名可以是空字符串。

为了改变序列化对象的结果，函数返回的值就是相应键的值。若函数返回了undefined，那么相应的属性会被忽略。

```javascript
var user = {
  "name": "Tom",
  "age": 20,
  "sex": "man",
  "birthday": "2000-1-1"
}
var jsonText = JSON.stringify(user, function(key, value) {
	switch(key) {
    case "sex":
      return undefined;
    case "birthday":
      return 5000;
    default:
      return value
  }
})
```

##### 字符串缩进

如果参数是一个数值，他表示的是每个级别缩进的空格数。最大缩进空格数为10，大于10的值都会自动转换为10。

只要传入有效的控制缩进的参数，结果字符串就会包含换行符。

```javascript
var user = {
  "name": "Tom",
  "age": 20,
  "sex": "man",
  "birthday": "2000-1-1"
}
var jsonText = JSON.stringify(user, null, 4)
// "{
//     "name": "Tom",
//     "age": 20,
//     "sex": "man",
//     "birthday": "2000-1-1"
// }"
```

如果所及参数是一个字符串而非数值，则中国字符串在JSON字符串中被用作缩进字符

```javascript
var user = {
  "name": "Tom",
  "age": 20,
  "sex": "man",
  "birthday": "2000-1-1"
}
var jsonText = JSON.stringify(user, null, "-")
// "{
// -"name": "Tom",
// -"age": 20,
// -"sex": "man",
// -"birthday": "2000-1-1"
// }"
```

#### toJSON()方法

可以给对象定义返回的对象

可作为函数过滤器的补充

**序列化对象顺序**

1. 若果存在toJSON()方法而且能通过该对象取得有效的值，则调用该方法。否则，返回对象本身；
2. 如果提供了第二个参数，应用这个函数过滤器。传入函数过滤器的值是第(1)步返回的值；
3. 对第(2)步返回的每个值进行相应的序列化；
4. 如果提供了第三个参数，执行相应的格式化。

```javascript
let json = {
  string: 'string',
  number: 123456,
  boolean: true,
  undefined: undefined,
  null: null,
  date: new Date(),
  symbol: Symbol('s'),
  object: { name: 'Tom' },
  array: [1],
  function: function () {},
  toJSON: function () {
    console.log(this)
    this.string = undefined // 删除 string 字段
    return this
  }
}
console.log('json', json)
let string = JSON.stringify(json)
console.log('string', string) // string {"number":123456,"boolean":true,"null":null,"date":"2020-11-16T08:15:22.100Z","object":{"name":"Tom"},"array":[1]}
let deep = JSON.parse(string)
console.log('deep', deep)
// {
//   array: [1]
//   boolean: true
//   date: "2020-11-16T08:15:22.100Z"
//   null: null
// 	number: 123456
// 	object: {name: "Tom"}
// }
```

#### 解析选项

`JSON.parse()`接收2个参数

+ 要解析的字符串
+ 还原函数(为了区别`JSON.stringify()`的过滤函数，本质功能相同)

如果还原函数返回undefined，则表示从结果中删除相应的键；如果返回其他值，则将该值插入到结果中。

```javascript
var user = {
  "name": "Tom",
  "age": 20,
  "sex": "man",
  "birthday": new Date(2000, 0, 1)
}
var jsonText = JSON.stringify(user);
var json = JSON.parse(jsonText, function(key, value) {
  if (key === "birthday") {
    return new Date(value);
  } else {
    return value;
  }
});
// {
//   age: 20
//   birthday: Sat Jan 01 2000 00:00:00 GMT+0800 (中国标准时间) {}
//   name: "Tom"
//   sex: "man"
// }
```



### JSON 深拷贝的缺点

+ 若有Date，则返回字符串形式而不是对象形式；
+ 若有RegExp、Error对象，则返回空对象；
+ 若有function、undefined，则会被丢弃；
+ 若有NaN、Infinity、-Infinity，则返回null；
+ 若为构造函数，使用原型继承的将会丢失；
+ 若存在循环引用，则无法实现深拷贝