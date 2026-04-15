---
title: 深入学习JavaScript
date: 2025-12-02 20:05:35
tags: ['JavaScript']
categories: JavaScript
cover: https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202200832048.png
---

# JavaScript 历史

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202201043998.png)

> 我们现在说的 es6 就是 2015 年发布的版本。

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202201143499.png)

# 数据类型

## 原始类型

### Number：整数，小数

**Number 常用方法和技巧：**

```js
// Conversion
console.log(Number('23'))
console.log(+'23')

// Parsing(解析)
console.log(Number.parseInt('30px')) // 输出30
console.log(Number.parseInt('e20')) // 输出NaN

console.log(Number.parseInt('30px', 10)) // 用10进制来解析
console.log(Number.parseInt('1010', 2)) // 用2进制来解析，输出10

console.log(Number.parseInt('2.5rem')) // 输出2
console.log(Number.parseFloat('2.5rem')) // 输出2.5

// 检测是否为数字(推荐)
console.log(Number.isFinite(20)) // true
console.log(Number.isFinite('20')) // false

// Checking if value is NaN
console.log(Number.isNaN(+'20X')) // true
console.log(Number.isNaN(23 / 0)) // false
```

```js
let age = 23
```

### String：字符串

```js
let name = 'akbar'

let name = 'akbar'
```

{% note primary modern %}
字符串虽然是原始类型，但当我们调用其方法时，JavaScript 引擎会通过“原始值包装”机制，自动将其临时转换为 String 对象来执行操作，完成后再转换回原始值，因此它拥有了对象的方法调用能力。
{% endnote %}

1. **通过索引获取字符：**

```js
const plane = 'A320'
console.log(plane[0])

// 字符串字面量也可以直接使用索引
console.log('A320'[0])

// 或者使用 at() 方法
console.log(plane.at(0)) // 'A'
console.log(plane.at(-1)) // '0'（最后一个字符）
```

2. **string.lenght：获取字符串长度**

3. **string.indexOF()：获取字符的下表**

4. **string.lastIndexOf()：该字符最后一次出现的索引**

5. **string.slice()：方法提取字符串的一部分，并将其作为新字符串返回，而不修改原始字符串**

```js
const str = 'The quick brown fox jumps over the lazy dog.'

console.log(str.slice(31))
// Expected output: "the lazy dog."

console.log(str.slice(4, 19))
// Expected output: "quick brown fox"
```

6. **string.toLowerCase()：转换成小写**

7. **string.toUpperCase()：转换成大学**

8. **string.trim()：从字符串的两端移除空白字符，并返回一个新的字符串，而不会修改原始字符串。**

9. **string.replace()：替换指定的字符。**

10. **string.replaceAll()：其中匹配的都被替换掉**

```js
const paragraph = "I think Ruth's dog is cuter than your dog!"

console.log(paragraph.replaceAll('dog', 'monkey'))
```

11. **string.includes()：判断字符串是否包好这个字符串。**

12. **string.starsWith()：判断是否以什么什么开头**

13. **string.endsWith()：判断是否以什么什么结尾。**

14. **string.split()：接受一个模式，通过搜索模式将字符串分割成一个有序的子串列表，将这些子串放入一个数组，并返回该数组。**

15. **string.padStart()：用另一个字符串填充当前字符串（如果需要会重复填充），直到达到给定的长度。填充是从当前字符串的开头开始的。**

16. **string.repeat()：构造并返回一个新字符串，其中包含指定数量的所调用的字符串副本，这些副本连接在一起。**

```js
const mood = 'Happy! '

console.log(`I feel ${mood.repeat(3)}`)
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
let b = null
```

跟 Undefined 比较：

| 值          | 由谁决定       | 含义                     |
| ----------- | -------------- | ------------------------ |
| `undefined` | JS 自动赋值    | 变量存在，但还没有内容   |
| `null`      | 程序员主动赋值 | 变量被刻意设为空（清空） |

> **注意**：<br/>
>
> ```js
> console.log(typeof null)
> ```
>
> 上面的代码会输出`object`，但是按道理应该输出`null`，所以这是 JavaScript 的一个 bug。

## NaN

{% note primary modern %}
`NaN` 是一个特殊的数值，表示“不是一个合法的数字（Not-a-Number）”，但它本身却属于 `number` 类型。
{% endnote %}

```js
typeof NaN // "number"
```

它表示一个数学计算失败后产生的数值。

比如：

```js
Number('hello') // NaN
0 / 0 // NaN
Math.sqrt(-1) // NaN
```

`NaN` 不等于任何东西，包括它自己

```js
NaN === NaN // false
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

### 数组 Array

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

{% btn
'https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

```js
const array1 = ['a', 'b', 'c']
const array2 = ['d', 'e', 'f']
const array3 = array1.concat(array2)

console.log(array3)
// Expected output: Array ["a", "b", "c", "d", "e", "f"]
```

1. `join()`：将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串，用逗号或指定的分隔符字符串分隔。如果数组只有一个元素，那么将返回该元素而不使用分隔符。

> 如果省略参数，数组元素用逗号（,）分隔。
> 如果 separator 是空字符串（""），则所有元素之间都没有任何字符。

```js
const user = 'Steven Thomas Williams'
const username = user
  .toLocaleLowerCase()
  .split(' ')
  .map(name => name.at(0)) // ['s', 't', 'w']
  .join('')

console.log(username)
```

1.  `slice()`：返回一个新的数组对象，这一对象是一个由  `start`  和  `end`  决定的原数组的浅拷贝（包括  `start`，不包括  `end`）

```js
const arr = ['a', 'b', 'c', 'd', 'e']

console.log(arr.slice(2)) // 不会修改原数组，返回一个从索引2开始到结束的新数组
console.log(arr.slice(2, 4)) // 返回一个从索引2开始到索引4（不包括4）的新数组
console.log(arr.slice(-2)) // 返回数组的最后两个元素
console.log(arr.slice()) // 进行shallow copy
```

11. `splice()`：就地移除或者替换已存在的元素和/或添加新的元素。

```js
const arr = ['a', 'b', 'c', 'd', 'e']

console.log(arr.splice(2)) // 修改原数组，删除从索引2开始到结束的元素，并返回删除的元素
console.log(arr.splice(1, 2))
console.log(arr)

// 删除最后一个元素
arr.splice(-1)
console.log(arr)
```

在 vue 中使用：

```html
<ul>
  <li v-for="(item, index) in items" :key="index">
    {{ item }}
    <button @click="removeItem(index)">Remove</button>
  </li>
</ul>
```

```js
Vue.createApp({
  data() {
    return {
      items: [],
    }
  },

  methods: {
    removeItem(index) {
      // 从数组下标 index 开始删除 1 个元素
      this.items.splice(index, 1)
    },
  },
}).mount('#app')
```

12. `reverse()`：就地反转数组中的元素，并返回同一数组的引用。数组的第一个元素会变成最后一个，数组的最后一个元素变成第一个。换句话说，数组中的元素顺序将被翻转，变为与之前相反的方向。

13. `at()`：接收一个整数值并返回该索引对应的元素，允许正数和负数。负整数从数组中的最后一个元素开始倒数。

```js
const arr = [23, 11, 64]
console.log(arr.at(-1)) // 最后一个元素
console.log(arr.at(0)) // 第一个元素
```

{% note info no-icon %}
几个非常常用的数组方法：
{% endnote %}

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251203093709179.png)

1. `map`方法：对遍历的每个元素进行我们指定的操作，然后返回新的数组，不会修改原始数组。

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

// 欧元转换成美元, 假设汇率为1.1
const eurToUsd = 1.1
const movementsUSD = movements.map(function (movement) {
  return movement * eurToUsd
})

console.log(movementsUSD)
```

如果用 for-of：

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

const movementsUSDfor = []
for (const movement of movements) movementsUSDfor.push(movement * eurToUsd)

// 如果使用箭头函数
// const movementsUSD = movements.map(movement => movement * eurToUsd);
// 使用全部参数
// const movementsUSD = movements.map((movement, index, array) => movement * eurToUsd);

console.log(movementsUSDfor)
```

2. `filter`方法：

> 不要想的太复杂，心里想什么，就写什么就可以了，比如我们要的是>0 的，那就写`movement => movement > 0`,如果我们要的是<0 的，那就写`movement => movement < 0`

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

// 过滤掉movements中的负值，只保留正值
const deposits = movements.filter(function (movement) {
  return movement > 0
})
console.log(deposits)

// 使用箭头函数
// const deposits = movements.filter(movement => movement > 0);
```

如果使用 for-of：

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

// 如果使用for-of
const depositsFor = []
for (const movement of movements) if (movement > 0) depositsFor.push(movement)

console.log(depositsFor)
```

3. `reduce`方法：

```js
// accumulator -> snowball，就是说accumulator会不断累积
// reduce会遍历数组的每一个元素, 每次遍历对应的元素累加到accumulator上，最终返回一个值
// reduce的第二个参数是accumulator的初始值
const balance = movements.reduce(function (accumulator, current, index, array) {
  console.log(`Iteration ${index}, ${accumulator}`)
  return accumulator + current
}, 0)

console.log(balance)

// 使用箭头函数
// const balance = movements.reduce((accumulator, current) => accumulator + current, 0);
```

{% note primary flat %}
如果没有指定 initialValue，则 accumulator 初始化为数组中的第一个值，并且 callbackFn 从数组中的第二个值作为 currentValue 开始执行。
{% endnote %}

如果使用 for-of：

```js
let sum = 0 // 相当于 accumulator，并设置了初始值等于0
for (const movement of movements) sum += movement
console.log(sum)
```

> 为什么不用 for-of，而推荐使用 reduce 呢？
> 因为 reduce 不需要在外面定义一个变量，比如 for-of 中的 sum。reduce 可以直接返回我们需要的数据。

找到数组中的最大值：

```js
// Maximum value
const max = movements.reduce((acc, mov) => {
  if (acc > mov) return acc
  else return mov
}, movements[0])

console.log(max)
```

4. `find`方法：返回数组中满足提供的测试函数的第一个元素的值。

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

const firstWithdrawal = movements.find(movement => movement < 0)

console.log(firstWithdrawal)
```

5. `findIndex`方法：返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回 -1。

6. `some`方法：测试数组中是否至少有一个元素通过了由提供的函数实现的测试。如果在数组中找到一个元素使得提供的函数返回 true，则返回 true；否则返回 false。

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

// 判断是否有任何存款
const anyDeposits = movements.some(movement => movement > 0)
console.log(anyDeposits)
```

7. `every`方法：测试一个数组内的所有元素是否都能通过指定函数的测试。它返回一个布尔值。

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

// 输出false
console.log(movements.every(movement => movement > 0))
```

8. `flat`方法：创建一个新的数组，并根据指定深度递归地将所有子数组元素拼接到新的数组中。

```js
const arr = [[1, 2, 3], 4, 5, 6, [7, 8, 9]]
const flatArr = arr.flat()
console.log(flatArr)
```

9. `sort`方法：对数组的元素进行排序，并返回排序后的数组。默认排序顺序是根据字符串Unicode码点。

```js
// Strings
const owners = ['Jonas', 'Zach', 'Adam', 'Martha']
// 根据字母顺序排序
console.log(owners.sort()) 

// Numbers
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]
// 默认排序是根据字符串Unicode码点，就是把数字也当作字符串排序
console.log(movements.sort())

/**
 * 自定义排序函数，升序
 * 如果 返回 < 0 ，a 会被排在 b 之前
 * 如果 返回 > 0 ，b 会被排在 a 之前
 */
console.log(
  movements.sort((a, b) => {
    if (a > b) return 1
    if (a < b) return -1
  })
)
```

{% btn
 'https://www.bilibili.com/video/BV1vA4y197C7?spm_id_from=333.788.videopod.episodes&vd_source=28e37be50df53ebbf04edfcc6228018f&p=153',
 'Jonas老师-数组sort方法',
 far fa-hand-point-right,blue
 %}

**Array 方法总结：**

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251203154436149.png)

### 对象 Object

{% note primary modern %}
注意，object 中的`{}`只是定义对象时候要用的括号而已，不是`Block`，不会创建自己的作用域。
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
  calcAge: function (birthYear) {
    return 2025 - birthYear
  },
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

**对象转换成字符串**：

我们可以使用`JSON.stringify()`方法把对象转换成字符串：

```js
const akbar = {
  name: 'akbar',
  job: 'noJob',
  birthYear: 2001,
}

console.log(JSON.stringify(akbar))
```

