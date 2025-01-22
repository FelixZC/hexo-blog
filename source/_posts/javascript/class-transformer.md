---
title: class-transformer
author: pzc
date: 2025-01-22
cover: /assets/images/jpg/139.jpg
categories: [javaScript]
---
## 介绍

`class-transformer` 是一个用于 TypeScript 和 JavaScript 的库，它允许你轻松地在类实例和普通对象（POJOs）之间进行转换。这个库特别有用当你使用像 NestJS 这样的框架时，这些框架依赖于装饰器来定义数据传输对象（DTOs），并且需要将请求和响应对象映射到这些 DTO 类。

以下是 `class-transformer` 的一些主要功能：

1. **PlainToClass**：将普通的 JavaScript 对象（POJOs）转换为带有装饰器的类实例。
2. **ClassToPlain**：将带有装饰器的类实例转换为普通的 JavaScript 对象。
3. **Exclude 和 Expose**：你可以选择性地排除某些属性不被序列化或反序列化，或者只暴露特定的属性。
4. **Transform**：可以在转换过程中对属性值进行自定义变换。
5. **Validation**：与 `class-validator` 一起使用可以验证类实例的数据。

### 使用示例

首先你需要安装 `class-transformer` 包：

```bash
npm install class-transformer
```

然后你可以创建一个类并使用 `class-transformer` 提供的装饰器来定义如何处理类的属性：

```typescript
import { plainToClass, classToPlain } from 'class-transformer';

class User {
  @Expose()
  id: number;

  @Expose()
  name: string;

  // This property will not be exposed when converting to plain object
  password: string;

  constructor(id: number, name: string, password: string) {
    this.id = id;
    this.name = name;
    this.password = password;
  }
}

// Creating an instance of User
const user = new User(1, 'John Doe', 'secret');

// Converting class to plain object
const plainUser = classToPlain(user); // { id: 1, name: 'John Doe' }

// Converting plain object back to class
const userFromPlain = plainToClass(User, plainUser); // User { id: 1, name: 'John Doe', password: undefined }
```

在这个例子中，`password` 属性不会出现在转换后的普通对象中，因为我们没有对其应用 `@Expose()` 装饰器。同时，当我们从普通对象转换回类实例时，`password` 属性会被设置为 `undefined`，因为原始的普通对象中没有这个属性。

`class-transformer` 库是构建强类型 API 或任何需要在类实例和普通对象之间转换的应用程序的一个有力工具。

## 示例

这里提供一个更加完整的 `class-transformer` 示例，包括类定义、转换过程以及使用装饰器来控制属性的暴露。这个例子还将展示如何结合 `class-validator` 使用来进行数据验证。

首先，确保安装了必要的依赖：

```bash
npm install class-transformer class-validator reflect-metadata
```

注意：`reflect-metadata` 需要被显式安装，并且需要在你的应用入口文件（如 `index.ts` 或 `main.ts`）顶部添加以下代码行来启用元数据反射：

```typescript
import 'reflect-metadata';
```

接下来是示例代码：

```typescript
import { plainToClass, classToPlain, Exclude, Expose, Transform } from 'class-transformer';
import { IsInt, IsString, Min, Max, validateOrReject } from 'class-validator';

class Product {
  @Expose()
  @IsInt()
  @Min(1)
  id: number;

  @Expose()
  @IsString()
  name: string;

  @Expose()
  @Transform(({ value }) => parseFloat(value), { toClassOnly: true })
  @Transform(({ value }) => value.toFixed(2), { toPlainOnly: true })
  price: number;

  @Exclude() // This field will not be included in the output
  cost: number;

  constructor(id: number, name: string, price: number, cost: number) {
    this.id = id;
    this.name = name;
    this.price = price;
    this.cost = cost;
  }
}

// Example usage:

async function run() {
  // Creating an instance of Product with some data.
  const product = new Product(1, 'Laptop', 999.99, 800);

  // Converting class to plain object - cost is excluded.
  const plainProduct = classToPlain(product);
  console.log('Plain Object:', plainProduct); // { id: 1, name: 'Laptop', price: '999.99' }

  // Converting plain object back to class - price transformation applies.
  const productFromPlain = plainToClass(Product, plainProduct);
  console.log('Class Instance:', productFromPlain); // Product { id: 1, name: 'Laptop', price: 999.99, cost: undefined }

  // Validating the class instance before use.
  try {
    await validateOrReject(productFromPlain);
    console.log('Validation passed!');
  } catch (errors) {
    console.error('Validation failed:', errors);
  }
}

run().catch(console.error);
```

