---
title: YAML
date: 2024-09-27
author: "pzc"
cover: /assets/images/jpg/47.jpg
categories: [yml]
---
YAML（YAML Ain't Markup Language）是一种人类可读的数据序列化语言。它通常用于配置文件、数据交换以及存储数据的场合。YAML的设计目标是使它易于阅读和编写，同时保持与诸如XML和JSON等其他数据格式的兼容性。YAML的核心特性包括简洁性、清晰性和强大的数据结构表达能力。

### YAML的基本语法

1. **缩进**：YAML使用缩进来表示层级关系。相同层级的元素需要对齐。缩进只能使用空格，不能使用制表符。

2. **键值对**：键值对通过冒号和空格分隔，例如 `key: value`。

3. **列表**：列表项前使用破折号加空格来表示，例如：
   ```
   - item1
   - item2
   ```

4. **映射**：映射是一组键值对的集合，例如：
   
   ```yaml
   key1: value1
   key2: value2
   ```
   
5. **多行字符串**：可以使用 `|` 或 `>` 来表示多行文本。`|` 会保留换行符，而 `>` 会将换行符转换为空格。
   
   ```yaml
   long_text: |
     这是一个
     多行字符串
   short_text: >
     这也是一个
     多行字符串，但是会被折叠成一行
   ```
   
6. **注释**：以 `#` 开头，表示注释，不会被解析器处理。

7. **锚点与别名**：可以使用 `&` 定义一个锚点，然后用 `*` 引用这个锚点，避免重复书写相同的值。
   ```yaml
   defaults: &defaults
     key1: value1
     key2: value2
   another_section:
     <<: *defaults
     key3: value3
   ```

8. **标签**：允许指定或改变节点的类型，例如：
   
   ```yaml
   explicit_integer: !!int "12"
   ```

### YAML的应用场景

- **配置文件**：许多软件和框架使用YAML作为配置文件格式，如Docker Compose、Kubernetes、Ansible等。
- **数据交换**：在不同系统之间交换数据时，YAML因其易读性而受到欢迎。
- **测试数据**：在开发过程中，YAML常用来定义测试数据。
- **API响应**：一些API选择返回YAML格式的数据，尤其是在原型设计阶段。

### 注意事项

虽然YAML非常强大且易于使用，但在某些情况下需要注意其潜在的陷阱，比如对于特殊字符的处理不当可能会导致解析错误。此外，由于YAML依赖于缩进，因此在编辑时需要特别小心，确保缩进的一致性。



### 高级特性

1. **合并键（Merge Key）**
   合并键允许你从一个映射中复制键值对到另一个映射中。这在处理多个配置文件时非常有用。
   
   ```yaml
   defaults: &defaults
     key1: value1
     key2: value2
   
   config1:
     <<: *defaults
     key3: value3
   
   config2:
     <<: *defaults
     key4: value4
   ```
   
2. **字面量块（Literal Block Scalars）**
   使用 `|` 可以保留文本中的所有换行符和空格。
   
   ```yaml
   literal_block: |
     这是一个
     字面量块
     换行和空格都会被保留
   ```
   
3. **折叠块（Folded Block Scalars）**
   使用 `>` 会将换行符转换为空格，连续的换行符会被转换为一个换行符。
   
   ```yaml
   folded_block: >
     这是一个
     折叠块
     换行符会被转换为空格
   ```
   
4. **流式风格（Flow Style）**
   流式风格允许你在一行内定义复杂的结构，适用于简单的数据结构。
   
   ```yaml
   inline_list: [item1, item2, item3]
   inline_map: {key1: value1, key2: value2}
   ```
   
5. **类型标签（Type Tags）**
   你可以显式地指定数据类型，以确保解析器正确处理数据。
   
   ```yaml
   explicit_int: !!int "123"
   explicit_float: !!float "123.45"
   explicit_null: !!null "null"
   ```
   
6. **布尔值**
   YAML 中有一些特定的字符串会被解析为布尔值。
   
   ```yaml
   true_values: [true, True, TRUE, on, On, ON, yes, Yes, YES]
   false_values: [false, False, FALSE, off, Off, OFF, no, No, NO]
   ```

### 常见问题和注意事项

1. **缩进一致性**
   缩进是 YAML 的核心，必须保持一致。使用空格而不是制表符，通常建议使用两个空格进行缩进。

2. **特殊字符**
   特殊字符（如 `!`, `&`, `*`, `?`, `:`, `-`, `,` 等）在 YAML 中有特殊含义，如果需要在字符串中使用这些字符，应使用引号包裹。

3. **多文档**
   一个 YAML 文件可以包含多个文档，每个文档之间用 `---` 分隔。
   
   ```yaml
   --- # 文档1
   key1: value1
   
   --- # 文档2
   key2: value2
   ```
   
4. **注释**
   注释以 `#` 开头，从 `#` 到行尾的所有内容都会被忽略。
   
   ```yaml
   key: value  # 这是一个注释
   ```
   
5. **默认值**
   如果一个键没有值，它会被解析为 `null`。
   ```yaml
   key:  # 等同于 key: null
   ```

### 工具和库

- **YAML Lint**：一个在线工具，可以帮助你检查 YAML 文件的语法。
- **PyYAML**：Python 的 YAML 解析库，广泛用于处理 YAML 文件。
- **SnakeYAML**：Java 的 YAML 解析库。
- **js-yaml**：JavaScript 的 YAML 解析库。

### 实际应用示例

#### Docker Compose 文件
```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
```

#### Kubernetes 配置文件
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: my-image:latest
    ports:
    - containerPort: 80
```

#### Ansible Playbook
```yaml
---
- hosts: all
  tasks:
  - name: Install httpd
    yum:
      name: httpd
      state: present
  - name: Start httpd service
    service:
      name: httpd
      state: started
```

### yml和yaml区别

YML 和 YAML 实际上指的是同一种数据序列化格式，它们之间的区别主要在于文件扩展名的不同。以下是详细的解释：

#### 文件扩展名

1. **YAML (.yaml)**
   - `.yaml` 是 YAML 文件的标准扩展名。
   - 这个扩展名更符合 YAML 的全称 "YAML Ain't Markup Language"。
   - 在大多数情况下，推荐使用 `.yaml` 扩展名，因为它更明确且广泛被各种工具和编辑器识别。

2. **YML (.yml)**
   - `.yml` 是 YAML 文件的另一种常见扩展名。
   - 这个扩展名较短，有时为了方便或出于历史原因被使用。
   - 在某些环境中，特别是早期的工具和系统中，`.yml` 更常见。

#### 兼容性和使用场景

- **工具支持**：大多数现代工具和编辑器都支持 `.yaml` 和 `.yml` 文件，但有些工具可能有默认偏好。例如，Docker Compose 默认使用 `.yml` 文件，而 Kubernetes 配置文件通常使用 `.yaml`。
- **社区惯例**：不同的社区和项目可能有不同的惯例。例如，Ruby on Rails 项目通常使用 `.yml`，而 Ansible 和 Kubernetes 项目通常使用 `.yaml`。
- **文件识别**：在某些情况下，文件扩展名可能会影响文件的识别和处理。例如，某些配置管理系统或 CI/CD 工具可能会根据文件扩展名来决定如何解析文件。