**对象增强写法**

1. **属性名相同，可以只写一个：**

```js
const family = {
  item1: 'akbar',
  item2: 'sipul',
}

const akbar = {
  name: 'akbar',
  age: 24,
  // family: family,
  family,
}

console.log(akbar)
```

2. **省略 function 关键字**

```js
const family = {
  item1: 'akbar',
  item2: 'sipul',
}

const akbar = {
  name: 'akbar',
  age: 24,
  family,
  // 不用这样写：
  // printAge: function() {}
  printAge() {
    console.log(this.age)
  },
}

console.log(akbar)
akbar.printAge()
```

### Sets

`Set`  对象是值的合集（collection）。集合（set）中的元素**只会出现一次**，即集合中的元素是唯一的。

```js
const orderSet = new Set(['Pasta', 'Pizza', 'Pizza', 'Risotto', 'Pasta', 'Pizza'])

console.log(orderSet)
```

但是输出是：

```txt
Set(3) {'Pasta', 'Pizza', 'Risotto'}
```

**常用的方法：**

1. set.size：set 的长度

```js
const orderSet = new Set(['Pasta', 'Pizza', 'Pizza', 'Risotto', 'Pasta', 'Pizza'])

console.log(orderSet.size) // 输出 3
```

2. set.has()：判断某个元素是否在 set 里面，很像 array 的 include 方法

```js
const orderSet = new Set(['Pasta', 'Pizza', 'Pizza', 'Risotto', 'Pasta', 'Pizza'])

console.log(orderSet.has('Pasta')) // 输出 true
```

3. set.add()：添加元素

```js
const orderSet = new Set(['Pasta', 'Pizza', 'Pizza', 'Risotto', 'Pasta', 'Pizza'])

orderSet.add('Lamian')
console.log(orderSet)
```

4. set.delete()：删除元素

5. set.clear()：删除 set 中的所有元素

**遍历 set：**

```js
const orderSet = new Set(['Pasta', 'Pizza', 'Pizza', 'Risotto', 'Pasta', 'Pizza'])

for (const item of orderSet) console.log(item)
```

**set 的使用场景：**

1. 从数组中删除重复的元素。

```js
const meals = ['Pasta', 'Pizza', 'Pizza', 'Risotto', 'Pasta', 'Pizza']

const newMeals = [...new Set(meals)]

console.log(newMeals)
```

### Maps

`Map`  对象是键值对的集合。`Map`  中的一个键**只能出现一次**；它在  `Map`  的集合中是独一无二的。任何类型的数据都可以作为键（key）。

但是 object 不一样，object 的 key 只能是字符串。

```js
const rest = new Map()
rest.set('name', 'Classico Italiano')
rest.set(1, 'Firenze, Italy')
console.log(rest)
```

set 方法返回插入元素之后的 map，所以我们可以链式调用：

```js
const rest = new Map()
rest.set('name', 'Classico Italiano').set(1, 'Firenze, Italy')
console.log(rest)
```

1. map.get()：根据 key 获取其值

2. map.has()：根据 key 判断其对应的值是否已经存在。

3. map.delete()：根据 key 删除

4. map.size：map 的长度

5. map.clear()：清空 map

## 数据结构使用建议

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202210147042.png)

# 原始类型和引用类型内存分析

## 原始类型的内存分析

原始类型存储在栈内存（Stack）中， 变量存储的是实际的值，而不是引用。

```js
let a = 10 // 在栈内存中存储值10
a = 20 // 改变a的值为20，只是改变值，不改变内存地址
let b = a // b存储的是a的值20，不是引用
```

## 引用类型

引用类型存储在堆内存（Heap）中， 变量存储的是对象的引用地址，而不是实际的值。

```js
const obj1 = { name: 'akbar' } // 在堆内存中创建对象，并将引用地址存储在obj1中
const obj2 = obj1 // obj2存储的是obj1的引用地址
obj2.name = 'sipul' // 通过obj2修改对象的属性，obj1也会受到影响
```

## 工程案例

1. **在 vue 项目中经常的案例**：

```js
export default {
  data() {
    return {
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description:
            'The official Vue.js guide is a great resource to get started with Vue.js and learn about its core concepts and features.',
          link: 'https://vuejs.org/',
        },
        {
          id: 'google',
          title: 'Google',
          description:
            'Google is a popular search engine that can help you find information on the web quickly and easily.',
          link: 'https://www.google.com/',
        },
      ],
    }
  },

  methods: {
    removeResource(resourceId) {
      /**
       * 这里filter返回一个新的数组，然后把这个新的数组的引用地址赋值给storedResources，
       * 所以原来的this.storedResources没有收到任何影响
       * 造成的结果是，provide里面的resources引用地址没有变化
       * 所以页面上依然能看到原来的资源列表
       *
       * 解决办法：不要把新的数组赋值给this.storedResources，而是直接在原来的数组上进行修改（就地修改）
       */
      this.storedResources = this.storedResources.filter(resource => resource.id !== resourceId)
    },
  },

  provide() {
    return {
      // 还是原来的this.storedResources引用地址，没有收到任何影响
      resources: this.storedResources,
      removeResource: this.removeResource,
    }
  },
}
```

解决办法：

```js
removeResource(resourceId) {
  const index = this.storedResources.findIndex(resource => resource.id === resourceId)
  if (index !== -1) {
    // 直接在原来的数组上进行修改（就地修改）
    this.storedResources.splice(index, 1)
  }
},
```

# 对象拷贝

## 浅拷贝（Shallow Copy）

浅拷贝是指创建一个新对象，这个新对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值；如果属性是引用类型，拷贝的就是内存地址。

1. **使用 Object.assign() 方法进行浅拷贝：**

> `Object.assign()`一个或者多个源对象中所有可枚举的自有属性复制到目标对象，并返回修改后的目标对象。
> 语法：`const returnedTarget = Object.assign(target, source);`

```js
const akbar = {
  name: 'akbar',
  age: 24,
  family: {
    father: 'sipul',
    mother: 'siti',
  },
}

const akbarShallowCopy = Object.assign({}, akbar)
```

akbarShallowCopy.family 存的还是原始对象的引用地址。

1. **使用扩展运算符（Spread Operator）进行浅拷贝：**

```js
const akbarShallowCopy = { ...akbar }
```

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

1.  **作用域范围不同**

var - 函数作用域

```js
function printAge() {
  if (birthYear >= 2001 && birthYear <= 2025) {
    var millenial = true // var 的作用域是整个函数
    // ...
  }
  console.log(millenial) // ✅ 可以访问，输出: true
}
```

我来通过这段代码详细讲解  `var`和  `let`的区别：

## 1. 作用域范围不同

### var - 函数作用域

```js
function printAge() {
  if (birthYear >= 2001 && birthYear <= 2025) {
    var millenial = true // var 的作用域是整个函数
    // ...
  }
  console.log(millenial) // ✅ 可以访问，输出: true
}
```

`var`在函数内部任何地方声明，在整个函数内都可访问。

let - 块级作用域

```js
function printAge() {
  if (birthYear >= 2001 && birthYear <= 2025) {
    let str = `Oh, and you're a millenial, ${firstName}` // let 的作用域是当前代码块
    // ...
  }
  console.log(str) // ❌ ReferenceError: str is not defined
}
```

`let`只在声明它的代码块（`{}`内部）内有效。

2. **变量提升的差异**

var - 会提升并初始化为 undefined

```js
function example() {
  console.log(x) // undefined (不会报错)
  var x = 5
}
```

let - 会提升但不会初始化

```js
function example() {
  console.log(x) // ❌ ReferenceError: Cannot access 'x' before initialization
  let x = 5
}
```

3. **重复声明**

var - 允许重复声明

```js
var x = 1
var x = 2 // ✅ 不会报错
```

let - 不允许重复声明

```js
let y = 1
let y = 2 // ❌ SyntaxError: Identifier 'y' has already been declared
```

4. **全局作用域的行为差异**

var - 会成为全局对象的属性

```js
var globalVar = 'hello'
console.log(window.globalVar) // 在浏览器中输出: 'hello'
```

let - 不会成为全局对象的属性

```js
let globalLet = 'hello'
console.log(window.globalLet) // undefined
```

# 操作符

## 幂次

```js
const myNumber = 2 ** 3 // 2的3次方
```

## `++ 和 --`

`++x`是先自身加 1 再参与运算，`x++`是先参与运算再自身加 1。

# 类型转换

## 手动转换

```js
// 转换成数字类型
console.log(Number('123'))

// 转换成字符串类型
console.log(String(23))
```

> 注意：
> 可以转换成 Number，String，Boolean，但是不能转换成 undefined，null。

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

5 个 falsy value：

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
1 === '1' // false
true === 1 // false
null === undefined // false
```

**`==`（宽松相等）**

**会先进行类型转换（Type Coercion），再比较。**

也就是说，它会“强行把两边转换成同一种类型”，然后再比。

```js
1 == '1' // true（字符串变成数字）
true == 1 // true（true 变成 1）
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

**什么样的场景更适合使用 switch case**:

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
3 + 4 // 产生值7
1991 // 产生值1991
tru && false && !false // 产生值false
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
if (23 > 10) {
  console.log('hello world')
}
```

上面的代码被执行，但是不会产生值，比如这里的 if 语句块产生或者返回一个值了吗？

**注意事项**：

模板字符串中不能写`声明语句`:

```js
// 错误的写法
console.log(`I am ${if (23 > 10) 'older' else 'younger'} than 10`)
```

# strict mode

严格模式通过下面的字符串来开启，只要把这个字符串写道 JavaScript 文件的最上面就可以了：

```js
'use strict'
```

> **严格模式让 JavaScript 更安全、更规范、更容易发现错误。**  
> 它禁止一些“危险行为”，让你写出的代码更可靠。

# 函数

> 其实函数也是一种 object,所以函数也有自己的方法,比如`call()`、`bind()`、`apply()`等方法

## 普通函数

```js
// 普通函数
function logger() {
  console.log('My name is Jonas')
}

// 调用
logger()
```

> 虽然这个函数没有返回值，但是它返回一个 undefined。

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

立即执行函数（IIFE - Immediately Invoked Function Expression）：

```js
;(function () {
  console.log('This function runs once immediately!')
})()
```

> 注意这里的分号`;`，因为如果前面没有分号的话，可能会报错。

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
    console.log(`${greeting} ${name}`)
  }
}

// 调用
const greeter = greet('Hello')
greeter('Akbar')

// 简化调用
greet('Hi')('Akbar')
```

用箭头函数实现：

```js
const greet = greeting => name => console.log(`${greeting} ${name}`)

const greeter = greet('Hello')
greeter('akbar')

greet('Hi')('Akbar')
```

## 函数参数设置默认值

比如(ES6)：

```js
const bookings = []

const createBooking = function (flightNum, numPassengers = 1, price = 199) {
  const booking = {
    flightNum,
    numPassengers,
    price,
  }

  console.log(booking)
  bookings.push(booking)
}

createBooking('LH123')
```

如果不适用 es6，应该这样写：

```js
const bookings = []

const createBooking = function (flightNum, numPassengers, price) {
  // 通过短路运算设置默认值
  numPassengers ||= 1
  price ||= 199

  const booking = {
    flightNum,
    numPassengers,
    price,
  }

  console.log(booking)
  bookings.push(booking)
}

createBooking('LH123')
```

# 循环

## for 循环

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

- `continue`： 跳过当前这轮循环，进入下一轮循环

```js
// continue
const myArray = ['akbar', 'age', 'major', 2025 - 2001, 'location', 'hobbies']

console.log('-----ONLY STRINGS----')
for (let i = 0; i < myArray.length; i++) {
  if (typeof myArray[i] !== 'string') continue // 跳过当前这轮循环，进入下一轮循环

  console.log(myArray[i])
}

// 所以不会输出类型是数字的元素
```

- `break`：直接结束循环

```js
const myArray = ['akbar', 'age', 'major', 2025 - 2001, 'location', 'hobbies']

console.log('-----BREAK WITH NUMBER----')
for (let i = 0; i < myArray.length; i++) {
  if (typeof myArray[i] !== 'string') break // 遇到类型不是string的时候，直接结束循环

  console.log(myArray[i])
}
```

## while 循环

> 在我们不知道到底进行多少轮循环的时候，while 循环是一个不错的选择

```js
let dice = Math.trunc(Math.random() * 6) + 1

