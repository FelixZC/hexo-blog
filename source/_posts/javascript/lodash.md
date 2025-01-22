---
title: lodash 
date: 2025-01-22
author: "pzc"
cover: /assets/images/jpg/138.jpg
categories: [javaScript]
---
## 介绍

Lodash 是一个 JavaScript 工具库，提供了很多用于操作对象、数组、字符串等数据类型的实用函数。它旨在使 JavaScript 编程更加简单和高效，避免了编写重复的样板代码。Lodash 的函数式编程风格使得代码更具有可读性和模块化。

一些 Lodash 的常用功能包括：

- `_.map()`, `_.filter()`, `_.reduce()` 等集合操作方法，这些是函数式编程中非常重要的高阶函数。
- `_.get()`, `_.set()`, `_.has()` 用来安全地获取、设置或检查对象属性，即使路径中的某些节点不存在也不会报错。
- `_.isEqual()` 用来进行深比较，判断两个值是否相等。
- `_.cloneDeep()` 用来创建复杂嵌套对象的深拷贝。
- `_.omit()` 和 `_.pick()` 分别用来从对象中移除或挑选指定键。
- `_.debounce()` 和 `_.throttle()` 用来控制函数调用的频率，在处理用户输入或窗口调整大小等事件时非常有用。

你可以通过 npm 或者直接在 HTML 文件中引入 lodash 库来使用它。如果你只使用了 lodash 的一小部分功能，还可以考虑使用 lodash 的按需加载特性或者改用 lodash-es，以减少打包后的文件体积。

例如，要安装 lodash 可以使用以下命令：
```
npm install lodash
```

然后在你的代码中这样引入：
```javascript
const _ = require('lodash');
// 或者在 ES6 模块环境中
import _ from 'lodash';
```

如果你只需要特定的功能，可以只引入那个功能，比如只引入 map 方法：
```javascript
import map from 'lodash/map';
```

这有助于减少最终部署的代码量，优化性能。

## 资料

下面是一些获取更多关于 Lodash 资料的途径：

