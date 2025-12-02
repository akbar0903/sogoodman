---
title: 深入学习JavaScript
date: 2025-12-02 20:05:35
tags: ['JavaScript']
categories: JavaScript
cover: https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202200832048.png
---

# JavaScript 历史

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202201043998.png)

> 我们现在说的 es6 就是2015年发布的版本。

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202201143499.png)

# 数据类型

## 原始类型

### Number：整数，小数

 ```js
 let age = 23
 ```

### String：字符串

```js
let name = 'akbar'

let name = "akbar"
```
{% note primary modern %}
字符串虽然是原始类型，但当我们调用其方法时，JavaScript 引擎会通过“原始值包装”机制，自动将其临时转换为 String 对象来执行操作，完成后再转换回原始值，因此它拥有了对象的方法调用能力。
{% endnote %}

1. **通过索引获取字符：**

```js
const plane = 'A320';
console.log(plane[0]); 

// 字符串字面量也可以直接使用索引
console.log('A320'[0]); 

// 或者使用 at() 方法
console.log(plane.at(0));  // 'A'
console.log(plane.at(-1)); // '0'（最后一个字符）
```

2. **string.lenght：获取字符串长度**

3. **string.indexOF()：获取字符的下表**

4. **string.lastIndexOf()：该字符最后一次出现的索引**

5. **string.slice()：方法提取字符串的一部分，并将其作为新字符串返回，而不修改原始字符串**

```js
const str = "The quick brown fox jumps over the lazy dog.";

console.log(str.slice(31));
// Expected output: "the lazy dog."

console.log(str.slice(4, 19));
// Expected output: "quick brown fox"
```

6. **string.toLowerCase()：转换成小写**

7. **string.toUpperCase()：转换成大学**

8. **string.trim()：从字符串的两端移除空白字符，并返回一个新的字符串，而不会修改原始字符串。**

9. **string.replace()：替换指定的字符。**

10. **string.replaceAll()：其中匹配的都被替换掉**

```js
const paragraph = "I think Ruth's dog is cuter than your dog!";

console.log(paragraph.replaceAll("dog", "monkey"));
```

11. **string.includes()：判断字符串是否包好这个字符串。**

12. **string.starsWith()：判断是否以什么什么开头**

13. **string.endsWith()：判断是否以什么什么结尾。**

14. **string.split()：接受一个模式，通过搜索模式将字符串分割成一个有序的子串列表，将这些子串放入一个数组，并返回该数组。**

15. **string.padStart()：用另一个字符串填充当前字符串（如果需要会重复填充），直到达到给定的长度。填充是从当前字符串的开头开始的。**

16. **string.repeat()：构造并返回一个新字符串，其中包含指定数量的所调用的字符串副本，这些副本连接在一起。**

```js
const mood = "Happy! ";

console.log(`I feel ${mood.repeat(3)}`);
// Expected output: "I feel Happy! Happy! Happy! "
```

### Boolean：布尔类型

```js
let result = true
```

### Undefined

{% note primary modern %}
变量声明了，但没有赋值时，它的值就是 undefined

可以这样理解：
我知道这个变量存在，但我不知道它里面是什么。
{% endnote %}

```js
let age
```

### Null

{% note primary modern %}
变量被刻意设为空（清空）
{% endnote %}

```js
let b = null; 
```

跟Undefined比较：

值           | 由谁决定        | 含义           |
| ----------- | ----------- | ------------ |
| `undefined` | JS 自动赋值 | 变量存在，但还没有内容  |
| `null`      | 程序员主动赋值| 变量被刻意设为空（清空）

> **注意**：<br/>
> ```js
> console.log(typeof null)
> ```
> 上面的代码会输出`object`，但是按道理应该输出`null`，所以这是JavaScript的一个bug。

## NaN

{% note primary modern %}
`NaN` 是一个特殊的数值，表示“不是一个合法的数字（Not-a-Number）”，但它本身却属于 `number` 类型。
{% endnote %}

```js
typeof NaN  // "number"
```
它表示一个数学计算失败后产生的数值。

比如：
```js
Number("hello")  // NaN
0 / 0            // NaN
Math.sqrt(-1)    // NaN
```

`NaN` 不等于任何东西，包括它自己

```js
NaN === NaN  // false
```

{% note primary modern %}
为什么？  
因为 `NaN` 表示“不确定的数字结果”，所以它不能和任何值相等。
{% endnote %}

判断 NaN 必须用 `Number.isNaN()`

```js
Number.isNaN(x)
```

## 引用数据类型

### 数组Array

**创建数组的两种方式：**
```js
// 第一种创建数组的方式
const friends = ['Michael', 'Steven', 'Peter']

// 第二种创建数组的方式
const friends = new Array('Michael', 'Steven', 'Peter')
```

**获取数组元素的技巧：**

```js
const friends = ['Michael', 'Steven', 'Peter']

// 通过下标获取
const item = friends[2]

// 通过表达式计算获取，注意，只能写表达式（返回一个值），不能写声明语句
const item = friends[friends.length - 1]

// 或者像字符串一样，可以使用at方法
```

**修改数组元素的值：**

```js
const friends = ['Michael', 'Steven', 'Peter']

friends[2] = 'Akbar'
```
{% note primary modern %}
我们是用`const`关键字定义的这个数组，我们可以修改它的元素吗？
答案是，可以的，因为数组不是原始类型，所以我们可以修改它的元素。但是修改整个数组是不行的
{% endnote %}

比如：
```js
const friends = ['Michael', 'Steven', 'Peter']

// 报错，const声明的变量不能被重新赋值
friends = ['Bob', 'Alice'] 
```