while (dice !== 6) {
  console.log(`You rolled a ${dice}`)
  // 每次循环改变dice
  dice = Math.trunc(Math.random() * 6) + 1
  if (dice === 6) console.log('Loop is about to end ...')
}
```

## for-of 循环

```js
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]

// 只能拿到item，拿不到索引
for (const item of arr) console.log(item)

// 可以拿到索引
for (const item of arr.entries()) console.log(item)
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
for (const [index, value] of arr.entries()) console.log(index, value)
```

## forEach 循环

{% note primary flat %}
对数组里的每个元素“做点什么”，而不需要这个操作产生一个新数组时，forEach 就是一个非常自然和直接的选择。
{% endnote %}

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

movements.forEach(function (movement) {
  if (movement > 0) {
    console.log(`You deposited ${movement}`)
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`)
  }
})
```

> forEach 循环会接受一个 callbackFunction，然后每次 JavaScript 调用这个 callbackFunction 的时候会把数组中的元素作为参数传递给 callbackFunction，然后我们可以通过在 callbackFunction 里面定义的函数逻辑，对数组中的每个元素进行操作。

其实 forEeach 循环跟 for-of 循环有点像：

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

/////////////////////////////////////////////////
// for-of
for (const movement of movements) {
  if (movement > 0) {
    console.log(`You deposited ${movement}`)
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`)
  }
}

console.log('---------------------------')

// forEach
movements.forEach(function (movement) {
  if (movement > 0) {
    console.log(`You deposited ${movement}`)
  } else {
    console.log(`You withdrew ${Math.abs(movement)}`)
  }
})
```

callbackFunction 可以有三个参数：

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300]

movements.forEach(function (movement, index, array) {
  if (movement > 0) {
    console.log(`Movement ${index + 1}: You deposited ${movement}`)
  } else {
    console.log(`Movement ${index + 1}: You withdrew ${Math.abs(movement)}`)
  }
})
```

## for-in 循环

`for-in`循环主要用于遍历对象的可枚举属性（包括继承的属性）。它会遍历对象的所有可枚举属性的键（key）。

{% btn
'https://tutorial.javascript.ac.cn/javascript-enumerable-properties/',
 '网友博客链接',
 far fa-hand-point-right,blue
larger %}

# 可选链操作符

```js
const user = {
  name: '张三',
  address: null, // 注意：address 是 null，没有 city 属性
}

// 直接访问：报错！因为 address 是 null，无法读取 city
console.log(user.address.city) // Uncaught TypeError: Cannot read properties of null (reading 'city')
```

为了避免报错，传统写法需要手动判断每个中间层级是否存在，代码冗长：

```js
// 传统写法：层层判断（繁琐）
if (user && user.address && user.address.city) {
  console.log(user.address.city)
} else {
  console.log('地址不存在')
}
```

使用`可选链操作符`：

```js
const user = {
  name: '张三',
  address: null,
}

// 如果 address 不是 null 或者 undefined ，再访问 city
// 如果是 undefined 或者 null，直接返回 ？前面的值
console.log(user.address?.city)
```

方法调用：

```js
const user = {
  name: '张三',
  address: null,
  sayHello() {
    console.log('hello world')
  },
}

// 如果这个方法存在就调用，否则就返回undefined
user.sayHello?.()
```

# 短路运算

## 短路`或运算||`

```js
// 短路运算符
// Use any data type, return any data type
console.log(3 || 'akbar') // 输出：3
```

> 如果第一个值是真，比如 3，那么直接就返回 3，不会再看后面呢`akbar`

猜猜下面的代码输出什么？

```js
console.log('' || 'akbar')
console.log(true || 0)
console.log(undefined || null)
console.log(undefined || 0 || '' || null || 'hello' || 25)
```

## 短路`与运算&&`

```js
console.log(0 && 'akbar') // 输出0
console.log(25 && 'akbar') // 输出 akbar
```

> 只有第一个真的时候，才返回第二个。如果第一个假，就不会看第二个，直接返回第一个。

猜猜下面的代码输出什么？

```js
console.log('hello' && 23 && null && undefined)
```

# 忽略不使用的参数`_`

当函数需要接收某个参数（由于 API 要求或函数签名约定），但你在函数体内不需要使用它时，可以用  `_`来表示这个参数被有意忽略：

```js
// 数组的 forEach 方法，只需要值，不需要索引
arr.forEach((_, index) => {
  console.log(index) // 只使用索引，忽略值
})
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
console.log(
  'My name is akbar, \n\
I am 24 years old',
)
```

# 解构语法

JavaScript 的解构语法（Destructuring）是一种从数组或对象中提取数据的简洁方式。

1. **数组解构：**

```js
const arr = [1, 2, 3]
// 解构
const [a, b, c] = arr

console.log(a, b, c)
```

如果只想解构第一个元素和最后一个元素

```js
const arr = [1, 2, 3]
// 解构
const [a, , c] = arr

console.log(a, c)
```

两数交换值：

```js
// 两个变量交换值(传统方法)
let a = 'Hello'
let b = 'Friend'

let temp = a
a = b
b = temp
console.log(a, b)
```

```js
// 两个变量交换值(使用解构语法)
let a = 'Hello'
let b = 'Friend'

;[b, a] = [a, b]
console.log(a, b)
```

2. **Object 解构：**

```js
const akbar = {
  name: 'akbar',
  age: 24,
  family: ['saipul', 'reyihanguli'],
}

const { name, age, family } = akbar

console.log(name, age, family)
```

> 对象解构和数组解构的区别：对象解构是根据`属性名`来解构的，数组解构是根据`位置`来解构的。
> 所以解构对象的时候，变量名必须和属性名一致。

自定义属性名

```js
const akbar = {
  name: 'akbar',
  age: 24,
  family: ['saipul', 'reyihanguli'],
}

const { name: myName, age: myAge, family: myFamily } = akbar

console.log(myName, myAge, myFamily)
```

设置默认值

```js
const akbar = {
  name: 'akbar',
  age: 24,
  family: ['saipul', 'reyihanguli'],
}

// 对象akbar没有home这个属性，为了避免undefined，可以赋默认值
const { name, age, family, home = 'hotan' } = akbar

console.log(name, age, family, home)
```

函数传递对象参数

```js
function myFun(obj) {
  console.log(obj)
}

myFun({
  name: 'akbar',
  age: 23,
})
```

也可以这样写：

```js
// 解构获取参数， 不用关心参数的顺序
function myFun({ name, age }) {
  console.log(name, age)
}

myFun({
  name: 'akbar',
  age: 23,
})
```

# 展开运算符

跟解构语法有什么不同？

> 解构： 解构用于从数组或对象中提取值到独立的变量中。<br/>
> 展开：展开运算符用于将可迭代对象（如 array、strings，maps，sets,（{% label 注意不包括对象，object不可迭代不是因为object的属性是无序的，而是因为对象本身不实现迭代协议 blue %}）展开为单个元素。

```js
const arr = [1, 2, 3]

// 根据arr创建新的数组
// 传统写法
const badNewArr = [56, 34, arr[0], arr[1], arr[2]]
console.log(badNewArr)
```

```js
const arr = [1, 2, 3]

// 根据arr创建新的数组
// 使用展开运算符
const goodNewArr = [34, 45, ...arr]
console.log(goodNewArr)
```

函数参数传递展开运算符

```js
const arr = [1, 2, 3]

console.log(...arr)
// 相当于console.log(1,2,3)
```

字符串展开：

```js
const str = 'Akbar'
const strArr = [...str, ' ', 'A.']
console.log(strArr)
```

对象展开：

```js
const akbar = {
  name: 'akbar',
  age: 24,
}

const akbarClone = { ...akbar, location: 'hotan' }
console.log(akbarClone)
```

> 注意：对象展开语法遵循的是对象展开语法`{...object}`， 而不是迭代器协议。

**常见用途：**

1. shallow copy array：

```js
const arr = [1, 2, 3]

const newArr = [...arr]
console.log(newArr)
```

2. join two arrays or more

数组的 concat()方法也可以

```js
const arr1 = [1, 2, 3]
const arr2 = [45, 63, 89]

const newArr = [...arr1, ...arr2]
console.log(newArr)
```

# rest 语法

作用跟展开运算符正好相反。

```js
// 展开运算符，因为在等号（=）的
const arr = [1, 2, 3, ...[4, 5]]

// rest 语法，因为在等号（=）的左边
// 这里的others是一个数组，值是右边的3，4，5
const [a, b, ...others] = [1, 2, 3, 4, 5]
```

函数参数用法：

```js
function add(...numbers) {
  let sum = 0
  for (let i = 0; i < numbers.length; i++) sum += numbers[i]

  console.log(sum)
}

add(1, 2, 3, 4)
add(12, 67)
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

**上面代码中的问题：** `||`  会把  `0`  当成 “无效假值”，但实际场景中  `numGuests: 0`  是合法的（表示餐厅当前没有客人）；

**修正方案：** 用之前讲的  **空值赋值运算符  `??=`**，只对  `null`/`undefined`  赋值，保留  `0`  这类合法假值：

```js
// 修正后：仅当 numGuests 是 null/undefined 时，才赋值 10
rest1.numGuests ??= 10 // rest1.numGuests 仍为 0（正确保留）
rest2.numGuests ??= 10 // rest2.numGuests 赋值为 10（正确新增）
```

# Event 事件

- **Event 是事件对象**：封装了事件发生时的具体信息（类型、时间戳、目标元素等）
- **传递**：当事件被触发时，Event 对象会作为参数传递给事件处理函数

```js
// Event 对象会作为参数传递给事件处理函数
const openModal = function (event) {
  event.preventDefault()
  modal.classList.remove('hidden')
  overlay.classList.remove('hidden')
}
```

示例代码：

```js
document.addEventListener('keyup', function (event) {
  if (event.key === 'Escape' && !model.classList.contains('hidden')) closeModel()
})
```

> 上面的`event`就是事件参数。
> 当这个事件被触发的时候，JavaScript 把事件对象作为参数给这个函数传进去，注意，我们自己没有调用这个函数，因为我们只是在这里声明了以下，由 JavaScript 来调用，并且传我们要求的参数`event`。

## 常见的事件类型

| 事件类型     | 说明                                                            |
| ------------ | --------------------------------------------------------------- |
| `click`      | 鼠标点击事件                                                    |
| `mouseenter` | 鼠标进入事件                                                    |
| `mouseleave` | 鼠标离开事件                                                    |
| `keyup`      | 键盘按键释放事件                                                |
| `keydown`    | 键盘按键按下事件                                                |
| `input`      | 输入框内容变化事件                                               |
| `change`     | 输入框内容改变并失去焦点事件（可以用来监听 checkbox, radio 等）       |
| `blur`       | 元素失去焦点事件（可以用来对input进行校验）                          |
| `load`       | 页面或资源加载完成事件                                            |
| `submit`     | 表单提交事件(form 提交)                                         |
| `error`      | 发生错误时触发的事件                                             |

## 事件绑定

```js
const h1 = document.querySelector('h1')

// 第一种绑定事件的方法(推荐)
h1.addEventListener('mouseenter', function () {
  window.alert('Hello from h1, you hovered the h1 element')
})

// 第二种绑定事件的方法(不推荐, 老的写法)
h1.onmouseenter = function () {
  window.alert('Hello from h1, you hovered the h1 element')
}

// 比如点击事件(不推荐， 老的写法)
h1.onclick = function () {
  window.alert('Hello from h1, you hovered the h1 element')
}
```

## 如果想只执行一次事件处理函数

```js
const h1 = document.querySelector('h1')

// 第一种绑定事件的方法
const alertH1 = function () {
  window.alert('Hello from h1, you hovered the h1 element')

  // 移除事件监听器, 先执行上面的alert, 再移除监听器
  h1.removeEventListener('mouseenter', alertH1)
}

h1.addEventListener('mouseenter', alertH1)
```

也可以这样写：

```js
const h1 = document.querySelector('h1')

// 第一种绑定事件的方法
const alertH1 = function () {
  window.alert('Hello from h1, you hovered the h1 element')
}