1. **官方文档**：
   - 访问 [Lodash 官方网站](https://lodash.com/) 可以找到最新的文档、下载链接和使用示例。
   - 官方文档详细解释了每一个函数的作用、用法、参数以及返回值，并且提供了代码片段作为例子。

2. **GitHub 仓库**：
   - 在 [Lodash GitHub 仓库](https://github.com/lodash/lodash) 中，您可以查看项目的源代码，了解开发进度，提交问题或者参与贡献。

3. **博客文章**：
   - 许多开发者会在个人博客上分享他们使用 Lodash 的经验和技巧，搜索相关关键词可能会发现一些有用的文章。

## 常用

Lodash 提供了非常多实用的功能，以下是其中一些最常用的功能列表。这些功能可以帮助开发者更高效地处理常见的编程任务。

### 集合操作

- **`_.map(collection, [iteratee=_.identity])`**：创建一个数组，其元素是 `collection` 中每个元素执行给定函数后的结果。
- **`_.filter(collection, [predicate=_.identity])`**：创建一个数组，包含所有满足 `predicate` 断言函数的元素。
- **`_.reduce(collection, [iteratee=_.identity], [accumulator])`**：减少 `collection` 到单个值，从左到右依次对每个元素应用 `iteratee` 函数。
- **`_.find(collection, [predicate=_.identity], [fromIndex=0])`**：返回集合中第一个满足断言函数的元素；如果没有找到，则返回 `undefined`。
- **`_.forEach(collection, [iteratee=_.identity])`**：对 `collection` 中的每个元素执行一次 `iteratee` 函数。

### 对象操作

- **`_.get(object, path, [defaultValue])`**：安全获取对象 `path` 路径下的值，如果路径不存在则返回 `defaultValue`。
- **`_.set(object, path, value)`**：设置对象 `path` 路径下的值为 `value`。
- **`_.has(object, path)`**：检查对象是否有指定 `path` 的属性。
- **`_.omit(object, [paths])`**：创建一个省略了指定键的对象副本。
- **`_.pick(object, [paths])`**：创建一个只包含指定键的对象副本。

### 数组操作

- **`_.chunk(array, [size=1])`**：将数组分割成多个长度为 `size` 的较小数组。
- **`_.flatten([array])`**：将多维数组展平成一维数组。
- **`_.uniq([array])`**：创建一个去重后的数组副本。
- **`_.union(...arrays)`**：创建一个由所有给定数组中的唯一元素组成的数组。
- **`_.difference(array, [values])`**：创建一个由 `array` 中不包含在 `values` 中的元素组成的数组。

### 比较与判断

- **`_.isEqual(value, other)`**：进行深度比较，判断两个值是否相等。
- **`_.isMatch(object, source)`**：检查 `object` 是否具有 `source` 所有键值对。
- **`_.isEmpty(value)`**：检查值是否为空（例如空数组、对象、字符串等）。

### 复制与克隆

- **`_.clone(value)`**：创建一个浅拷贝。
- **`_.cloneDeep(value)`**：创建一个深拷贝，递归复制对象和数组。

### 函数操作

- **`_.debounce(func, wait, [options={}] )`**：创建一个防抖动函数，该函数会在停止调用后等待 `wait` 毫秒才执行。
- **`_.throttle(func, wait, [options={}] )`**：创建一个节流函数，确保 `func` 不会比 `wait` 毫秒更频繁地被调用。

### 字符串操作

- **`_.trim([string=' '], [chars=' \t\r\n'])`**：移除字符串开头和结尾处的空白字符或其他字符。
- **`_.split([string=''], [separator], [limit])`**：通过指定分隔符将字符串拆分成数组。

### 其他

- **`_.noop()`**：一个什么都不做的函数，通常用作默认回调或占位符。
- **`_.times(n, [iteratee=_.identity])`**：调用 `iteratee` 函数 `n` 次，并创建一个包含每次调用结果的数组。

这只是 Lodash 库的一小部分功能。它还提供了许多其他有用的方法来处理日期、数学运算、随机数生成等。要了解所有可用方法及其详细用法，请参阅官方文档。如果您需要关于某个特定功能的帮助或示例代码，请随时询问。

## 示例

下面是几个使用 Lodash 的完整示例代码，这些例子涵盖了常见的操作和场景。为了演示的目的，我将展示如何使用一些最常用的功能。

### 示例 1: 使用 `_.map` 和 `_.filter`

假设我们有一个包含用户信息的数组，并且我们想要获取所有年龄大于30岁的用户的姓名列表。

```javascript
const users = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 31 },
  { name: 'Charlie', age: 35 }
];

// 获取年龄大于30岁的用户姓名
const names = _.chain(users)
  .filter(user => user.age > 30)
  .map('name')
  .value();

console.log(names); // 输出: ['Bob', 'Charlie']
```

在这个例子中，我们使用了链式调用（`_.chain`）来组合多个 Lodash 方法，最后通过 `value()` 来执行链中的所有操作并返回结果。

### 示例 2: 使用 `_.get` 安全访问嵌套对象属性

考虑一个可能有也可能没有某些嵌套属性的对象，我们可以安全地尝试获取其值而不用担心抛出错误。

```javascript
const user = {
  address: {
    city: 'New York'
  }
};

// 安全地获取地址的城市名，默认值为 'Unknown'
const city = _.get(user, 'address.city', 'Unknown');
console.log(city); // 输出: 'New York'

// 尝试获取不存在的属性，使用默认值
const street = _.get(user, 'address.street', 'No Street Info');
console.log(street); // 输出: 'No Street Info'
```

### 示例 3: 深拷贝对象

当我们需要复制一个复杂的数据结构而不影响原始数据时，可以使用 `_.cloneDeep`。

```javascript
const source = {
  name: 'Example',
  details: {
    description: 'An example object.',
    tags: ['example', 'test']
  }
};

// 创建深拷贝
const clone = _.cloneDeep(source);

// 修改克隆对象
clone.details.description = 'Modified description';

console.log(clone.details.description); // 输出: 'Modified description'
console.log(source.details.description); // 输出: 'An example object.'
```

### 示例 4: 使用 `_.debounce` 防抖动函数

在处理如窗口调整大小或用户输入等高频事件时，防抖动可以限制回调函数的执行频率。

```javascript
// 创建一个防抖动函数，在最后一次调用后的1秒后执行
const debouncedResize = _.debounce(() => {
  console.log('Window resized.');
}, 1000);

window.addEventListener('resize', debouncedResize);
```

### 示例 5: 使用 `_.isEqual` 进行深度比较

当我们要比较两个复杂对象是否相等时，`_.isEqual` 提供了一个简单的方法。

```javascript
const obj1 = { a: [{ b: 2 }] };
const obj2 = { a: [{ b: 2 }] };

console.log(_.isEqual(obj1, obj2)); // 输出: true

obj1.a[0].b = 3;
console.log(_.isEqual(obj1, obj2)); // 输出: false
```

### 示例 6: 使用 `_.omit` 和 `_.pick`

有时候我们需要创建一个对象的副本，只保留或者排除某些特定键。

```javascript
const original = { id: 1, name: 'John', email: 'john@example.com' };

// 创建一个新对象，仅保留 'id' 和 'name'
const picked = _.pick(original, ['id', 'name']);
console.log(picked); // 输出: { id: 1, name: 'John' }

// 创建一个新对象，省略 'email'
const omitted = _.omit(original, ['email']);
console.log(omitted); // 输出: { id: 1, name: 'John' }
```

这些只是 Lodash 功能的一小部分示例。Lodash 提供了大量的工具方法，可以帮助简化 JavaScript 编程中的各种任务。希望这些例子能够帮助您更好地理解如何在实际项目中应用 Lodash。