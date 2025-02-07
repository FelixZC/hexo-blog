---
title: "Jest"
date: 2024-12-18
author: "pzc"
cover: /assets/images/jpg/128.jpg
categories: [nodejs]
tags: [Jest]
---
## 介绍

Jest 是一个现代的 JavaScript 测试框架，以其简单配置和丰富的功能而闻名。它最初由 Facebook 开发并维护，主要用于 React 应用程序的测试，但它同样适用于其他 JavaScript 项目。以下是 Jest 的一些关键特性和概念：

1. **零配置**：对于很多项目，Jest 可以自动找出测试文件并执行它们，无需过多配置。

2. **快照测试**：Jest 支持快照测试，这是一种记录组件输出的方式，并在未来的测试运行中确保该输出没有改变。这对于 UI 组件尤其有用。

3. **异步代码支持**：Jest 支持 Promises 和 async/await 语法，可以轻松测试异步代码。

4. **模拟（Mocking）**：提供了强大的模块和函数的模拟能力，使你能够控制依赖行为，隔离测试。

5. **内置 JSDOM**：Jest 内置了 JSDOM 环境，这使得浏览器环境下的代码可以在 Node.js 环境中运行和测试。

6. **并行测试执行**：为了加速测试过程，Jest 能够并行地运行测试。

7. **代码覆盖率报告**：Jest 可生成详细的代码覆盖率报告，帮助识别哪些部分的代码尚未被测试覆盖。

8. **匹配器（Matchers）**：提供了一套丰富的断言库，用于验证测试结果是否符合预期。

9. **交互式 watch 模式**：Jest 提供了一个交互式的命令行界面，可以只运行受影响的测试，加快开发速度。

10. **社区和文档**：拥有活跃的社区支持和详细的官方文档，方便学习和解决问题。

Jest 是一个非常适合前端开发者的工具，尤其是那些使用 React 或者其他 JavaScript 生态系统构建应用的人。由于其快速、易用和功能强大，它已经成为许多项目的首选测试框架。

## 资料

如果你正在寻找关于 Jest 更详细的资料，这里有一些资源可以帮助你深入学习和使用 Jest 测试框架：