h1.addEventListener('mouseenter', alertH1)
window.setTimeout(() => h1.removeEventListener('mouseenter', alertH1), 3000)
```

## 事件冒泡

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251205105421125.png)

事件冒泡（Event Bubbling）是指当一个事件被触发时，它会从最具体的元素（事件目标）开始，逐级向上传播到其父元素，直到到达最顶层的 DOM 树。

事件冒泡有三个阶段：

1. 捕获阶段（Capturing Phase）：事件从根节点向下传播到目标元素的路径上。
2. 目标阶段（Target Phase）：事件到达目标元素并触发事件处理程序。
3. 冒泡阶段（Bubbling Phase）：事件从目标元素向上传播回根节点的路径上。

默认情况下，事件处理程序会在冒泡阶段被调用。
如果想在捕获阶段处理事件，可以在添加事件监听器时传递第三个参数`true`。

html 解构：
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251205133219889.png)

**示例代码**：

```js
const randomInt = (min, max) => Math.trunc(Math.random() * (max - min + 1) + min)

const randomColor = () => `rgb(${randomInt(0, 255)}, ${randomInt(0, 255)}, ${randomInt(0, 255)})`

document.querySelector('.nav__link').addEventListener('click', function (e) {
  // this 指向当前绑定事件的元素
  this.style.backgroundColor = randomColor()
  console.log('LINK', e.target, e.currentTarget)
  // e.currentTarget 指向当前绑定事件的元素
  // e.target 指向实际触发事件的元素
  console.log(this === e.currentTarget) // true
})

document.querySelector('.nav__links').addEventListener('click', function (e) {
  this.style.backgroundColor = randomColor()
  console.log('CONTAINER', e.target, e.currentTarget)
})

document.querySelector('.nav').addEventListener('click', function (e) {
  this.style.backgroundColor = randomColor()
  console.log('NAV', e.target, e.currentTarget)
})
```

**怎么阻止事件冒泡**：

{% codeblock lang:javascript mark:13,14 %}
const randomInt = (min, max) => Math.trunc(Math.random() \* (max - min + 1) + min);

const randomColor = () => `rgb(${randomInt(0, 255)}, ${randomInt(0, 255)}, ${randomInt(0, 255)})`;

document.querySelector('.nav\_\_link').addEventListener('click', function (e) {
// this 指向当前绑定事件的元素
this.style.backgroundColor = randomColor();
console.log('LINK', e.target, e.currentTarget);
// e.currentTarget 指向当前绑定事件的元素
// e.target 指向实际触发事件的元素
console.log(this === e.currentTarget); // true

// 阻止事件冒泡, 阻止事件传播到更外层的元素
e.stopPropagation();
});

document.querySelector('.nav\_\_links').addEventListener('click', function (e) {
this.style.backgroundColor = randomColor();
console.log('CONTAINER', e.target, e.currentTarget);
});

document.querySelector('.nav').addEventListener('click', function (e) {
this.style.backgroundColor = randomColor();
console.log('NAV', e.target, e.currentTarget);
});
{% endcodeblock %}

## 事件委托

事件委托（Event Delegation）是一种常用的事件处理模式，通过将事件监听器添加到父元素上，而不是每个子元素上，从而利用事件冒泡机制来处理子元素的事件。

**原理**：
浏览器在执行事件时，默认会先在最具体的目标元素上触发（target 阶段），然后事件会沿着 DOM 树向上冒泡，经过每个祖先元素，直到根节点。因此在父元素上注册点击监听器，会接收到子元素触发并冒泡上来的事件。

示例代码：

html 解构：

```html
<ul class="nav__links">
  <li class="nav__item">
    <a class="nav__link" href="#section--1">Features</a>
  </li>
  <li class="nav__item">
    <a class="nav__link" href="#section--2">Operations</a>
  </li>
  <li class="nav__item">
    <a class="nav__link" href="#section--3">Testimonials</a>
  </li>
  <li class="nav__item">
    <a class="nav__link nav__link--btn btn--show-modal" href="#">Open account</a>
  </li>
</ul>

<!--  要跳转的section是这样的 -->
<section class="section" id="section--1"></section>
<section class="section" id="section--2"></section>
```

我们的目标是点击导航栏的链接时，页面平滑滚动到对应的 section。

```js
// 效率较低的做法
// document.querySelectorAll('.nav__link').forEach(function (el) {
//   el.addEventListener('click', function (event) {
//     event.preventDefault();                // 阻止a标签的默认跳转行为
//     const id = this.getAttribute('href');  // 获取链接的目标id(相对路径， 如 #section--1)
//     document.querySelector(id).scrollIntoView({ behavior: 'smooth' });
//   });
// });

// 高效的做法： 事件委托
// 1. 在共同的父元素上添加事件监听器
// 2. 利用事件对象event，确定事件的目标元素
/**
 * 原理：
 * 浏览器在执行事件时，默认会先在最具体的目标元素上触发（target 阶段），
 * 然后事件会沿着 DOM 树向上冒泡，经过每个祖先元素，直到根节点。
 * 因此在父元素上注册点击监听器，会接收到子元素触发并冒泡上来的事件。
 */
document.querySelector('.nav__links').addEventListener('click', function (event) {
  event.preventDefault()

  if (event.target.classList.contains('nav__link') && event.target.getAttribute('href') !== '#') {
    const id = event.target.getAttribute('href')
    document.querySelector(id).scrollIntoView({ behavior: 'smooth' })
  }
})
```

# window

`window`：浏览器中的全局对象（全局作用域的根）。

它代表浏览器窗口或标签页，包含控制窗口/浏览器行为的 API（计时器、地址栏、历史、对话框、localStorage 等）。

可以把它理解为“浏览器环境”的接口集合。

<mark>因为是全局对象，所以在全局作用域中可以直接访问其属性和方法，而不需要显式引用 window。</mark>

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Window',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

## windwo.location

获取/设置 window 对象的位置，或当前的 URL。

> `window.location` **引用本身只读**（不能改成指向新对象）<br/>

`window.location`和`Location`是什么关系？

| 名称                  | 类型                                | 作用                              |
| --------------------- | ----------------------------------- | --------------------------------- |
| **`window.location`** | **属性** (指向一个 `Location` 实例) | 当前窗口的 URL 信息对象           |
| **`Location`**        | **内置对象类（接口）**              | 定义用于处理 URL 的各种属性和方法 |

```js
class Location {...}         // 「类型」或「构造说明」
window.location = new Location // 浏览器内部创建好并挂载到 window 上
```

你无法 new Location，但浏览器已经替你创建好，并挂在 `window.location` 上供你使用。

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Window/location',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

### 属性

常用的属性：

```js
location.href // 整个URL
location.protocol // http:
location.host // wwww.xx.com:80
location.hostname // 主机名
location.port // 端口
location.pathname // 路径
location.search // ?a=1&b=2
location.hash // #部分
```

### 方法

| 方法                    | 用途                   |
| ----------------------- | ---------------------- |
| `location.assign(url)`  | 跳转到新页面（可返回） |
| `location.replace(url)` | 跳转但无法后退         |
| `location.reload()`     | 刷新页面               |

## window.console

> 注意：<br/> > `console` 确实挂在 `window` 上，但它不是 `Window.prototype` 上定义的属性。<br/>
> 它是浏览器提供的 **全局对象**，并在运行环境中被放到 `window` 下以便访问。

```js
console.log(Window.prototype.hasOwnProperty('console')) // false
console.log('console' in window) // true
```

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Console_API',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

### 常用的实例方法

1.**console.log**：向 Web 控制台输出一条信息

2.**console.error**：向 Web 控制台输出一条错误消息。

3.**console.table**：将数据以表格的形式显示。

4.**console.warn**：向 Web 控制台输出一条警告信息。

## window.document

document：window 的一个属性（window.document）

表示当前网页的 DOM（Document Object Model）—— HTML 的节点树，是操作页面内容、结构、样式的主要对象。

通过 document 对象，可以访问和修改网页中的元素，实现动态交互效果。

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251204103412659.png)

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251204103720348.png)

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251204104530487.png)

```js
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

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Document',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

### 选择元素

1. **document.documentElement**：获取根元素（如`<html>`）

```js
// 4.获取根元素
const rootElement = document.documentElement // entire HTML document
```

2. **document.title**：获取网页标题。

```js
const title = document.title // <head> element of the document
console.log(`Page title: ${title}`)
```

3. **document.body**：获取 body 元素

```js
console.log(document.body) // <body> element of the document
```

4. **document.querySelector**：返回文档中与指定选择器匹配的第一个`Element`对象。

```js
const header = document.querySelector('.header') // first element with class 'header'
```

5. **document.querySelectorAll**：返回与指定的选择器组匹配的文档中的元素列表，返回的对象是 NodeList。

> NodeList 对象是节点的集合。
> NodeList 不是一个数组，是一个类似数组的对象 (Like Array Object)。虽然 NodeList 不是一个数组，但是可以使用 forEach() 来迭代。

6. **getElementById()**：返回一个表示`id`属性与指定字符串相匹配的元素的`Element`对象。(updated live)

7. **document.getElementsByClassName()**：返回一个包含了所有指定类名的子元素的类数组对象。(updated live)

8. **document.getElementsByTagName**：根据元素的标签名选择。(updated live)

### 创建元素

1. **document.createElement**：create a new element, and return it

```js
const message = document.createElement('div') // create a new <div> element, and return it
```

2. **设置文本：`textContent`**

不仅可以读取元素的文本，还可以设置文本。

> `<input>`、`<textarea>` 等 可输入元素的内容并不是一个文本节点，而是存储在它们的 value 属性中。
> 为什么呢？
> 因为 `<input>` 标签是自闭合的，没有内部文本节点：

```js
const message = document.createElement('div') // create a new <div> element, and return it
message.textContent = 'We use cookies for improved functionality and analytics.'
```

3. `innerHTML`：设置或获取 HTML 语法表示的元素的后代。

```js
const message = document.createElement('div')
message.innerHTML =
  'We use cookies for improved functionality and analytics. <button class="btn btn--close-cookie">Got it!</button>'
```

4. **value**: current value of the [`<input>`] element as a string.

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLInputElement',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

比如：

```js
document.querySelector('input').value = 'Hello' // 正确 ✔
document.querySelector('input').textContent = 'Hello' // 无效 ❌
```

```js
<input type="text" />   <!-- 没有像 <p>xxx</p> 那样的内容节点 -->
```

### 插入元素

1. **prepend**：作为第一个元素插入

```js
// 作为第一个子元素插入到header中
header.prepend(message)
```

2. **append**：作为最后一个子元素插入

```js
// 作为最后一个子元素插入到header中
header.append(message)
```

{% note primary modern %}
需要注意的是：  
如果一个元素已经存在于页面中，调用 prepend 或 append 会将其从原来的位置移动到新的位置，而不是再插入一个新的元素。
{% endnote %}

3. **cloneNode**：插入相同的多个元素

```js
// 如果想在header中插入多个相同的元素，可以使用cloneNode方法
header.append(message.cloneNode(true)) // 深度克隆，包括子元素
```

4. **before**：插入到该元素之前

```js
// 将message插入到header之前
header.before(message)
```

5. **after**：插入到该元素之后。

```js
// 将message插入到header之后
header.after(message)
```

6. `insertAdjacentHTML()`：将指定的文本解析为  `Element`元素，并将结果节点插入到 DOM 树中的指定位置。

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Element/insertAdjacentHTML',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

7. **appendChild()**： 将一个节点添加到指定父节点的子节点列表的末尾。

### 删除元素

1. **remove**：自己删除自己

```js
// 删除元素
document.querySelector('.btn--close-cookie').addEventListener('click', function () {
  message.remove()
})
```

2. **removeChild**：让父元素去删除

```js
// 删除元素
document.querySelector('.btn--close-cookie').addEventListener('click', function () {
  message.parentElement.removeChild(message)
})
```

### 行内样式 Styles

格式：`element.style.[具体属性]`

> 不仅可以设置行内样式，还可以读取行内样式。

```js
const message = document.createElement('div')

// 设置行内样式
message.style.backgroundColor = '#37383d'
message.style.width = '120%'

// 只能获取内联样式，如果不存在这个行内样式，则返回空字符串
console.log(message.style.backgroundColor)
console.log(message.style.width)
```

如果想获取 css 选择器设置的样式，怎么办？

```js
// 如果想获取通过css选择器设置的样式，需要使用getComputedStyle
console.log(getComputedStyle(message).color)
console.log(getComputedStyle(message).height)
```

### 控制 css variables

```js
document.documentElement.style.setProperty('--color-primary', 'orangered');

// 相当于
:root {
  --color-primary: orangered;
}
```

### Attributes

> src, alt, class, id 等等都是 Attributes。
> 这些属性都可以读，也可以写。

比如：