在这个例子中：

- `@Expose()` 装饰器用来标记哪些属性应该在转换为普通对象时包含。
- `@Exclude()` 装饰器用于排除特定属性，这样它们就不会出现在转换后的普通对象中。
- `@Transform()` 装饰器允许你在转换过程中对值进行修改。这里它用于将价格格式化为两位小数的字符串表示形式（当从类转换到普通对象时），并且在反向转换时将字符串转换回数字。
- `class-validator` 的装饰器（如 `@IsInt`, `@IsString`, `@Min`, `@Max`）用于定义字段的有效性规则。`validateOrReject` 函数用于执行这些规则并返回任何验证错误。

这段代码展示了如何创建一个 `Product` 类实例，然后将其转换为普通对象再转回来，同时利用 `class-transformer` 和 `class-validator` 来处理和验证数据。

## POJOs

POJO 是 Plain Old JavaScript Object 的缩写，在 Java 领域也有类似的术语，称为 Plain Old Java Object。这个术语用来描述那些没有继承任何特殊类或实现特定接口的简单对象。在 JavaScript 和 TypeScript 中，POJO 指的是那些只包含数据属性的对象，而不包含方法或其他复杂的特性。

### POJO 的特点

1. **简单性**：POJOs 只是普通的对象字面量，它们不需要依赖于框架或库，可以很容易地创建和理解。
2. **互操作性**：由于它们不依赖于特定的上下文或环境，POJOs 可以轻松地与不同的库或框架一起使用。
3. **易序列化**：POJOs 很容易被转换为 JSON 字符串（通过 `JSON.stringify`），也可以从 JSON 字符串中解析出来（通过 `JSON.parse`）。
4. **轻量级**：因为它们仅仅是数据容器，所以 POJOs 通常占用较少的内存资源。

### 创建 POJO

在 JavaScript 或 TypeScript 中创建一个 POJO 是非常直接的：

```javascript
// 简单的 POJO
const person = {
  name: 'Alice',
  age: 30,
  city: 'Wonderland'
};

console.log(person.name); // 输出: Alice
```

或者你可以使用构造函数来创建多个具有相同结构的 POJOs：

```javascript
function createPerson(name, age, city) {
  return {
    name,
    age,
    city
  };
}

const alice = createPerson('Alice', 30, 'Wonderland');
const bob = createPerson('Bob', 25, 'Builderland');

console.log(alice.city); // 输出: Wonderland
console.log(bob.age);    // 输出: 25
```

### 在 `class-transformer` 中的作用

在 `class-transformer` 库中，POJOs 起到了桥梁的作用，用于在类实例和普通对象之间进行转换。例如，当你接收到来自 API 请求的数据时，这些数据通常是 JSON 格式的，并且会被解析成 POJOs。然后你可以使用 `plainToClass` 方法将这些 POJOs 转换成带有装饰器定义的类实例，从而利用类型检查、验证和其他功能。相反，当你需要发送响应给客户端时，你可能会使用 `classToPlain` 方法将类实例转换回 POJOs，以便更容易地转换为 JSON 并传输。

总之，POJOs 是 JavaScript/TypeScript 编程中的基础概念之一，尤其是在涉及到数据交换和处理的时候。它们提供了灵活性和简洁性，同时保持了代码的清晰性和可维护性。