**数组常用的属性和方法：**

1. `length`：获取数组长度，注意这是属性，不是方法。

```js
const friends = ['Michael', 'Steven', 'Peter']
const length = friends.length
```

2. `push()`：在数组的末尾添加元素，返回新数组的长度

```js
const friends = ['Michael', 'Steven', 'Peter']

// 在数组的末尾添加元素，返回新数组的长度
const newLength = friends.unshift('John')
```

3. `unshift()`：在数组的开头添加元素，返回新数组的长度

```js
// 在数组的开头添加元素，返回新数组的长度
const newLength = friends.unshift('John')
```

4. `pop()`：删除数组末尾的元素， 并返回删除的元素

```js
// 删除数组末尾的元素， 并返回删除的元素
friends.pop()
```

5. `shift()`：删除数组开头的元素， 并返回删除的元素

```js
// 删除数组开头的元素， 并返回删除的元素
const first = friends.shift()
```

6. `indexOf()`：返回元素在数组中的索引位置， 如果不存在则返回 -1

```js
// 返回元素在数组中的索引位置， 如果不存在则返回 -1
console.log(friends.indexOf('Steven'))
console.log(friends.indexOf('Bob'))
```

7. `includes()`：判断数组中是否包含某个元素， 返回布尔值。`严格比较`

```js
// 判断数组中是否包含某个元素， 返回布尔值。注意，这个方法使用的是严格比较
console.log(friends.includes('Steven'))
console.log(friends.includes('Bob'))
```

8. `concat()`：合并两个数组，然后返回一个新数组

MDN链接：https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat

```js
const array1 = ["a", "b", "c"];
const array2 = ["d", "e", "f"];
const array3 = array1.concat(array2);

console.log(array3);
// Expected output: Array ["a", "b", "c", "d", "e", "f"]
```

9. `join()`：将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串，用逗号或指定的分隔符字符串分隔。如果数组只有一个元素，那么将返回该元素而不使用分隔符。

10.  `slice()`：返回一个新的数组对象，这一对象是一个由 `start` 和 `end` 决定的原数组的浅拷贝（包括 `start`，不包括 `end`）

11.  `splice()`：就地移除或者替换已存在的元素和/或添加新的元素。

12.  `reverse()`：就地反转数组中的元素，并返回同一数组的引用。数组的第一个元素会变成最后一个，数组的最后一个元素变成第一个。换句话说，数组中的元素顺序将被翻转，变为与之前相反的方向。

13.  `at()`：接收一个整数值并返回该索引对应的元素，允许正数和负数。负整数从数组中的最后一个元素开始倒数。

```js
const arr = [23, 11, 64];
console.log(arr.at(-1)); // 最后一个元素
console.log(arr.at(0));  // 第一个元素
```

### 对象Object

{% note primary modern %}
注意，object中的`{}`只是定义对象时候要用的括号而已，不是`Block`，不会创建自己的作用域。
{% endnote %}

```js
const akbar = {
  name: 'Akbar',
  age: 2025 - 2001,
  isMarried: false,
  hobbies: ['reading', 'traveling', 'swimming'],
}

// 通过点（.）来访问属性
console.log(akbar.name)

// 通过下表来访问，括号里面可以写表达式
console.log(akbar['age'])
```

**添加元素：**

```js
const akbar = {
  name: 'Akbar',
  age: 32,
  isMarried: false,
  hobbies: ['reading', 'traveling', 'swimming'],
}

// 添加元素
akbar.job = 'No job'
akbar['location'] = 'China'

console.log(akbar)
```

**添加方法属性：**
```js
const akbar = {
  name: 'akbar',
  job: 'noJob',
  birthYear: 2001,

  // 这里要写函数表达式（会产生值），不能写函数声明
  calcAge: function(birthYear) {
    return 2025 - birthYear
  }
}

console.log(akbar.calcAge(2001))
console.log(akbar['calcAge'](2004))
```

**使用`this`关键字：**
```js
const akbar = {
  name: 'akbar',
  job: 'noJob',
  birthYear: 2001,

  calcAge: function () {
    // 谁调用这个方法，this就指向它
    return 2025 - this.birthYear
  },
}

console.log(akbar.calcAge())
console.log(akbar['calcAge']())
```
> 这里 this 指向的是当前方法的调用者。

**对象增强写法**

1. **属性名相同，可以只写一个：**

```js
const family = {
  item1: 'akbar',
  item2: 'sipul',
};

const akbar = {
  name: 'akbar',
  age: 24,
  // family: family,
  family
};

console.log(akbar);
```

2. **省略function关键字**

```js
const family = {
  item1: 'akbar',
  item2: 'sipul',
};

const akbar = {
  name: 'akbar',
  age: 24,
  family,
  // 不用这样写：
  // printAge: function() {}
  printAge() {
    console.log(this.age);
  },
};

console.log(akbar);
akbar.printAge()
```

### Sets

`Set` 对象是值的合集（collection）。集合（set）中的元素**只会出现一次**，即集合中的元素是唯一的。

```js
const orderSet = new Set([
  'Pasta',
  'Pizza',
  'Pizza',
  'Risotto',
  'Pasta',
  'Pizza',
]);

console.log(orderSet)
```

但是输出是：
```txt
Set(3) {'Pasta', 'Pizza', 'Risotto'}
```

**常用的方法：**

1. set.size：set的长度

```js
const orderSet = new Set([
  'Pasta',
  'Pizza',
  'Pizza',
  'Risotto',
  'Pasta',
  'Pizza',
]);

console.log(orderSet.size);    // 输出 3
```