```html
        <img
          src="img/logo.png"
          alt="Bankist logo"
          class="nav__logo"
          id="logo"
          designer="akbar"            自定义属性
          data-version-number="3.0"   data attributes
        />

          <a class="nav__link nav__link--btn btn--show-modal" href="#">
             Open account
          </a
```

```js
// Attributes
const logo = document.querySelector('.nav__logo')
console.log(logo.alt)
console.log(logo.className)
console.log(logo.src) // 绝对路径
console.log(logo.getAttribute('src')) // 相对路径
console.log(logo.getAttribute('designer')) // 自定义属性
logo.setAttribute('company', 'Bankist') // 设置自定义属性
console.log(logo.getAttribute('company'))
console.log(logo.dataset.versionNumber) // 访问data-version-number属性

const link = document.querySelector('.nav__link--btn')
console.log(link.href) // 绝对路径
console.log(link.getAttribute('href')) // 相对路径
```

### 类名 Class

```html
<img
  src="img/logo.png"
  alt="Bankist logo"
  class="nav__logo"
  id="logo"
  designer="akbar"
  自定义属性
  data-version-number="3.0"
  data
  attributes
/>
```

```js
const logo = document.querySelector('.nav__logo')

logo.className = 'jonas' // 不推荐， 会覆盖掉所有的类

logo.classList.add('class1', 'class2')
logo.classList.remove('class1')
logo.classList.toggle('class2') // 如果存在则删除，否则添加
logo.classList.contains('class2') // true
```

### getBoundingClientRect()

其提供了元素的大小及其相对于视口的位置。
这里的 Rect 是 Rectangle 的意思。

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

### clientWidth 和 clientHeight

返回元素的可见宽高（内容 + 内边距，不包括边框、滚动条、外边距）。

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Element/clientWidth',
'MDN ClientWidth 文档',
far fa-hand-point-right,blue larger
%}

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Element/clientHeight',
'MDN ClientHeight 文档',
far fa-hand-point-right,blue larger
%}

### focus()元素聚焦

input 元素获取焦点

```js
const inputDistance = document.querySelector('.form__input--distance')

inputDistance.focus()
```

## window.innerWidth

获取浏览器窗口的宽高。

## window.innerHeight

获取浏览器窗口的内容区域的高度，包括（已渲染的）水平滚动条。

## window.localStorage

{% note warning flat %}
**注意**
localstorage 操作会阻塞主线程，尤其是在存储大量数据时。
{% endnote %}

### 实例方法

1.**localStorage.setItem()**：往 localStorage 存储数据，如果键名已存在，则更新其对应的值。

```js
// 格式
window.localStorage.setItem(keyName, keyValue)

// 比如
window.localStorage.setItem('myCat', 'Tom')
```

2. **localStorage.getItem()**：返回该键的值；而如果不存在该键，则返回  `null`。

```js
let cat = window.localStorage.getItem('myCat')
```

3. **localStorage.removeItem()**：当传递一个键名时，删除该键（如果它存在）。

```js
window.localStorage.removeItem('myCat')
```

4. **localStorage.clear()**：清除所有数据。

```js
// 移除所有
localStorage.clear()
```

## window.alert()

弹出对话框。

## window.confirm()

确认对话框。

## window.prompt()

提示输入对话框。

## window.setInterval()

重复调用一个函数或执行一个代码片段，在每次调用之间具有固定的时间间隔。

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setInterval',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

```js
const startLogoutTimer = function () {
  // Set time to 5 minutes
  let time = 10

  // Call the timer every second
  const myTimer = setInterval(function () {
    const min = String(Math.trunc(time / 60)).padStart(2, '0')
    const sec = String(time % 60).padStart(2, '0')

    //in each call , print the remaining time to console
    console.log(`${min}:${sec}`)

    // when 0 seconds, stop timer and logout user
    if (time === 0) {
      clearInterval(myTimer)
      console.log('Log out!')
    }

    // decrease 1s
    time--
  }, 1000)
}

startLogoutTimer()
```

## window.clearInterval()

window.setInterval()返回的值可以用来传递给  `clearInterval()`来清除定时器。

## window.setTimeout()

设置一个定时器，一旦定时器到期，就会执行一个函数或指定的代码片段。

定时器属于宏任务。

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

示例代码：

```js
window.setTimeout(
  () => console.log('Here is your pizza'),
  3000, // 3秒之后执行callback函数
)

console.log('Waiting...')
```

> JavaScript 一旦看到 setTimeout，就知道这是一个延迟执行的代码，背后开启一个计时器，紧接着继续执行下面的代码，一旦背后的计时器的时间到了，比如`3000`毫秒，就回头执行`setTimeout`中的代码。

完整写法：

```js
window.setTimeout(
  (ing1, ing2) => console.log(`Here is your ${ing1} and ${ing2}`),
  3000,
  'Pizza 🍕',
  'Pasta 🍝',
)
```

```js
'Pizza 🍕', 'Pasta 🍝'
```

给 callback 函数传递参数，对应 ing1，ing2

## window.clearTimeout()

可以将 window.setTimeout()返回的值传递给  `clearTimeout()`来取消该定时器。

```js
const myTimer = window.setTimeout(() => console.log(`Here is your ${ing1} and ${ing2}`), 3000)

// 3000毫秒到达之前取消定时器
window.clearTimeout(myTimer)
```

## window.scrollTo()

滚动窗口到指定位置

参数：

- x-coord：水平像素值
- y-coord：垂直像素值
- behavior（可选）：滚动行为，`'auto'`（默认）或`'smooth'`

{% note warning flat %}
**注意**
x-coord 和 y-coord 是相对于文档左上角的坐标，而不是相对于当前视口的位置。
{% endnote %}

示例代码：

```js
// Scrolling
const btnScrollTo = document.querySelector('.btn--scroll-to')
const section1 = document.querySelector('#section--1')

btnScrollTo.addEventListener('click', function () {
  const s1coords = section1.getBoundingClientRect()
  // 相对于视口的信息
  console.log(s1coords)

  window.scrollTo({
    left: s1coords.left + window.scrollX,
    top: s1coords.top + window.scrollY,
    behavior: 'smooth',
  })
})
```

但是还有更简单的方法 😁，推荐使用`scrollIntoView()`方法。

```js
// Scrolling
const btnScrollTo = document.querySelector('.btn--scroll-to')
const section1 = document.querySelector('#section--1')

btnScrollTo.addEventListener('click', function () {
  section1.scrollIntoView({ behavior: 'smooth' })
})
```

## window.scrollX 和 window.scrollY

返回文档在水平方向和垂直方向已滚动的像素值。

{% note warning flat %}
**注意**
scrollX 和 scrollY 返回的是相对于文档左上角的坐标，而不是相对于当前视口的位置。
{% endnote %}

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Window/scrollX',
'MDN ScrollX 文档',
far fa-hand-point-right,blue larger
%}

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/API/Window/scrollY',
'MDN ScrollY 文档',
far fa-hand-point-right,blue larger
%}

## window.navigator

可以用于请求运行当前代码的应用程序的相关信息。

1. **navigator.geolocation.getCurrentPosition()**：获取用户的当前位置。

语法：

```js
getCurrentPosition(success) // success 回调函数
getCurrentPosition(success, error) // success 是成功回调， error 是失败回调
getCurrentPosition(success, error, options) // options 可选参数
```

# 为什么说 JavaScript 不是纯解释型语言？

> 现代 JS 引擎早已不是单纯逐行解释执行，而是结合了解释执行 + 编译执行 + 多段优化机制。

现代 v8 引擎等的运行流程是这样的：

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
  return a + b
}

for (let i = 0; i < 1e9; i++) {
  add(1, 2)
}
```

V8 会做两件事：

1.  先解释执行（启动快）
1.  发现执行频繁后 → **JIT 编译，并优化成机器码（提速）**

纯解释型语言不会做第 2 步，因此**现代 JS 就不是纯解释型语言了**。

# `执行上下文` 和 `作用域链`

{% btn
'https://juejin.cn/post/7486429532720349199',
'掘金文档',
far fa-hand-point-right,blue larger
%}

# Math

## Math.trunc()

该静态方法通过删除任何小数位来返回数字的整数部分。

比如：

```js
console.log(Math.trunc(13.37)) // 输出 13
```

## Math.floor()

向下取整，返回小于或等于给定数字的最大整数。

比如：

```js
console.log(Math.floor(13.37)) // 输出 13
console.log(Math.floor(13.99)) // 输出 13
console.log(Math.floor(-13.37)) // 输出 -14
```

## Math.ceil()

向上取整，返回大于或等于给定数字的最小整数。

比如：

```js
console.log(Math.ceil(13.37)) // 输出 14
console.log(Math.ceil(13.01)) // 输出 14
console.log(Math.ceil(-13.37)) // 输出 -13
```

## Math.round()

四舍五入，返回最接近的整数。

比如：

```js
console.log(Math.round(13.37)) // 输出 13
console.log(Math.round(13.5)) // 输出 14
console.log(Math.round(-13.37)) // 输出 -13
console.log(Math.round(-13.5)) // 输出 -13
```

```js
// 求平方根
console.log(Math.sqrt(25)) // 输出 5
console.log(25 ** (1 / 2)) // 输出 5

// 求最大值
console.log(Math.max(5, 18, 23, 11, 2)) // 输出 23

// 求最小值
console.log(Math.min(5, 18, 23, 11, 2)) // 输出 2

// 计算圆周率
console.log(Math.PI)

// Random number
console.log(Math.random()) // 输出 0 到 1 之间的随机数
console.log(Math.random() * 6) // 输出 0 到 6 之间的随机数，但不包括 6
console.log(Math.trunc(Math.random() * 6) + 1) // 去除小数部分，输出 1 到 6 之间的随机整数，包括 1 和 6

// 编写一个生成指定范围内随机整数的函数
/**
 * 比如：10 到 20
 * max - min + 1 => 11，0 到 11(不包括) 之间
 * 再加上min(10) => 10 到 20 之间
 */
const randomInt = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min

console.log(randomInt(10, 20))

// Rounding integers(取整)
console.log(Math.trunc(23.3)) // 输出 23，去除小数部分

// 四舍五入取整
console.log(Math.round(23.3)) // 输出 23
console.log(Math.round(23.9)) // 输出 24

// 向上取整
console.log(Math.ceil(23.3)) // 输出 24
console.log(Math.ceil(23.9)) // 输出 24

// 向下取整
console.log(Math.floor(23.3)) // 输出 23
console.log(Math.floor(23.9)) // 输出 23

// 小数点后取整
console.log((2.7).toFixed(0)) // 输出 '3'，四舍五入取整，返回字符串
console.log((2.7).toFixed(3))
```

# Numeric Separators

```js
// Numeric Separators(大数字分隔符)
const diameter = 287_460_000_000
console.log(diameter)
```

# Dates and Times，国际化

```js
// create a dates
const now = new Date()
console.log(now)

// parsing date from string
console.log(new Date('Aug 02 2023 18:05:41'))
console.log(new Date('December 24, 2015'))
console.log(new Date('2019-11-18T21:31:17.178Z'))

// Date常用的方法
const myTime = new Date(`2019-11-18T21:31:17.178Z`)
console.log(myTime.getFullYear())
console.log(myTime.getMonth())
console.log(myTime.getDate()) // 获取当前月的第几天
console.log(myTime.getDay()) // 获取星期几
console.log(myTime.getMinutes())
console.log(myTime.getSeconds())
console.log(myTime.toISOString()) // 转化为标准时间格式
console.log(myTime.getTime()) // 转化为时间戳
console.log(Date.now()) // 当前时间戳
```

## Internationalizing 时间国际化

```js
const options = {
  hour: 'numeric',
  minute: 'numeric',
  day: 'numeric',
  month: 'numeric',
  year: 'numeric',
}
console.log(new Intl.DateTimeFormat('zh-CN', options).format(now))
```

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat',
具体细节,
far fa-hand-point-right,blue larger
%}

## 数字国际化

```js
const num = 3884764.23
const optionsForNum = {
  style: 'unit',
  unit: 'mile-per-hour',
}
console.log('China:', new Intl.NumberFormat('zh-CN', optionsForNum).format(num))
```

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat',
具体细节,
far fa-hand-point-right,blue larger
%}

# this 关键字

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251202210422015.png)

- 对象方法：`this` 指向调用该方法的对象。
- 普通函数：`this` 指向全局对象（浏览器中是 `window`，严格模式下是 `undefined`）。
- 构造函数：`this` 指向新创建的实例对象。
- 箭头函数：`this` 继承自外层作用域。
- 事件处理器：`this` 指向触发事件的 DOM 元素。

## function.call()方法

{% btn
'https://www.bilibili.com/video/BV1vA4y197C7?spm_id_from=333.788.videopod.episodes&vd_source=28e37be50df53ebbf04edfcc6228018f&p=124',
'B站视频',
far fa-hand-point-right,blue larger
%}

{% btn
'https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call',
'MDN 文档',
far fa-hand-point-right,blue larger
%}

## function.bind()方法

`function.bind()` 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为传入的第一个参数。

比如：

```js
const person = {
  firstName: 'Akbar',
  greet: function () {
    console.log(`Hello, my name is ${this.firstName}`)
  },
}