1. **官方文档**：
   - [Jest 官方网站](https://jestjs.io/)
   - 这是获取最新信息的最佳来源，包括安装指南、配置选项、API 参考以及最佳实践。

2. **教程与指南**：
   - MDN Web Docs 提供了有关 JavaScript 测试的教程，虽然不专门针对 Jest，但可以提供很好的背景知识。
   - 各种在线编程教育平台如 freeCodeCamp, Udemy, Coursera 等可能有专门针对 Jest 的课程。

3. **书籍**：
   - 一些专注于 JavaScript 测试或全栈开发的书籍可能会涵盖 Jest 的使用。例如，《JavaScript Testing with Jest》是一本专注于此主题的书。

4. **博客文章和论坛**：
   - Medium、Dev.to 和其他技术博客经常会有开发者分享他们使用 Jest 的经验和技巧。

5. **GitHub 仓库**：
   - 许多开源项目会使用 Jest 进行测试，查看这些项目的代码库可以了解实际应用中的 Jest 使用方式。
   - Jest 自己的 GitHub 仓库也是一个重要的资源，它包含了项目的源代码、issue 跟踪器和贡献指南。

通过以上资源，你可以获得从基础到高级的所有必要信息来掌握 Jest，并将其应用于你的项目中。根据你的具体需求和学习风格选择最适合你的资源。

## 基础

让我们重新回到 Jest 的基础，确保你对如何开始使用 Jest 进行 JavaScript 测试有一个清晰的理解。

### 安装 Jest

首先，你需要在你的项目中安装 Jest。如果你使用的是 npm 或 yarn，可以通过以下命令安装：

```bash
# 使用 npm
npm install --save-dev jest

# 使用 yarn
yarn add --dev jest
```

### 创建第一个测试

创建一个简单的 JavaScript 文件来测试。比如，我们创建一个 `math.js` 文件，里面有一些基本的数学函数：

```javascript
// math.js
function add(a, b) {
  return a + b;
}

module.exports = { add };
```

然后，在同一个目录下或者在 `__tests__` 目录下创建一个对应的测试文件 `math.test.js`：

```javascript
// math.test.js
const { add } = require('./math');

test('adds 1 + 2 to equal 3', () => {
  expect(add(1, 2)).toBe(3);
});
```

在这个测试文件中，我们导入了 `add` 函数，并编写了一个简单的测试用例来验证 `1 + 2` 是否等于 `3`。`test` 函数是 Jest 提供的一个全局函数，用来定义测试用例。`expect` 和 `toBe` 是内置的匹配器（matcher），用来断言某个值是否符合预期。

### 运行测试

确保你的 `package.json` 包含一个用于运行测试的脚本命令：

```json
{
  "scripts": {
    "test": "jest"
  }
}
```

你可以通过以下命令来运行测试：

```bash
npm test
# 或者
npx jest
```

如果一切正常，你应该会看到类似如下输出，表示测试通过：

```
PASS  ./math.test.js
✓ adds 1 + 2 to equal 3 (5ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.234s
```

### Jest 的基础概念

- **测试套件（Test Suite）**：一组相关的测试用例。通常使用 `describe` 来分组。
- **测试用例（Test Case）**：单个测试，使用 `test` 或 `it` 来定义。
- **匹配器（Matchers）**：用于断言值的函数，例如 `toBe`, `toEqual`, `toContain` 等。
- **Mock Functions**：模拟函数行为，以便隔离测试。
- **快照测试（Snapshot Testing）**：记录组件或数据结构的输出，并在未来测试中对比。

### 示例：使用 `describe` 组织测试

```javascript
// math.test.js
const { add } = require('./math');

describe('Math functions', () => {
  test('adds 1 + 2 to equal 3', () => {
    expect(add(1, 2)).toBe(3);
  });

  // 可以添加更多测试...
});
```

这只是一个非常基础的介绍。希望这些信息能帮助你理解如何开始使用 Jest。

## 进阶

对于已经熟悉 Jest 基础的开发者，进阶介绍可以涵盖更复杂的特性和最佳实践，帮助你更加高效和灵活地使用 Jest 进行测试。以下是关于 Jest 的一些高级主题和技巧：

### 1. **自定义匹配器（Custom Matchers）**

Jest 内置了许多有用的匹配器，但有时你可能需要创建自己的匹配器来满足特定的需求。你可以通过 `expect.extend` 方法添加自定义匹配器。

```javascript
expect.extend({
  toBeWithinRange(received, floor, ceiling) {
    const pass = received >= floor && received <= ceiling;
    if (pass) {
      return {
        message: () => `expected ${received} not to be within range ${floor} - ${ceiling}`,
        pass: true,
      };
    } else {
      return {
        message: () => `expected ${received} to be within range ${floor} - ${ceiling}`,
        pass: false,
      };
    }
  },
});
```

### 2. **Mock 函数与模块**

- **手动 Mock**：你可以为模块或函数编写自己的 mock 实现。
- **自动 Mock**：Jest 可以自动 mock 模块，这对于测试时隔离依赖非常有用。
- **Spying on Functions**：使用 `jest.spyOn` 来监控函数调用，而不改变其行为。

```javascript
const myModule = require('./myModule');
jest.spyOn(myModule, 'myFunction').mockReturnValue('mocked value');
```

### 3. **异步代码测试**

- 使用 `async/await` 或 `.then()` 测试 Promises。
- 使用 `done` 回调确保异步操作完成。

```javascript
test('the data is peanut butter', async () => {
  await fetchData();
  expect(data).toBe('peanut butter');
});
```

### 4. **快照测试优化**

- 快照更新策略：了解如何安全地更新快照，避免不必要的变更。
- 使用 `toMatchSnapshot` 的选项参数，例如 `only` 和 `updateSnapshot`。

```javascript
expect(component.toJSON()).toMatchSnapshot({ mode: 'deep' });
```

### 5. **CI/CD 集成**

- 设置持续集成管道中的 Jest 测试。
- 使用 Jest 的覆盖率报告生成工具，并将其集成到 CI 管道中，确保代码质量。

## 示例

下面是一个使用 Jest 进行单元测试的完整示例，包括配置、测试代码和被测函数。我们将创建一个简单的 JavaScript 模块，并为其编写测试用例。

### 项目结构

```
my-project/
├── src/
│   └── calculator.js
├── __tests__/
│   └── calculator.test.js
├── package.json
└── jest.config.js (可选)
```

### 被测模块 (`src/calculator.js`)

```javascript
// src/calculator.js
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

function multiply(a, b) {
  return a * b;
}

function divide(a, b) {
  if (b === 0) {
    throw new Error('Division by zero is not allowed');
  }
  return a / b;
}

module.exports = { add, subtract, multiply, divide };
```

### 测试文件 (`__tests__/calculator.test.js`)

```javascript
// __tests__/calculator.test.js
const { add, subtract, multiply, divide } = require('../src/calculator');

describe('Calculator functions', () => {
  test('adds 1 + 2 to equal 3', () => {
    expect(add(1, 2)).toBe(3);
  });

  test('subtracts 5 - 2 to equal 3', () => {
    expect(subtract(5, 2)).toBe(3);
  });

  test('multiplies 4 * 5 to equal 20', () => {
    expect(multiply(4, 5)).toBe(20);
  });

  test('divides 8 / 2 to equal 4', () => {
    expect(divide(8, 2)).toBe(4);
  });

  test('throws an error when dividing by zero', () => {
    expect(() => divide(8, 0)).toThrow('Division by zero is not allowed');
  });
});
```

### 配置文件 (`jest.config.js`)（如果需要）

对于简单项目，Jest 的零配置特性通常足够了，但如果你想要定制化设置，可以添加一个配置文件：

```javascript
// jest.config.js
module.exports = {
  // 如果你有其他配置项，例如测试环境、转换器等，请在此处定义
  // 例如：
  // testEnvironment: 'node',
};
```

### `package.json`

确保你的 `package.json` 包含 Jest 作为开发依赖，并包含一个用于运行测试的脚本命令：

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "jest"
  },
  "devDependencies": {
    "jest": "^29.0.0" // 或者最新版本
  }
}
```

### 安装依赖

在项目根目录下运行以下命令来安装 Jest：

```bash
npm install --save-dev jest
```

### 执行测试

你可以通过 npm 或 npx 来运行测试：

```bash
npm test
# 或者
npx jest
```

### 结果

当你运行上述命令时，Jest 将会自动找到 `__tests__` 目录下的测试文件并执行它们。你应该看到类似如下的输出，表示所有测试都通过了：

```
PASS  __tests__/calculator.test.js
✓ adds 1 + 2 to equal 3 (5ms)
✓ subtracts 5 - 2 to equal 3
✓ multiplies 4 * 5 to equal 20
✓ divides 8 / 2 to equal 4
✓ throws an error when dividing by zero