2. set.has()：判断某个元素是否在set里面，很像array的include方法

```js
const orderSet = new Set([
  'Pasta',
  'Pizza',
  'Pizza',
  'Risotto',
  'Pasta',
  'Pizza',
]);

console.log(orderSet.has('Pasta'));   // 输出 true
```
3. set.add()：添加元素

```js
const orderSet = new Set([
  'Pasta',
  'Pizza',
  'Pizza',
  'Risotto',
  'Pasta',
  'Pizza',
]);

orderSet.add('Lamian')
console.log(orderSet)
```

4. set.delete()：删除元素

5. set.clear()：删除set中的所有元素

**遍历set：**
```js
const orderSet = new Set([
  'Pasta',
  'Pizza',
  'Pizza',
  'Risotto',
  'Pasta',
  'Pizza',
]);

for (const item of orderSet) console.log(item);
```

**set的使用场景：**

1. 从数组中删除重复的元素。

```js
const meals = ['Pasta', 'Pizza', 'Pizza', 'Risotto', 'Pasta', 'Pizza'];

const newMeals = [...new Set(meals)];

console.log(newMeals);
```

### Maps

`Map` 对象是键值对的集合。`Map` 中的一个键**只能出现一次**；它在 `Map` 的集合中是独一无二的。任何类型的数据都可以作为键（key）。

但是object不一样，object的key只能是字符串。

```js
const rest = new Map();
rest.set('name', 'Classico Italiano');
rest.set(1, 'Firenze, Italy');
console.log(rest);
```
set方法返回插入元素之后的map，所以我们可以链式调用：

```js
const rest = new Map();
rest
   .set('name', 'Classico Italiano')
   .set(1, 'Firenze, Italy');
console.log(rest);
```

1. map.get()：根据key获取其值

2. map.has()：根据key判断其对应的值是否已经存在。

3. map.delete()：根据key删除

4. map.size：map的长度

5. map.clear()：清空map

## 数据结构使用建议

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202210147042.png)

# 声明变量的关键字

## var

js 旧语法

## let

es6 新语法

## const

es6 新语法。

声明后的变量不能被更改：
```js
const birthYear = 1991
birthYear = 1990

// 会报这样的错误
Uncaught TypeError: Assignment to constant variable.
```

定义的变量一定要初始化:
```js
const job

// 报这样的错误
Uncaught SyntaxError: Missing initializer in const declaration
```

## 最佳实践

默认就使用`const`关键字声明变量，百分百能确定这个变量以后要改，这时候再考虑使用`let`关键字。

## var 和 let 的区别

 1. **作用域范围不同**

 var - 函数作用域
 ```js
 function printAge() {
  if (birthYear >= 2001 && birthYear <= 2025) {
    var millenial = true; // var 的作用域是整个函数
    // ...
  }
  console.log(millenial); // ✅ 可以访问，输出: true
}
 ```
 我来通过这段代码详细讲解 `var`和 `let`的区别：

## 1. 作用域范围不同

### var - 函数作用域

```js
function printAge() {
  if (birthYear >= 2001 && birthYear <= 2025) {
    var millenial = true; // var 的作用域是整个函数
    // ...
  }
  console.log(millenial); // ✅ 可以访问，输出: true
}
```

`var`在函数内部任何地方声明，在整个函数内都可访问。

let - 块级作用域

```js
function printAge() {
  if (birthYear >= 2001 && birthYear <= 2025) {
    let str = `Oh, and you're a millenial, ${firstName}`; // let 的作用域是当前代码块
    // ...
  }
  console.log(str); // ❌ ReferenceError: str is not defined
}
```
`let`只在声明它的代码块（`{}`内部）内有效。

2. **变量提升的差异**

var - 会提升并初始化为 undefined
```js
function example() {
  console.log(x); // undefined (不会报错)
  var x = 5;
}
```
let - 会提升但不会初始化
```js
function example() {
  console.log(x); // ❌ ReferenceError: Cannot access 'x' before initialization
  let x = 5;
}
```

3. **重复声明**

var - 允许重复声明

```js
var x = 1;
var x = 2; // ✅ 不会报错
```

let - 不允许重复声明

```js
let y = 1;
let y = 2; // ❌ SyntaxError: Identifier 'y' has already been declared
```

4. **全局作用域的行为差异**

var - 会成为全局对象的属性
```js
var globalVar = 'hello';
console.log(window.globalVar); // 在浏览器中输出: 'hello'
```

let - 不会成为全局对象的属性
```js
let globalLet = 'hello';
console.log(window.globalLet); // undefined
```


# 操作符

## 幂次

```js
const myNumber = 2 ** 3;    // 2的3次方
```

## `++ 和 --`

`++x`是先自身加1再参与运算，`x++`是先参与运算再自身加1。

# 类型转换

## 手动转换
```js
// 转换成数字类型
console.log(Number('123'))

// 转换成字符串类型
console.log(String(23))
```

> 注意：
> 可以转换成Number，String，Boolean，但是不能转换成undefined，null。

## 隐式转换

```js
// 这里的23自动转换成字符串23
console.log('I am' + 23 + 'years old')

// 输出10，说明字符串23，10自动变换成了数字类型
console.log('23' - '10' - 3)

// 输出24
console.log('22' * '2')

// 输出11
console.log('22' / '2')