const akbar = person.greet
akbar() // 输出: Hello, my name is undefined

// 使用 bind 方法将 this 绑定到 person 对象
const boundGreet = akbar.bind(person)
boundGreet() // 输出: Hello, my name is Akbar
```

比如 vue3 中使用

{% codeblock lang:typescript mark:12 %}
const app = Vue.createApp({

data() {
  return {
    counter: 0,
  }
},

watch: {
  counter(value) {
    if (value > 50) {
      window.setTimeout(function () { // // this 原本指向的是 window 对象
      this.counter = 0
      }.bind(this), 2000) // 通过 bind 将 this 绑定到 Vue 实例
    }
  },
},
{%endcodeblock%}

# 面向对象

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251205154030603.png)

**面向对象的几个元素**：

- 抽象（Abstraction）
- 封装（Encapsulation）
- 继承（Inheritance）
- 多态（Polymorphism）

## JavaScript 中的面向对象

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251205155904569.png)

**JavaScript 中如何创建`prototype`**？

- 使用构造函数（Constructor Functions）
- 使用`Object.create()`
- 使用 ES6 的`class`语法糖：背后还是基于原型的继承机制、构造函数创建。

## 构造函数

> 构造函数和其它函数没什么不一样的，但是构造函数我们可以使用`new`关键字来调用它。
> 不要用`箭头函数`来定义构造函数，因为箭头函数没有自己的`this`。

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251205171531632.png)

**原型链：**
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251205172131457.png)

```js
const Person = function (firstName, birthYear) {
  // Instance properties, available on all instances
  this.firstName = firstName
  this.birthYear = birthYear
}

const akbar = new Person('Akbar', 2001)
```

构造流程（当你执行 `new Person(...)` 时）：

- 创建一个空对象 `{}`。
- 将函数 `Person` 内的 `this` 绑定到这个新对象。
- 新对象会被自动链接到构造函数的 `prototype`（即新对象的 `__proto__` 指向 `Person.prototype`）。
- 函数执行完毕后，默认返回这个新对象。

---

```js
const Person = function (firstName, birthYear) {
  // Instance properties, available on all instances
  this.firstName = firstName
  this.birthYear = birthYear
}

const akbar = new Person('Akbar', 2001)

console.log(akbar instanceof Person)
```

**`instanceof`**：

- `akbar instanceof Person` → true，因为 `Person.prototype` 在 `akbar` 的原型链上。`akbar.__proto__ === Person.prototype`。

---

```js
const Person = function (firstName, birthYear) {
  // Instance properties, available on all instances
  this.firstName = firstName
  this.birthYear = birthYear

  // Never create methods inside constructor functions
  // because it will create a new copy of the method for every object
  // this.calcAge = function() {
  //   console.log(2025 - this.birthYear);
  // }
}

// 要这样写
Person.prototype.calcAge = function () {
  console.log(2025 - this.birthYear)
}

// 调用calcAge方法
akbar.calcAge()
```

**最佳实践小结**：

- 不要在构造函数内部为每个实例创建方法（会造成每个实例持有独立函数）。
- 需要共享行为时，把方法放到 `Constructor.prototype` 或者使用 ES6 `class`（本质上仍是基于原型）。
- 如果要创建没有原型链的对象、或做更细的继承控制，可考虑 `Object.create()`。

---

```js
const Person = function (firstName, birthYear) {
  this.firstName = firstName
  this.birthYear = birthYear
}

Person.prototype.species = 'Homo Sapiens'

console.log(akbar.hasOwnProperty('firstName'))
console.log(akbar.hasOwnProperty('species'))
```

**`hasOwnProperty` vs 继承属性`**：

- `akbar.hasOwnProperty('firstName')` 为 `true`（实例自身的属性）。
- `akbar.hasOwnProperty('species')` 为 `false`，因为 `species` 在原型上，是继承来的。

**原型链查找**：

- 当你访问 `akbar.calcAge()` 时，JavaScript 先在 akbar 对象自身查找；找不到就沿着 `__proto__`（即 `Person.prototype`）查找；找到则调用。

### 有趣的示例代码

> 我想扩展 Array.prototype

```js
const arr = [1, 1, 1, 3, 3, 3, 4, 4, 5]

Array.prototype.unique = function () {
  return [...new Set(this)]
}

console.log(arr.unique()) // 输出：[1, 3, 4, 5]
```

{% note warning modern %}
**提示**
但是不推荐这么做。
{% endnote %}

### 挑战

1. Use a constructor function to implement a Car. A car has a make and a speed property. The speed property is the current speed of the car in km/h;
2. Implement an 'accelerate' method that will increase the car's speed by 10, and log the new speed to the console;
3. Implement a 'brake' method that will decrease the car's speed by 5, and log the new speed to the console;
4. Create 2 car objects and experiment with calling 'accelerate' and 'brake' multiple times on each of them.

DATA CAR 1: 'BMW' going at 120 km/h
DATA CAR 2: 'Mercedes' going at 95 km/h

GOOD LUCK 😀

```js
const Car = function (make, speed) {
  this.make = make
  this.speed = speed
}

Car.prototype.accelerate = function () {
  this.speed += 10
  console.log(`${this.make} is going at ${this.speed} km/h`)
}

Car.prototype.brake = function () {
  this.speed -= 5
  console.log(`${this.make} is going at ${this.speed} km/h`)
}

const bmw = new Car('BMW', 120)
const mercedes = new Car('Mercedes', 95)

bmw.accelerate()
bmw.brake()

mercedes.accelerate()
mercedes.brake()
```

## ES6 Classes

> class 其实一种特殊的函数，是构造函数的语法糖。

有两种定义 class 的方式：

```js
// class expression
const Animal = class {}

// class declaration
class Person {}
```

示例代码：

```js
class Person {
  constructor(firstName, birthYear) {
    this.firstName = firstName
    this.birthYear = birthYear
  }

  calcAge() {
    console.log(2025 - this.birthYear)
  }
}

const akbar = new Person('Akbar', 2001)

console.log(akbar)
akbar.calcAge()

console.log(akbar instanceof Person)
console.log(akbar.__proto__ === Person.prototype)

// 手动添加方法
Person.prototype.greet = function () {
  console.log(`Hello, my name is ${this.firstName}`)
}
akbar.greet()
```

### 注意事项

1. Class 没有提升（hoisting），必须在声明后才能使用。
2. Class 是一等公民，因为它是一种特殊的函数。
3. Class 内部遵循严格模式（'use strict'）。

## Setters 和 Getters

getter 和 setter 是 JavaScript 类中用于访问和修改对象属性的特殊方法，它们让你能够更好地控制属性的读写操作。

比如：

```js
const account = {
  owner: 'akbar',
  movements: [200, 450, -400, 3000, -650, -130, 70, 1300],

  get latest() {
    return this.movements.slice(-1)[0]
  },

  set latest(mov) {
    this.movements.push(mov)
  },
}

// 使用 getter
console.log(account.latest)
// 使用 setter
account.latest = 50
console.log(account.movements)
```

**class 也可以使用 getter 和 setter**：

```js
class Person {
  constructor(name, age) {
    this._name = name // 使用下划线表示私有属性
    this._age = age
  }

  // getter方法
  get name() {
    return this._name
  }

  get age() {
    return this._age
  }

  // setter方法
  set name(newName) {
    if (newName.length > 0) {
      this._name = newName
    }
  }

  set age(newAge) {
    if (newAge >= 0 && newAge <= 150) {
      this._age = newAge
    }
  }
}

const person = new Person('张三', 25)
console.log(person.name) // 使用getter，输出: 张三
person.name = '李四' // 使用setter
console.log(person.name) // 输出: 李四
```

## Static

static 关键字用于定义类的静态方法或静态属性，它们属于类本身而不是类的实例。

比如：`Array.from()`, `Number.parseInt()`等。只能通过类本身调用，不能通过实例调用，因为这些属性和方法只属于类，而不是属于示例。

```js
class Person {
  constructor(name, age) {
    this._name = name
    this._age = age
  }

  // getter方法
  get name() {
    return this._name
  }

  get age() {
    return this._age
  }

  // setter方法
  set name(newName) {
    if (newName.length > 0) {
      this._name = newName
    }
  }

  set age(newAge) {
    if (newAge >= 0 && newAge <= 150) {
      this._age = newAge
    }
  }
}

// 创建静态方法
Person.hey = function () {
  console.log('Hey there!')
  console.log(this) // 指向Person类本身, 因为Person调用这个方法
}

const person = new Person('张三', 25)

console.log(person.hey) // undefined
Person.hey() // Hey there!
```

## Object.create()

`Object.create()`方法创建一个新对象，使用现有的对象来提供新创建的对象的`__proto__`。

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251205204715659.png)

比如：

```js
const PersonProto = {
  // 初始化方法, 相当于类的构造函数
  init(firstName, birthYear) {
    this.firstName = firstName
    this.birthYear = birthYear
  },

  calcAge() {
    // 这里的 this 指向调用该方法的对象
    console.log(2025 - this.birthYear)
  },
}

const akbar = Object.create(PersonProto)

akbar.init('Akbar', 1998)
akbar.calcAge()
console.log(akbar)

console.log(akbar.__proto__ === PersonProto) // true
```

## 继承

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251206105621598.png)

### 通过构造函数实现继承

```js
const Person = function (firstName, birthYear) {
  this.firstName = firstName
  this.birthYear = birthYear
}

Person.prototype.calcAge = function () {
  console.log(2025 - this.birthYear)
}

const Student = function (firstName, birthYear, course) {
  Person.call(this, firstName, birthYear)
  this.course = course
}

// Linking prototypes
// 注意顺序：必须在定义 Student.prototype.introduce 之前
Student.prototype = Object.create(Person.prototype)

Student.prototype.introduce = function () {
  console.log(`My name is ${this.firstName} and I study ${this.course}`)
}

// Correct the constructor pointer because it points to Person
Student.prototype.constructor = Student

const mike = new Student('Mike', 2020, 'Computer Science')
console.log(mike)
mike.introduce()
mike.calcAge()
```

### 通过 ES6 class 实现继承

```js
class Person {
  constructor(fullName, birthYear) {
    this.name = fullName
    this.birthYear = birthYear
  }

  calcAge() {
    const age = 2025 - this.birthYear
    console.log(`${this.name} is ${age} years old.`)
  }
}

class Student extends Person {
  constructor(fullName, birthYear, course) {
    // Call the parent class constructor
    super(fullName, birthYear)
    this.course = course
  }

  // 重写calcAge方法
  calcAge() {
    const age = 2025 - this.birthYear
    console.log(`${this.name} is ${age} years old., and is studying ${this.course}.`)
  }

  introduce() {
    console.log(`My name is ${this.name} and I study ${this.course}.`)
  }
}

const student1 = new Student('Alice Johnson', 2000, 'Computer Science')
student1.introduce()
student1.calcAge()
```

## 最后总结

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251206153513853.png)

# `JSON` 命名空间

{% note primary modern %}
`JSON` 命名空间包含用于解析和生成 JSON 数据的功能。
{% endnote %}

## JSON.parse()

将 JSON 字符串转换为 JavaScript 对象。

```js
const jsonString = '{"name": "Akbar", "age": 24, "isStudent": false}'
const jsonObj = JSON.parse(jsonString)
console.log(jsonObj)
```

## JSON.stringify()

将 JavaScript 对象转换为 JSON 字符串。

```js
const jsonObj = { name: 'Akbar', age: 24, isStudent: false }
const jsonString = JSON.stringify(jsonObj)
console.log(jsonString)
```

# Object 命名空间

{% note primary modern %}
`Object`是 JavaScript 的引用数据类型。
`Object` 命名空间包含用于操作对象的各种方法和属性。
{% endnote %}