Test Suites: 1 passed, 1 total
Tests:       5 passed, 5 total
Snapshots:   0 total
Time:        1.234s
```

这个例子展示了如何为一个简单的计算器模块编写单元测试。你可以根据自己的项目需求扩展这些测试，比如添加更复杂的逻辑、异步操作或者集成测试等。

## 注意事项

在使用 Jest 进行测试时，有一些注意事项可以帮助你避免常见错误，并确保测试代码的健壮性和可维护性。以下是几个关键点：

### 1. **保持测试独立**

- **避免全局状态**：确保每个测试都是独立的，不依赖于其他测试的状态或顺序执行。
- **清理副作用**：使用 `beforeEach` 和 `afterEach` 来设置和清除测试环境，防止不同测试之间产生干扰。

```javascript
beforeEach(() => {
  // 设置测试前的准备工作
});

afterEach(() => {
  // 清理工作，例如重置 mock 函数
});
```

### 2. **合理使用 Mock**

- **适度模拟**：只模拟必要的依赖，不要过度模拟导致测试难以理解和维护。
- **恢复默认行为**：使用 `jest.restoreAllMocks()` 在测试后恢复所有被模拟的行为，以确保测试间的隔离性。

```javascript
afterEach(() => {
  jest.restoreAllMocks();
});
```

### 3. **异步代码测试**

- **正确处理 Promise**：确保所有的异步操作都被正确等待完成，可以使用 `async/await` 或 `.then()`.
- **超时设置**：对于长时间运行的测试，考虑增加超时时间以避免不必要的失败。

```javascript
test('the data is peanut butter', async () => {
  await fetchData();
  expect(data).toBe('peanut butter');
}, 10000); // 第二个参数是超时时间（毫秒）
```

### 4. **快照测试谨慎使用**

- **审查快照更新**：当快照发生变化时，仔细检查变化是否合理，避免因为 UI 改动而频繁更新快照。
- **快照文件管理**：定期审查和整理快照文件，删除不再需要的快照。

### 5. **避免过于复杂的测试**

- **单职责原则**：每个测试应只验证一个逻辑点，不要试图在一个测试中覆盖多个场景。
- **测试粒度**：编写单元测试时尽量保持细粒度，针对函数或方法级别的测试，而不是整个模块。

### 6. **代码覆盖率报告**

- **关注未覆盖区域**：利用 Jest 提供的覆盖率报告来识别未被测试到的代码路径，并补充相应的测试用例。
- **不过分追求覆盖率**：高覆盖率并不总是意味着高质量的测试，重要的是测试的有效性和针对性。

通过遵守这些注意事项，你可以编写更可靠、更易维护的测试代码，从而提升整体软件质量。