// 猜猜这个会输出什么?
let n = '1' + 1
n = n - 1
console.log(n)
```

## Truthy 和 Falsy

5个falsy value：

1. 0
2. 空字符串：`""`
3. undefined
4. null
5. NaN

**这个一定要记得，非常重要。**

# `==` 和 `===`

**`===`（严格相等）**

**不做类型转换，类型不同直接 false。**

```js
1 === "1"   // false
true === 1  // false
null === undefined // false
```

**`==`（宽松相等）**

**会先进行类型转换（Type Coercion），再比较。**

也就是说，它会“强行把两边转换成同一种类型”，然后再比。

```js
1 == "1"   // true（字符串变成数字）
true == 1  // true（true 变成 1）
null == undefined // true（JS 规定的特殊规则）
```

**最佳实践**

用`===`，不用`===`。直接把`==`当成不存在就好了。 

# `!=` 和 `!===`

这个也是跟上面的严格相等和宽松相等很相似。

**最佳实践**：

使用`!===`，不要使用`！=`

# switch 语句

示例代码：
```js
const day = 'monday'

switch (day) {
  case 'monday':
    console.log('Plan course structure')
    console.log('Go to coding meetup')
    break
  case 'tuesday':
    console.log('Prepare theory videos')
    break
  case 'wednesday':
  case 'thursday':
    console.log('Write code examples')
    break
  case 'friday':
    console.log('Record videos')
    break
  case 'saturday':
  case 'sunday':
    console.log('Enjoy the weekend')
    break
  default:
    console.log('Not a valid day!')
}
```

`case 'monday'`这里是`严格相等`。

**什么样的场景更适合使用switch case**:

当要根据同一个变量的不同`“明确值”`来执行不同逻辑时，这是最标准的场景。

比如：
```js
switch (state) {
  case 'success':
    console.log('Operation was successful!')
    break
  case 'error':
    console.log('There was an error during the operation.')
    break
  default:
    console.log('Unknown status.')
}
```

上面的代码如果使用 if else，很长，很乱。

# `表达式` 和 `声明`

**表达式(expression)**:

会产生的值得语句：

```js
3 + 4                    // 产生值7
1991                     // 产生值1991
tru && false && !false   // 产生值false
```

三目运算符也是`表达式`，因为他会返回一个值：
```js
const drink = age >= 18 ? 'wine🍷' : 'water💧'
```

又比如：
```js
console.log(`I like to drink ${age >= 18 ? 'wine🍷' : 'water💧'}`)
```

**声明语句(statement)**:

会被执行，但是不会产生任何值：

比如：

```js
if(23 > 10) {
    console.log('hello world')
}
```
上面的代码被执行，但是不会产生值，比如这里的if语句块产生或者返回一个值了吗？


**注意事项**：

模板字符串中不能写`声明语句`:

```js
// 错误的写法
console.log(`I am ${if (23 > 10) 'older' else 'younger'} than 10`)
```

# strict mode

严格模式通过下面的字符串来开启，只要把这个字符串写道JavaScript文件的最上面就可以了：
```js
'use strict'
```
> **严格模式让 JavaScript 更安全、更规范、更容易发现错误。**  
它禁止一些“危险行为”，让你写出的代码更可靠。

# 函数

> 其实函数也是一种object,所以函数也有自己的方法,比如`call()`、`bind()`、`apply()`等方法

## 普通函数

```js
// 普通函数
function logger() {
  console.log('My name is Jonas')
}

// 调用
logger()
```

> 虽然这个函数没有返回值，但是它返回一个undefined。

## 函数表达式和函数声明

**函数声明**：

```js
// 普通函数
function sayHello() {
  return 'helllo world'
}

// 调用
const message = sayHello()
```

**函数表达式（也叫匿名函数）**：

```js
// 匿名函数
const sayHello = function () {
  return 'helllo world'
}

// 调用
const message = sayHello()
```

为什么叫`函数表达式`呢?
因为表达式会产生一个值，我们需要用一个变量来存储这个值，比如
```js
function () {
  return 'helllo world'
}
```
然后我们需要用变量`sayHello`来存储这个函数：

```js
const sayHello = function () {
  return 'helllo world'
}
```
> 所以我们可以认为`function`也是一种变量。

## 函数声明可以在定义之前调用

比如：

```js
// 调用
logger()

// 普通函数（函数声明）
function logger() {
  console.log('My name is Jonas')
}
```

但是函数表达式`匿名函数`则不能。

## 箭头函数

箭头函数其实就是`函数表达式`:
```js
const logger = () => {
    console.log('My name is Jonas')
}

logger()
```

> **注意**<br/>
> 箭头函数没有`this`。

## 立即执行函数


## 函数调用其它函数

```js
function cutFruitPieces(fruit) {
  return fruit * 4
}

function fruitProcessor(apples, oranges) {
  const applesPieces = cutFruitPieces(apples)
  const orangesPieces = cutFruitPieces(oranges)

  const juice = `Juice with ${applesPieces} apples and ${orangesPieces} oranges.}`
  return juice
}

console.log(fruitProcessor(2, 3))
```

## 函数返回函数

函数返回函数：
```js
const greet = function (greeting) {
  return function (name) {
    console.log(`${greeting} ${name}`);
  };
};

// 调用
const greeter = greet('Hello');
greeter('Akbar');

// 简化调用
greet('Hi')('Akbar');
```

用箭头函数实现：
```js
const greet = greeting => name => console.log(`${greeting} ${name}`);

const greeter = greet('Hello');
greeter('akbar');

greet('Hi')('Akbar');
```

## 函数参数设置默认值

比如(ES6)：
```js
const bookings = [];

const createBooking = function (flightNum, numPassengers = 1, price = 199) {
  const booking = {
    flightNum,
    numPassengers,
    price,
  };

  console.log(booking);
  bookings.push(booking);
};