## Object.keys()

返回一个包含对象所有可枚举属性名称的数组。

```js
const obj = { name: 'Akbar', age: 24, isStudent: false }
const keys = Object.keys(obj)
console.log(keys)

// 输出： ['name', 'age', 'isStudent']
```

# Asynchronous JavaScript

## 什么是 Synchronous JavaScript？

同步 JavaScript 是指代码按顺序执行，一行接一行，直到所有代码执行完毕。在同步执行中，后续代码必须等待前面的代码执行完成后才能继续执行。这种方式简单直观，但在处理耗时操作（如网络请求、文件读取等）时，可能会导致阻塞，影响用户体验。

比如看下面的代码：

```diff
const p = document.querySelector('p');
p.textContent = 'Hello World!';
- alert('This is an alert box!'); // 这里会阻塞后续代码的执行，直到用户关闭弹窗
p.style.color = 'red';
```

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251208143704074.png)

## 什么是 Asynchronous JavaScript？

异步 JavaScript 是指代码可以在不阻塞主线程的情况下执行。异步操作允许程序在等待某些任务完成（如网络请求、定时器等）时，继续执行其他代码，从而提高应用的响应性和性能。异步编程通常使用回调函数、Promises 或 async/await 来处理异步操作的结果。

比如看下面的代码：

```diff
const p = document.querySelector('p');
+ setTimeout(() => {                // 这里是异步操作
+   p.textContent = 'Hello World!';
+ }, 5000);                         // 2秒后更新文本内容
p.style.color = 'red'; // 立即执行，不会被阻塞
```

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251208144318601.png)

有些操作自动就是异步的，比如：
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251208144613389.png)

```js
const img = document.querySelector('img')
img.src = 'large-image.jpg' // 加载大图是异步的
img.addEventListener('load', function () {
  console.log('Image loaded!')
})
p.style.border = '2px solid black' // 立即执行
```

## AJAX

AJAX（Asynchronous JavaScript and XML）是一种用于在不重新加载整个网页的情况下与服务器异步通信的技术。它允许网页在后台与服务器进行通信，从而实现更动态和交互式的用户体验。

虽然是叫`XML`，但现在大多数情况下我们使用`JSON`作为数据交换格式。

### XMLHttpRequest 对象

`XMLHttpRequest` 对象是用于在浏览器中与服务器进行异步通信的核心 API。它允许你发送 HTTP 请求并接收响应，而无需刷新整个页面。

但是现在更推荐使用 Fetch API 来进行异步请求，因为它更现代化，使用起来也更简洁。

{% btn
 'https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest',
 'MDN 文档',
 far fa-hand-point-right,blue larger
%}

比如：

```js
const request = new XMLHttpRequest()
request.open('GET', `https://restcountries.com/v3.1/name/${name}`)
request.send() // 发送请求，但不会阻塞代码运行，因为这个操作在后台进行。
// 所以不能简单接受请求发送后就立刻使用数据
// const response = request.send() // 不能这样写, 因为异步操作的结果不能立刻获得

request.addEventListener('load', function () {
  const [data] = JSON.parse(this.responseText)
  console.log(data)
})
```

### Fetch API

Fetch API 是现代浏览器中用于发起网络请求的接口，提供了更简洁和强大的方式来处理异步请求。它基于 Promise，使得处理异步操作更加直观和易于管理。

```js
fetch('https:example.com/data', {
  method: 'POST', // 或 'POST', 'PUT', 'DELETE' 等
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({ key: 'value' }), // 仅在 POST 或 PUT 请求中使用
}).then(function(response) {
  return response.json()
}).then(function(data) {
  console.log(data)
})
```

### Content-Type是什么？

在 HTTP 请求中，`Content-Type`（内容类型）是一个极其重要的请求头。它的作用是**告诉服务器：我发送给你的数据是什么格式的，请你按照这种格式来解析。**

如果 `Content-Type` 设置错误，服务器可能无法正确读取你发送的数据，导致报错（如 400 Bad Request 或 500 错误）。

**常见 Content-Type**：

#### 1. `application/json` (最常用)

这是现代 Web 开发（尤其是 RESTful API）中最标准的格式。

* **含义**：发送的是一个 **JSON 字符串**。
* **前端写法**：需要手动用 `JSON.stringify(data)` 转化。
* **后端处理**：后端（如 Node.js, Spring Boot）会自动将其解析为对象。
* **例子**：
```javascript
fetch('/api/user', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: "张三", age: 25 })
});
```

#### 2. `application/x-www-form-urlencoded`

这是传统的 **HTML 表单** 默认的提交方式。

* **含义**：数据被编码为键值对，用 `&` 分隔，类似于 URL 的查询字符串。
* **特点**：不支持发送文件，只能发简单的文本。
* **数据长相**：`name=%E5%BC%A0%E4%B8%89&age=25`
* **例子**：
```javascript
const params = new URLSearchParams({ name: "张三", age: 25 });
fetch('/api/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
  body: params.toString()
});
```

#### 3. `multipart/form-data`

这种格式专门用于 **上传文件** 或发送包含二进制数据的内容。

* **含义**：数据被分成多个部分（parts），每个部分可以有不同的类型（如文本字段 + 图片文件）。
* **注意点**：使用 `fetch` 发送 `FormData` 对象时，**不要手动设置 Content-Type**。浏览器会自动帮你添加，并生成一个复杂的 `boundary`（边界字符串）来区分不同的字段。
* **例子**：
```javascript
const formData = new FormData();
formData.append('username', 'Alice');
formData.append('avatar', fileInput.files[0]); // 文件对象

fetch('/upload', {
  method: 'POST',
  body: formData // 此时 fetch 会自动识别并设置 multipart/form-data
});
```

#### 4. `text/plain`

* **含义**：纯文本格式。
* **特点**：没有任何特定的结构。服务器通常不会对其进行解析，只会当做一串普通的文字处理。现在在 API 开发中已经很少使用了。

---

## Callback Hell(回调地狱)

回调地狱是指在使用回调函数处理异步操作时，代码层层嵌套，导致代码难以阅读和维护的情况。
比如，下一个操作依赖于上一个操作的结果，而上一个操作又是异步的，这样就会导致回调函数嵌套。

比如：

```js
setTimeout(() => {
  console.log('1 second passed')
  setTimeout(() => {
    console.log('2 seconds passed')
    setTimeout(() => {
      console.log('3 seconds passed')
      setTimeout(() => {
        console.log('4 seconds passed')
      }, 1000)
    }, 1000)
  }, 1000)
}, 1000)
```

又比如：

```js
const btn = document.querySelector('.btn-country')
const countriesContainer = document.querySelector('.countries')

const renderCountry = function (data, className = '') {
  const html = `
       <article class="country ${className}">
          <img class="country__img" src="${data.flags.png}" />
          <div class="country__data">
            <h3 class="country__name">${data.name.common}</h3>
            <h4 class="country__region">${data.region}</h4>
            <p class="country__row"><span>👫</span>
            ${(+data.population / 1000000).toFixed(1)}M people
            </p>
            <p class="country__row"><span>🗣️</span>${
              data.languages[Object.keys(data.languages)[0]]
            }</p>
            <p class="country__row"><span>💰</span>${
              data.currencies[Object.keys(data.currencies)[0]].name
            }</p>
          </div>
        </article>`

  countriesContainer.insertAdjacentHTML('beforeend', html)
  countriesContainer.style.opacity = 1
}

// 回调地狱示例代码
const getCountryAndNeighbor = function (name) {
  // AJAX 1
  const request = new XMLHttpRequest()
  request.open('GET', `https://restcountries.com/v3.1/name/${name}`)
  request.send()

  request.addEventListener('load', function () {
    const [data] = JSON.parse(this.responseText)
    console.log(data)

    // 渲染本国
    renderCountry(data)

    // 获取邻国
    const [neighbor] = data.borders
    console.log(neighbor)
    if (!neighbor) return

    // AJAX 2
    const request2 = new XMLHttpRequest()
    request2.open('GET', `https://restcountries.com/v3.1/alpha/${neighbor}`)
    request2.send()

    request2.addEventListener('load', function () {
      const [data2] = JSON.parse(this.responseText)
      console.log(data2)
      renderCountry(data2, 'neighbour')

      const [neighbor2] = data2.borders
      console.log(neighbor2)
      if (!neighbor2) return

      // AJAX 3
      const request3 = new XMLHttpRequest()
      request3.open('GET', `https://restcountries.com/v3.1/alpha/${neighbor2}`)
      request3.send()

      request3.addEventListener('load', function () {
        const [data3] = JSON.parse(this.responseText)
        console.log(data3)
        renderCountry(data3, 'neighbour')

        const [neighbor3] = data3.borders
        console.log(neighbor3)
        if (!neighbor3) return

        // AJAX 4
        const request4 = new XMLHttpRequest()
        request4.open('GET', `https://restcountries.com/v3.1/alpha/${neighbor3}`)
        request4.send()
        request4.addEventListener('load', function () {
          const [data4] = JSON.parse(this.responseText)
          console.log(data4)
          renderCountry(data4, 'neighbour')

          const [neighbor4] = data4.borders
          console.log(neighbor4)
          if (!neighbor4) return

          // AJAX 5
          const request5 = new XMLHttpRequest()
          request5.open('GET', `https://restcountries.com/v3.1/alpha/${neighbor4}`)
          request5.send()
          request5.addEventListener('load', function () {
            const [data5] = JSON.parse(this.responseText)
            console.log(data5)
            renderCountry(data5, 'neighbour')
          })
        })
      })
    })
  })
}

// getCountryAndNeighbor('portugal');
getCountryAndNeighbor('china')
```

## Promises

Promise 是 JavaScript 中用于处理异步操作的一种机制。它表示一个可能在未来某个时间点完成或失败的操作，并允许你注册回调函数来处理这些结果。Promise 有三种状态：待定（pending）、已完成（fulfilled）和已拒绝（rejected）。

Promise 是属于微任务队列的。所以当主线程执行完同步代码后，会先去执行微任务队列中的任务，再去执行宏任务队列中的任务。

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251208163144529.png)
![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20251208163714981.png)

### Consuming Promises

如果你有一个返回 Promise 的函数，比如``fetch()` api，你可以使用 `.then()` 方法来处理成功的结果，使用 `.catch()` 方法来处理错误。

```js
const btn = document.querySelector('.btn-country')
const countriesContainer = document.querySelector('.countries')

const renderCountry = function (data, className = '') {
  const html = `
       <article class="country ${className}">
          <img class="country__img" src="${data.flags.png}" />
          <div class="country__data">
            <h3 class="country__name">${data.name.common}</h3>
            <h4 class="country__region">${data.region}</h4>
            <p class="country__row"><span>👫</span>
            ${(+data.population / 1000000).toFixed(1)}M people
            </p>
            <p class="country__row"><span>🗣️</span>${
              data.languages[Object.keys(data.languages)[0]]
            }</p>
            <p class="country__row"><span>💰</span>${
              data.currencies[Object.keys(data.currencies)[0]].name
            }</p>
          </div>
        </article>`

  countriesContainer.insertAdjacentHTML('beforeend', html)
  countriesContainer.style.opacity = 1
}

// Consuming Promises
const getCountryData = function (name) {
  fetch(`https://restcountries.com/v3.1/name/${name}`)
    .then(function (response) {
      // 假设promise状态是fulfilled
      console.log(response)
      // 所有的response对象都有一个.json()方法, 这个方法也是异步的, 它同样会返回一个promise
      // 因为json（）方法也是异步，我们接下来也返回一个promise
      return response.json()
    })
    .then(function (data) {
      console.log(data)
      renderCountry(data[0])
    })
}

getCountryData('portugal')
```

**链式调用，下一个请求依赖上一个请求的结果：**

```js
const getCountryData = function (name) {
  fetch(`https://restcountries.com/v3.1/name/${name}`)
    .then(response => response.json())
    .then(data => {
      renderCountry(data[0])
      // console.log(data);
      const neighbor = data[0].borders?.[0]
      console.log(neighbor)
      if (!neighbor) return

      // 获取邻国数据, 返回一个新的fetch的promise
      return fetch(`https://restcountries.com/v3.1/alpha/${neighbor}`)
    }) // 上面返回的promise，就是下面then的输入，比如下面的response
    .then(response => response.json())
    .then(data => renderCountry(data[0], 'neighbour'))
}