createBooking('LH123');
```

如果不适用es6，应该这样写：
```js
const bookings = [];

const createBooking = function (flightNum, numPassengers, price) {
  // 通过短路运算设置默认值
  numPassengers ||= 1;
  price ||= 199;

  const booking = {
    flightNum,
    numPassengers,
    price,
  };

  console.log(booking);
  bookings.push(booking);
};

createBooking('LH123');
```


# 循环

## for循环

```js
for (let i = 0; i <= 100; i++) {
  console.log(`hello world ${i}`)
}
```

**遍历数组：**
```js
// 遍历数组
const myArray = ['akbar', 'saipulla', 'rexida', 'abliz']

for (let i = 0; i < myArray.length; i++) {
  console.log(myArray[i])
}
```

**continue 和 break：**

-  `continue`： 跳过当前这轮循环，进入下一轮循环

```js
// continue
const myArray = ['akbar', 'age', 'major', 2025 - 2001, 'location', 'hobbies']

console.log('-----ONLY STRINGS----')
for (let i = 0; i < myArray.length; i++) {
  if(typeof myArray[i] !== 'string') continue  // 跳过当前这轮循环，进入下一轮循环

  console.log(myArray[i])
}

// 所以不会输出类型是数字的元素
```

- `break`：直接结束循环

```js
const myArray = ['akbar', 'age', 'major', 2025 - 2001, 'location', 'hobbies']

console.log('-----BREAK WITH NUMBER----')
for (let i = 0; i < myArray.length; i++) {
  if(typeof myArray[i] !== 'string') break  // 遇到类型不是string的时候，直接结束循环

  console.log(myArray[i])
}
```

## while 循环

> 在我们不知道到底进行多少轮循环的时候，while循环是一个不错的选择

```js
let dice = Math.trunc(Math.random() * 6) + 1

while (dice !== 6) {
  console.log(`You rolled a ${dice}`)
  // 每次循环改变dice
  dice = Math.trunc(Math.random() * 6) + 1
  if(dice === 6) console.log('Loop is about to end ...')
}
```

## for-of循环

```js
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];

// 只能拿到item，拿不到索引
for (const item of arr) console.log(item);

// 可以拿到索引
for (const item of arr.entries()) console.log(item);
```

第二种是这种方式输出：
```txt
[0, 1]
[1, 2]
[2, 3]
[3, 4]
[4, 5]
[5, 6]
[6, 7]
[7, 8]
[8, 9]
```

所以更优秀的写法是这样的：
```js
// 更好的写法
for (const [index, value] of arr.entries()) console.log(index, value);
```

##  forEach循环

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300];

movements.forEach(function (movement) {
  if (movement > 0) {
    console.log(`You deposited ${movement}`);
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`);
  }
});
```

> forEach循环会接受一个callbackFunction，然后每次JavaScript调用这个callbackFunction的时候会把数组中的元素作为参数传递给callbackFunction，然后我们可以通过在callbackFunction里面定义的函数逻辑，对数组中的每个元素进行操作。

其实forEeach循环跟for-of循环有点像：

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300];

/////////////////////////////////////////////////
// for-of
for (const movement of movements) {
  if (movement > 0) {
    console.log(`You deposited ${movement}`);
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`);
  }
}

console.log('---------------------------')

// forEach
movements.forEach(function (movement) {
  if (movement > 0) {
    console.log(`You deposited ${movement}`);
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`);
  }
});
```

callbackFunction可以有三个参数：
```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300];

movements.forEach(function (movement, index, array) {
  if (movement > 0) {
    console.log(`Movement ${index + 1}: You deposited ${movement}`);
  } else {
    console.log(`Movement ${index + 1}: You withdrew ${Math.abs(movement)}`);
  }
});
```

# 可选链操作符

```js
const user = {
  name: '张三',
  address: null // 注意：address 是 null，没有 city 属性
};

// 直接访问：报错！因为 address 是 null，无法读取 city
console.log(user.address.city); // Uncaught TypeError: Cannot read properties of null (reading 'city')
```

为了避免报错，传统写法需要手动判断每个中间层级是否存在，代码冗长：
```js
// 传统写法：层层判断（繁琐）
if (user && user.address && user.address.city) {
  console.log(user.address.city);
} else {
  console.log('地址不存在');
}
```

使用`可选链操作符`：
```js
const user = {
  name: '张三',
  address: null,
};

// 如果 address 不是 null 或者 undefined ，再访问 city
// 如果是 undefined 或者 null，直接返回 ？前面的值
console.log(user.address?.city);
```

方法调用：
```js
const user = {
  name: '张三',
  address: null,
  sayHello() {
    console.log('hello world');
  },
};

// 如果这个方法存在就调用，否则就返回undefined
user.sayHello?.();
```

# 短路运算

**短路`或运算||`**

```js
// 短路运算符
// Use any data type, return any data type
console.log(3 || 'akbar');   // 输出：3
```
> 如果第一个值，比如3，那么直接就返回3，不会再看后面呢`akbar`

猜猜下面的代码输出什么？
```js
console.log('' || 'akbar');
console.log(true || 0);
console.log(undefined || null);
console.log(undefined || 0 || '' || null || 'hello' || 25);
```

**短路`与运算&&`**
```js
console.log(0 && 'akbar'); // 输出0
console.log(25 && 'akbar'); // 输出 akbar
```
只有第一个真的时候，才返回第二个。如果第一个假，就不会看第二个，直接返回第一个。

猜猜下面的代码输出什么？
```js
console.log('hello' && 23 && null && undefined);
```

# 忽略不使用的参数`_`

当函数需要接收某个参数（由于API要求或函数签名约定），但你在函数体内不需要使用它时，可以用 `_`来表示这个参数被有意忽略：

```js
// 数组的 forEach 方法，只需要值，不需要索引 
arr.forEach((_, index) => { 
    console.log(index); // 只使用索引，忽略值 
});
```

# 模板字符串

```js
const name = 'akbar'

const message = `my names ${name}`

console.log(message)
```

模板字符串输出多行字符串：


```js
console.log(`My name is akbar,
I am 24 years old`)
```

如果是用普通字符串输出多行，很麻烦的
```js
console.log('My name is akbar, \n\
I am 24 years old')
```

# 解构语法


JavaScript 的解构语法（Destructuring）是一种从数组或对象中提取数据的简洁方式。

1. **数组解构：**

```js
const arr = [1, 2, 3];
// 解构
const [a, b, c] = arr;

console.log(a, b, c);
```

如果只想解构第一个元素和最后一个元素
```js
const arr = [1, 2, 3];
// 解构
const [a, , c] = arr;

console.log(a, c);
```

两数交换值：
```js
// 两个变量交换值(传统方法)
let a = 'Hello';
let b = 'Friend';

let temp = a;
a = b;
b = temp;
console.log(a, b);
```

```js
// 两个变量交换值(使用解构语法)
let a = 'Hello';
let b = 'Friend';

[b, a] = [a, b];
console.log(a, b);
```

2. **Object解构：**

```js
const akbar = {
  name: 'akbar',
  age: 24,
  family: ['saipul', 'reyihanguli'],
};

const { name, age, family } = akbar;

console.log(name, age, family);
```

自定义属性名
```js
const akbar = {
  name: 'akbar',
  age: 24,
  family: ['saipul', 'reyihanguli'],
};

const { name: myName, age: myAge, family: myFamily } = akbar;

console.log(myName, myAge, myFamily);
```

设置默认值

```js
const akbar = {
  name: 'akbar',
  age: 24,
  family: ['saipul', 'reyihanguli'],
};

// 对象akbar没有home这个属性，为了避免undefined，可以赋默认值
const { name, age, family, home = 'hotan' } = akbar;

console.log(name, age, family, home);
```

函数传递对象参数

```js
function myFun(obj) {
  console.log(obj);
}

myFun({
  name: 'akbar',
  age: 23,
});
```

也可以这样写：
```js

// 解构获取参数， 不用关心参数的顺序
function myFun({ name, age }) {
  console.log(name, age);
}

myFun({
  name: 'akbar',
  age: 23,
});
```

# 展开运算符

跟解构语法有什么不同？

> 解构： 解构用于从数组或对象中提取值到独立的变量中。<br/>
> 展开：展开运算符用于将可迭代对象（如array、strings，maps，注意不包括对象）展开为单个元素。


```js
const arr = [1, 2, 3];

// 根据arr创建新的数组
// 传统写法
const badNewArr = [56, 34, arr[0], arr[1], arr[2]];
console.log(badNewArr)
```

```js
const arr = [1, 2, 3];

// 根据arr创建新的数组
// 使用展开运算符
const goodNewArr = [34, 45, ...arr];
console.log(goodNewArr);
```

函数参数传递展开运算符
```js
const arr = [1, 2, 3];

console.log(...arr);
// 相当于console.log(1,2,3)
```

字符串展开：

```js
const str = 'Akbar';
const strArr = [...str, ' ', 'A.'];
console.log(strArr);
```

**常见用途：**

1. shallow copy array：

```js
const arr = [1, 2, 3];

const newArr = [...arr];
console.log(newArr);
```

2. join two arrays or more

数组的concat()方法也可以

```js
const arr1 = [1, 2, 3];
const arr2 = [45, 63, 89];

const newArr = [...arr1, ...arr2];
console.log(newArr);
```

# rest语法

作用跟展开运算符正好相反。

```js
// 展开运算符，因为在等号（=）的
const arr = [1, 2, 3, ...[4, 5]];

// rest 语法，因为在等号（=）的左边
// 这里的others是一个数组，值是右边的3，4，5
const [a, b, ...others] = [1, 2, 3, 4, 5];
```

函数参数用法：
```js
function add(...numbers) {
  let sum = 0;
  for (let i = 0; i < numbers.length; i++) sum += numbers[i];

  console.log(sum);
}

add(1, 2, 3, 4);
add(12, 67);
```

# 复合赋值运算符

```js
jsconst rest1 = {
  name: 'akbar',
  numGuests: 0,
};

const rest2 = {
  name: 'La Piazza',
  owner: 'Giovanni Rossi',
};

// OR assignment operator
// 如果对象没有 numGuests 属性，或 numGuests 是「假值」，就赋值 10；否则保留原属性值”。
rest1.numGuests = rest1.numGuests || 10;
rest2.numGuests = rest2.numGuests || 10;

// 简化写法
rest1.numGuests ||= 10;
rest2.numGuests ||= 10;
```

**上面代码中的问题：** `||` 会把 `0` 当成 “无效假值”，但实际场景中 `numGuests: 0` 是合法的（表示餐厅当前没有客人）；

**修正方案：** 用之前讲的 **空值赋值运算符 `??=`**，只对 `null`/`undefined` 赋值，保留 `0` 这类合法假值：
```js
// 修正后：仅当 numGuests 是 null/undefined 时，才赋值 10 
rest1.numGuests ??= 10; // rest1.numGuests 仍为 0（正确保留） 
rest2.numGuests ??= 10; // rest2.numGuests 赋值为 10（正确新增）
```

# 事件参数

示例代码：
```js
document.addEventListener('keyup', function (event) {
  if (event.key === 'Escape' && !model.classList.contains('hidden'))
    closeModel();
});
```
> 上面的`event`就是事件参数。
> 当这个事件被触发的时候，JavaScript把事件对象作为参数给这个函数传进去，注意，我们自己没有调用这个函数，因为我们只是在这里声明了以下，由JavaScript来调用，并且传我们要求的参数`event`。

# window

`window`：浏览器中的全局对象（全局作用域的根）。

它代表浏览器窗口或标签页，包含控制窗口/浏览器行为的 API（计时器、地址栏、历史、对话框、localStorage 等）。

可以把它理解为“浏览器环境”的接口集合。

<mark>因为是全局对象，所以在全局作用域中可以直接访问其属性和方法，而不需要显式引用 window。</mark>

详细信息查看： https://developer.mozilla.org/zh-CN/docs/Web/API/Window

## windwo.location

获取/设置 window 对象的位置，或当前的 URL。

> `window.location` **引用本身只读**（不能改成指向新对象）<br/>

`window.location`和`Location`是什么关系？

名称                    | 类型                          | 作用                  |
| --------------------- | --------------------------- | ------------------- |
| **`window.location`** | **属性** (指向一个 `Location` 实例) | 当前窗口的 URL 信息对象      |
| **`Location`**        | **内置对象类（接口）**               | 定义用于处理 URL 的各种属性和方法

```js
class Location {...}         // 「类型」或「构造说明」
window.location = new Location // 浏览器内部创建好并挂载到 window 上
```
你无法 new Location，但浏览器已经替你创建好，并挂在 `window.location` 上供你使用。


MDN链接：https://developer.mozilla.org/zh-CN/docs/Web/API/Window/location

### 属性

常用的属性：
```js
location.href       // 整个URL
location.protocol   // http:
location.host       // wwww.xx.com:80
location.hostname   // 主机名
location.port       // 端口
location.pathname   // 路径
location.search     // ?a=1&b=2
location.hash       // #部分
```
### 方法

方法                      | 用途          |
| ----------------------- | ----------- |
| `location.assign(url)`  | 跳转到新页面（可返回） |
| `location.replace(url)` | 跳转但无法后退     |
| `location.reload()`     | 刷新页面

## window.console

> 注意：<br/>
> `console` 确实挂在 `window` 上，但它不是 `Window.prototype` 上定义的属性。<br/>
> 它是浏览器提供的 **全局对象**，并在运行环境中被放到 `window` 下以便访问。

```js
console.log(Window.prototype.hasOwnProperty("console")); // false
console.log("console" in window);                         // true
```

MDN 文档：https://developer.mozilla.org/zh-CN/docs/Web/API/Console_API

### 常用的实例方法

1.**console.log**：向 Web 控制台输出一条信息

2.**console.error**：向 Web 控制台输出一条错误消息。

3.**console.table**：将数据以表格的形式显示。

4.**console.warn**：向 Web 控制台输出一条警告信息。

## window.document

document：window 的一个属性（window.document）

表示当前网页的 DOM（Document Object Model）—— HTML 的节点树，是操作页面内容、结构、样式的主要对象。

通过 document 对象，可以访问和修改网页中的元素，实现动态交互效果。


![image.png](https://p0-xtjj-private.juejin.cn/tos-cn-i-73owjymdk6/4868143e8b98479388aea90c72de6d5a~tplv-73owjymdk6-jj-mark-v1:0:0:0:0:5o6Y6YeR5oqA5pyv56S-5Yy6IEAgTmljb2xhc0NhZ2U=:q75.awebp?policy=eyJ2bSI6MywidWlkIjoiMTIyOTY3MDE4OTYzMTMzOSJ9&rk3s=f64ab15b&x-orig-authkey=f32326d3454f2ac7e96d3d06cdbb035152127018&x-orig-expires=1765244479&x-orig-sign=dDZ%2BYG3lPcm6Mttr93jfzZHvbv4%3D)

MDN 文档： https://developer.mozilla.org/zh-CN/docs/Web/API/Document

### 实例属性

1. **document.documentElement**：获取根元素（如`<html>`）

```js
// 4.获取根元素
const rootElement = document.documentElement
```

2. **document.title**：获取网页标题。

```js
const title = document.title
console.log(`Page title: ${title}`)
```

3.**document.body**：获取body元素

### 实例方法

1. **document.querySelector()**：返回文档中与指定选择器匹配的`Element`对象。

2. **document.querySelectorAll**：返回与指定的选择器组匹配的文档中的元素列表

3. **getElementById()**：返回一个表示 `id`属性与指定字符串相匹配的元素的 `Element` 对象。

4. **document.getElementsByClassName()**：返回一个包含了所有指定类名的子元素的类数组对象。


## window.innerWidth

获取浏览器窗口的宽高。

## window.innerHeight

获取浏览器窗口的内容区域的高度，包括（已渲染的）水平滚动条。

## window.localStorage

### 实例方法

1.**localStorage.setItem()**：往localStorage存储数据，如果键名已存在，则更新其对应的值。

```js
// 格式
window.localStorage.setItem(keyName, keyValue)

// 比如
window.localStorage.setItem("myCat", "Tom");
```

2. **localStorage.getItem()**：返回该键的值；而如果不存在该键，则返回 `null`。

```js
let cat = window.localStorage.getItem("myCat");
```

3. **localStorage.removeItem()**：当传递一个键名时，删除该键（如果它存在）。

```js
window.localStorage.removeItem("myCat");
```

4. **localStorage.clear()**：清除所有数据。

```js
// 移除所有
localStorage.clear();
```

## window.alert()

弹出对话框。

## window.confirm()

确认对话框。

## window.prompt()

提示输入对话框。

## window.setInterval()

重复调用一个函数或执行一个代码片段，在每次调用之间具有固定的时间间隔。

MDN 文档：https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setInterval

## window.clearInterval()

window.setInterval()返回的值可以用来传递给 `clearInterval()`来清除定时器。

## window.setTimeout()

设置一个定时器，一旦定时器到期，就会执行一个函数或指定的代码片段。

MDN 文档：https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout

## window.clearTimeout()

可以将window.setTimeout()返回的值传递给 `clearTimeout()`来取消该定时器。

## window.scrollTo()

滚动窗口到指定位置

```js
window.scrollTo(0, 500); // 滚动到垂直位置500px
```

# DOM, Node, Element之间的关系

```txt
DOM (Document Object Model)
│
└── Node（所有节点的基类）
    ├── Document            document
    ├── Element             div, span, a, p...
    ├── Text                文本节点
    ├── Comment             注释节点
    ├── Attr                属性节点
    └── ... etc
```

# Node

Node 是 DOM 中的所有节点；

Element要继承Node

## 实例属性

1. **textContent**：表示一个节点及其后代的文本内容。

实例代码：

```js
document.querySelector('.message').textContent = 'Correct Number'
```

解释：
```js
document.querySelector('.message')
    ↓ 返回的对象是 Element
Element 继承自 Node
    ↓
所以可以使用 Node 的属性和方法
```

# Element

**Element** 是最通用的基类，`Document`中的所有元素对象（即表示元素的对象）都继承自它。它只具有各种元素共有的方法和属性。

## 实例属性

1. **classList**：返回一个元素 `class` 属性的动态 `DOMTokenList` 集合。这可以用于操作 class 集合。

```js
// 使用 classList API 移除、添加类值 
div.classList.add("anotherclass");
div.classList.remove("foo"); 

// 如果 visible 类值已存在，则移除它，否则添加它 
div.classList.toggle("visible");

// 将类值 "foo" 替换成 "bar" 
div.classList.replace("foo", "bar");
```

2. `innerHTML`：设置或获取 HTML 语法表示的元素的后代。

## 示例方法

1. `insertAdjacentHTML()`：将指定的文本解析为 `Element`元素，并将结果节点插入到 DOM 树中的指定位置。


# HTMLInputElement

**`HTMLInputElement`** 接口提供了特定的属性和方法，用于管理 `<input>`元素的选项、布局和外观。

MDN 链接：https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLInputElement

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202211244636.png)

1. **value**: current value of the [`<input>`] element as a string.

> `<input>`、`<textarea>` 等 **可输入元素的内容并不是一个文本节点**，而是存储在它们的 **value 属性中**。
> 为什么呢？
> 因为 `<input>` 标签是**自闭合的**，没有内部文本节点：

比如：
```js
document.querySelector("input").value = "Hello"   // 正确 ✔
document.querySelector("input").textContent = "Hello" // 无效 ❌
```

```js
<input type="text" />   <!-- 没有像 <p>xxx</p> 那样的内容节点 -->
```

# EventTarget

只要一个对象继承了 `EventTarget`，它就能使用 `addEventListener()`、`removeEventListener()`。

```js
EventTarget
   ├── Node
   │    ├── Element
   │    │    ├── HTMLElement
   │    │    │    ├── HTMLInputElement
   │    │    │    ├── HTMLButtonElement
   │    │    │    ├── ...各种元素
   │    └── Document
   └── Window
```
对象                     | 示例                               |
| ---------------------- | -------------------------------- |
| `Element`              | div, p, span, button, input…     |
| `Document`             | `document.addEventListener(...)` |
| `Window`               | `window.addEventListener(...)`   |
| 其它继承 `EventTarget` 的对象 | 如自定义事件目标

# HTMLElement

HTMLElement 接口表示所有的HTML元素。

继承自父接口 `Element`。

1. **style**：为元素的内联 `style`属性中定义的属性分配值。

比如：
```js
document.body.style.backgroundColor = '#60b347'
```

# 为什么说JavaScript不是纯解释型语言？

> 现代 JS 引擎早已不是单纯逐行解释执行，而是结合了解释执行 + 编译执行 + 多段优化机制。

现代v8引擎等的运行流程是这样的：

```txt
JS 源码
   ↓  解析解析成 AST
解释器 Ignition（快速执行）
   ↓
JIT 编译器 TurboFan（热点代码进一步优化编译为机器码）
   ↓
CPU 直接执行高性能本地代码
```

举个例子：

当 JS 引擎运行一个**循环执行很多次的 function**时，会认为它是“热点代码”：
```js
function add(a, b) {
  return a + b;
}

for (let i = 0; i < 1e9; i++) {
  add(1, 2);
}
```

V8 会做两件事：

1.  先解释执行（启动快）
1.  发现执行频繁后 → **JIT 编译，并优化成机器码（提速）**

纯解释型语言不会做第 2 步，因此**现代 JS 就不是纯解释型语言了**。

# 执行上下文 和 作用域链

[JavaScript 执行上下文、作用域与词法环境详解一、执行上下文（Execution Context） 定义： 执行 - 掘金](https://juejin.cn/post/7486429532720349199)

# this 关键字

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202210422015.png)