getCountryData('portugal')
```

**简单的处理错误**：

```js
const getCountryData = function (name) {
  fetch(`https://restcountries.com/v3.1/name/${name}`)
    .then(
      response => response.json(),
      // err => window.alert(err) // 一个一个处理错误（不推荐）
    )
    .then(data => {
      renderCountry(data[0])
      const neighbor = data[0].borders?.[0]
      console.log(neighbor)
      if (!neighbor) return

      return fetch(`https://restcountries.com/v3.1/alpha/${neighbor}`)
    })
    .then(response => response.json())
    .then(data => renderCountry(data[0], 'neighbour'))
    .catch(err => {
      // catch会自动返回promise
      // 一次性处理错误（推荐）
      console.error(`${err} 💥💥`)
      renderError(`Something went wrong 💥💥 ${err.message}. Try again!`)
    })
    .finally(() => {
      // 无论成功还是失败，都会执行
    })
}
```

**抛出错误**：

```js
// 显示错误
const renderError = function (msg) {
  countriesContainer.insertAdjacentText('beforeend', msg)
}

// 错误处理
const getJson = function (url, errorMessage = 'Something went wrong') {
  return fetch(url).then(response => {
    if (!response.ok) throw new Error(`${errorMessage} (${response.status})`)

    return response.json()
  })
}

const getCountryData = function (name) {
  getJson(`https://restcountries.com/v3.1/name/${name}`, 'Country not found')
    .then(data => {
      renderCountry(data[0])
      const neighbor = data[0].borders?.[0]

      if (!neighbor) throw new Error('No neighbor found!')

      return getJson(`https://restcountries.com/v3.1/alpha/${neighbor}`, 'Country not found')
    })
    .then(data => renderCountry(data[0], 'neighbour'))
    .catch(err => {
      console.error(`${err} 💥💥`)
      renderError(`Something went wrong 💥💥 ${err.message}. Try again!`)
    })
    .finally(() => {
      countriesContainer.style.opacity = 1
    })
}

btn.addEventListener('click', function () {
  getCountryData('australia')
})
```

### Building Promises

你可以使用 `new Promise()` 来创建一个新的 Promise 对象。这个构造函数接受一个执行器函数作为参数，该函数包含两个参数：`resolve` 和 `reject`。当异步操作成功时，调用 `resolve`；当失败时，调用 `reject`。

```js
// 创建一个promise
// 参数函数叫executor
const lotteryPromise = new Promise(function (resolve, reject) {
  console.log('Lottery draw is happening 🔮')

  // 用定时器模拟异步操作, 否则就是同步操作
  setTimeout(() => {
    if (Math.random() >= 0.5) {
      // fulfilled, 参数可以通过.then()访问
      resolve('You WIN 💰')
    } else {
      // rejected, 参数可以通过.catch()访问
      reject(new Error('You LOSE 💩'))
    }
  }, 2000)
})

// Consuming the promise
lotteryPromise.then(res => console.log(res)).catch(err => console.error(err))
console.log('---')
```

> 其实这段代码是同步和异步混合执行的，我们来一步步拆解：
> 同步部分：new Promise(...) 构造函数本身以及传递给它的那个函数（executor function）是同步执行的。
> 所以，当这段代码运行时，console.log('Lottery draw is happening 🔮') 会立刻被打印出来。
> Math.random() 的计算和 if 判断也是立刻完成的，Promise 的状态（fulfilled 或 rejected）在这一步就已经决定了。
> 异步部分：.then() 和 .catch() 里的回调函数是异步执行的。
> 它们会被放入一个叫做“微任务”（microtask）的队列里，要等到当前所有同步代码（包括 console.log('---')）都执行完毕后，才会被调用。

**Promisefy**：

将基于回调的异步函数转换为返回 Promise 的函数。

比如下面这是基于回调的异步函数：

```js
setTimeout(() => {
  console.log('1 second passed')
  setTimeout(() => {
    console.log('2 seconds passed')
    setTimeout(() => {
      console.log('3 seconds passed')
      setTimeout(() => {
        console.log('4 seconds passed')
      }, 1000)
    }, 1000)
  }, 1000)
}, 1000)
```

你可以把它改写成返回 Promise 的函数：

```js
// Promisifying setTimeout
const wait = function (seconds) {
  // 不需要reject，因为定时器不会失败
  return new Promise(function (resolve) {
    setTimeout(resolve, seconds * 1000)
  })
}

wait(1)
  .then(() => {
    console.log('1 second passed')
    return wait(1)
  })
  .then(() => {
    console.log('2 seconds passed')
    return wait(1)
  })
  .then(() => {
    console.log('3 seconds passed')
    return wait(1)
  })
  .then(() => console.log('4 seconds passed'))
```

**快速创建 fullfilled 或者 rejected 的 Promise**：

```js
// Promise.resolve, 立刻执行并返回一个成功的promise
Promise.resolve('abc').then(x => console.log(x))
// Promise.reject, 立刻执行并返回一个失败的promise
Promise.reject(new Error('Problem!')).catch(x => console.error(x))
```

**把 callback base 异步函数转化成 Promise 异步函数**：

```js
// callback base 异步获取地理位置
window.navigator.geolocation.getCurrentPosition(
  position => console.log(position),
  err => console.error(err),
)

// Promise base 获取地理位置
const getPosition = function () {
  return new Promise(function (resolve, reject) {
    window.navigator.geolocation.getCurrentPosition(
      position => resolve(position),
      err => reject(err),
    )
  })
}

getPosition()
  .then(pos => console.log(pos))
  .catch(err => console.error(err))
```

简化代码：

```js
position => resolve(position), err => reject(err)

// 可以简化为：
// resolve,
// reject

// 比如
const getPosition = function () {
  return new Promise(function (resolve, reject) {
    window.navigator.geolocation.getCurrentPosition(resolve, reject)
  })
}
```

## Async/Await

`async` 和 `await` 是 JavaScript 中用于处理异步操作的关键字。它们使得异步代码看起来更像同步代码，从而提高了代码的可读性和可维护性。

需要注意的是，这只是语法糖，底层依然是基于 Promise 实现的。比如，背后还是 then(),catch()在起作用。

```js
const renderError = function (msg) {
  countriesContainer.insertAdjacentText('beforeend', msg)
}

// Async / Await
// 用async声明这个函数是异步的
const getCountryData = async function (country) {
  try {
    // await 等待这个promise完成，所以我们可以拿到异步操作后的结果
    const response = await fetch(`https://restcountries.com/v3.1/name/${country}`)

    if (!response.ok) throw new Error(`Country not found (${response.status})`)

    // 解析json也是异步的，所以也要await
    const [data] = await response.json()
    renderCountry(data)
  } catch (err) {
    console.error(`${err} 💥💥`)
    renderError(`Something went wrong 💥💥 ${err.message}. Try again!`)
  } finally {
    countriesContainer.style.opacity = 1
  }
}

btn.addEventListener('click', function () {
  getCountryData('germany')
})
```

## Async 函数返回什么？

`async` 函数总是返回一个 Promise。如果函数内部返回一个值，这个值会被自动包装成一个已解决的 Promise；如果函数抛出一个错误，这个错误会被包装成一个已拒绝的 Promise。

```js
// Async / Await
const getCountryData = async function (country) {
  try {
    const response = await fetch(`https://restcountries.com/v3.1/name/${country}`)

    if (!response.ok) throw new Error(`Country not found (${response.status})`)

    const [data] = await response.json()
    renderCountry(data)

    // 返回值会被包装在一个fulfilled的promise里
    return `You are in ${data.name.common}`
  } catch (err) {
    console.error(`${err} 💥💥`)
    renderError(`Something went wrong 💥💥 ${err.message}. Try again!`)
  } finally {
    countriesContainer.style.opacity = 1
  }
}

btn.addEventListener('click', function () {
  console.log('btn clicked')
  const name = getCountryData('germany')
  console.log(name) // Promise {<pending>}
  console.log('getCountryData called')
})
```

可以通过 then 获取 fullfilled 值：

```js
getCountryData('germany').then(msg => console.log(msg))
```

为什么这里不用 await 呢？因为 await 只能在 async 函数内部使用。

如果还是喜欢使用 async/await 的语法，可以这样写：

```js
// IIFE
// 立即调用异步函数
;(async function () {
  const msg = await getCountryData('portugal')
  console.log(msg)
})()
```

## 多个 Promise 并行执行

下面是一种不推荐的写法：

```js
const getJson = function (url, errorMessage = 'Something went wrong') {
  return fetch(url).then(response => {
    if (!response.ok) throw new Error(`${errorMessage} (${response.status})`)

    return response.json()
  })
}

const get3Countries = async function (c1, c2, c3) {
  try {
    // 按顺序执行，虽然下一个请求不依赖于上一个请求的结果
    const [data1] = await getJson(`https://restcountries.com/v3.1/name/${c1}`)
    const [data2] = await getJson(`https://restcountries.com/v3.1/name/${c2}`)
    const [data3] = await getJson(`https://restcountries.com/v3.1/name/${c3}`)
    console.log([data1.capital[0], data2.capital[0], data3.capital[0]])
  } catch (error) {
    console.error(error)
  }
}

get3Countries('germany', 'usa', 'china')
```

推荐的写法是用`Promise.all()`，这个函数的参数是一个 promise 数组，返回一个新的 promise，这个新的 promise 在所有的 promise 都 fulfilled 后才会 fulfilled。如果某个 promise 发生 rejected，那么整个 promise.all 都是 rejected。

```js
const get3Countries = async function (c1, c2, c3) {
  try {
    // 并行执行
    const [[data1], [data2], [data3]] = await Promise.all([
      getJson(`https://restcountries.com/v3.1/name/${c1}`),
      getJson(`https://restcountries.com/v3.1/name/${c2}`),
      getJson(`https://restcountries.com/v3.1/name/${c3}`),
    ])
    console.log([data1.capital[0], data2.capital[0], data3.capital[0]])
  } catch (error) {
    console.error(error)
  }
}

get3Countries('germany', 'usa', 'china')
```

## 一些常用的 Promise 组合方法

### Promise.race()

这个方法的参数是一个 promise 数组，返回这数组里面第一个 fullfilled 的 promise。

我们通过这个方法，可以设置请求超时事件。

```js
const timeout = function (sec) {
  return new Promise(function (_, reject) {
    setTimeout(function () {
      reject(new Error('Request took too long!'))
    }, sec * 1000)
  })
}

Promise.race([getJson('https://restcountries.com/v3.1/name/egypt'), timeout(0.3)])
  .then(res => console.log(res[0]))
  .catch(err => console.error(err))
```

### Promise.allSettled()

这个方法的参数是一个 promise 数组，返回一个新的 promise，这个新的 promise 在所有的 promise 都 settled（不管是 fulfilled 还是 rejected）后才会 fulfilled。返回值是一个对象数组，表示每个 promise 的结果状态。

```js
Promise.allSettled([
  Promise.resolve('Success'),
  Promise.reject('Error'),
  Promise.resolve('Another success'),
]).then(res => console.log(res))
```

# MODULES

{% btn
 'https://juejin.cn/post/7445507443868172323',
 '掘金链接',
 far fa-hand-point-right,blue larger
%}

# NPM

## 初始化

```bash
npm init
```

然后产生一个`package.json`文件。

```json
{
  "name": "16-asynchronous",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Akbar",
  "license": "ISC",
  "description": "Akbar's Asynchronous JavaScript Project"
}
```

## 安装依赖

- **生产依赖：**生产依赖是指在应用程序运行时所需的库或模块。这些依赖对于应用程序的核心功能是必不可少的。生产依赖通常会被包含在最终的部署包中，以确保应用程序在生产环境中能够正常运行。

```bash
npm install lodash-es --save
```

默认就是`--save`，所以可以省略。

- **开发依赖：**开发依赖是指在开发过程中所需的库或工具，这些依赖对于应用程序的运行并不是必需的。它们通常用于测试、构建、代码质量检查等任务。开发依赖不会被包含在最终的部署包中，因为它们只在开发环境中使用。

```bash
npm install jest --save-dev
```

- **安装全部依赖**

```bash
npm install
```

## 使用已安装的包

默认指向的就是`node_modules`目录下的包。

```js
import deepClone from 'lodash-es/cloneDeep.js'
```

# PUBLIC API

{% btn
 'https://github.com/public-apis/public-apis',
 'Public APIs 列表(GitHub)',
 far fa-hand-point-right,blue larger
%}

1. **获取国家信息**：搜索`REST Countries`
