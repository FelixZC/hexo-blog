---
title: Mongoose
date: 2024-12-01
author: "pzc"
cover: /assets/images/jpg/85.jpg
categories: [sql]
tags: [Database]
---
## 介绍

Mongoose 是一个Node.js的库，用于与MongoDB数据库进行交互。它提供了一种直观、简洁的方式来定义对象模型，执行数据库查询，并处理文档之间的关系。通过Mongoose，开发者可以更方便地操作MongoDB中的数据，而不需要直接编写复杂的MongoDB驱动程序代码。

Mongoose的主要特点包括：

1. **Schema定义**：允许你定义你的数据结构，类似于其他编程语言中的类定义。你可以指定字段类型、默认值、验证规则等。
2. **Model创建**：基于Schema创建Model，Model是构造函数，用来创建和保存实例到MongoDB。
3. **Middleware支持**：在保存或更新数据前后执行自定义逻辑。
4. **Populate功能**：简化了文档间关联的操作，比如一对多或多对多的关系。
5. **Query Building**：提供了链式API来构建复杂的查询条件。
6. **插件系统**：可以通过插件扩展Mongoose的功能。

如果你想要开始使用Mongoose，首先需要安装它（通常通过npm）：
```bash
npm install mongoose
```

然后，可以在你的项目中引入并连接到MongoDB：
```javascript
const mongoose = require('mongoose');

// 连接到本地MongoDB服务器
mongoose.connect('mongodb://localhost:27017/mydatabase', {
  useNewUrlParser: true,
  useUnifiedTopology: true
}).then(() => console.log('Connected to MongoDB...'))
  .catch(err => console.error('Could not connect to MongoDB...', err));

// 定义Schema
const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  tags: [String],
  date: { type: Date, default: Date.now },
  isPublished: Boolean
});

// 创建Model
const Course = mongoose.model('Course', courseSchema);

// 使用Model
async function createCourse() {
  const course = new Course({
    name: 'React Course',
    author: 'John Doe',
    tags: ['frontend', 'javascript'],
    isPublished: true
  });

  try {
    const result = await course.save();
    console.log(result);
  } catch (ex) {
    console.error(ex);
  }
}

createCourse();
```

这段代码展示了如何设置Mongoose的基本配置、定义一个简单的Schema、创建对应的Model以及如何使用这个Model来添加新数据到数据库中。Mongoose非常适合于那些希望以一种更加面向对象的方式与MongoDB工作的Node.js开发者。



## 和MongoDB 关系

Mongoose 与 MongoDB 之间的关系可以这样理解：Mongoose 是一个面向对象的库，它构建于官方的 MongoDB Node.js 驱动之上，为开发者提供了一种更直观的方式来定义模型、执行查询和处理文档。简而言之，Mongoose 提供了一个更高层次的抽象层来简化与MongoDB数据库的交互。



### 使用场景

当直接使用 MongoDB 的 Node.js 驱动时，你需要手动管理很多细节，比如连接池、错误处理、模式验证等。而 Mongoose 通过其提供的工具和方法帮助开发者更容易地完成这些任务，特别适合于那些希望以一种更加面向对象的方式工作的开发者。

### 关系总结

- **依赖性**：Mongoose 依赖于 MongoDB Node.js 驱动来执行底层操作。
- **抽象层**：Mongoose 在 MongoDB 基础上提供了一个额外的抽象层，简化了应用开发过程中的数据库操作。
- **可选性**：虽然 Mongoose 很受欢迎且强大，但并不是所有项目都需要它。对于一些简单的应用或者需要更高性能的情况，直接使用 MongoDB 的驱动可能更为合适。

总之，Mongoose 是 MongoDB 的一个辅助工具，它让开发者能够以一种更高效、更有组织的方式与 MongoDB 进行交互。如果你正在寻找一种方式来快速搭建你的Node.js应用程序，并且需要丰富的数据建模功能，那么Mongoose会是一个不错的选择。



## 官方资料

Mongoose 的官方资料是学习和使用 Mongoose 的最佳资源。以下是一些关键的官方文档和资源链接，可以帮助你深入了解 Mongoose 的功能和用法：

1. **官方网站**：
   - Mongoose 官方网站：[mongoosejs.com](https://mongoosejs.com/)
   - 这里提供了最新的文档、教程、API 参考以及社区支持。
2. **官方文档**：
   - [Mongoose 官方文档](https://mongoosejs.com/docs/) 是非常全面的学习资源，它涵盖了从安装到高级特性的所有内容。
   - 文档中包括了安装指南、Schema 和 Model 的定义、CRUD 操作、查询构建、中间件、数据验证、引用与关联、聚合查询等主题。
3. **API 参考**：
   - [Mongoose API 参考](https://mongoosejs.com/docs/api.html) 提供了详细的 API 说明，对于需要深入理解每个方法和属性的人来说非常有用。
5. **插件**：
   - [Mongoose 插件](https://mongoosejs.com/docs/plugins.html) 页面介绍了如何使用和创建插件来扩展 Mongoose 功能。
6. **常见问题（FAQ）**：
   - [Mongoose FAQ](https://mongoosejs.com/docs/faq.html) 列出了一些常见的问题及其解答，对于解决日常遇到的问题很有帮助。
7. **GitHub 仓库**：
   - [Mongoose GitHub 仓库](https://github.com/Automattic/mongoose) 不仅可以查看源码，还可以提交问题或贡献代码。
8. **社区论坛**：
   - [Stack Overflow 上的 Mongoose 标签](https://stackoverflow.com/questions/tagged/mongoose) 是一个很好的地方，你可以在这里找到许多关于 Mongoose 的问题和答案。
   - [Mongoose Google Group](https://groups.google.com/g/mongoose-orm) 也是一个活跃的讨论社区。

通过这些官方资源，你可以获得有关 Mongoose 的最新信息和支持。如果你有任何具体的技术问题或者需要进一步的帮助，也可以访问这些资源或直接询问我。



## 完整使用示例

下面是一个使用 Mongoose 的完整示例，它将展示如何设置一个简单的 Node.js 应用程序来连接到 MongoDB 数据库，并执行一些基本的 CRUD（创建、读取、更新、删除）操作。这个例子假设你已经安装了 Node.js 和 MongoDB。

### 1. 安装必要的依赖

首先，确保你的项目中安装了 `express` 和 `mongoose`。你可以通过 npm 来安装这些包：

```bash
npm init -y
npm install express mongoose
```

### 2. 创建服务器并连接到 MongoDB

接下来，我们将创建一个简单的 Express 服务器，并使用 Mongoose 连接到 MongoDB。

```javascript
// server.js
const express = require('express');
const mongoose = require('mongoose');

const app = express();
app.use(express.json()); // 使用 JSON 中间件

// 连接到 MongoDB
mongoose.connect('mongodb://localhost:27017/mydatabase', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  useCreateIndex: true,
  useFindAndModify: false
}).then(() => console.log('Connected to MongoDB...'))
  .catch(err => console.error('Could not connect to MongoDB...', err));

// 定义 Schema
const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  tags: [String],
  date: { type: Date, default: Date.now },
  isPublished: Boolean
});

// 创建 Model
const Course = mongoose.model('Course', courseSchema);

// CRUD 操作
app.post('/api/courses', async (req, res) => {
  const course = new Course(req.body);
  try {
    await course.save();
    res.send(course);
  } catch (error) {
    res.status(400).send(error.message);
  }
});

app.get('/api/courses', async (req, res) => {
  try {
    const courses = await Course.find();
    res.send(courses);
  } catch (error) {
    res.status(500).send(error.message);
  }
});

app.put('/api/courses/:id', async (req, res) => {
  try {
    const course = await Course.findByIdAndUpdate(req.params.id, req.body, { new: true });
    if (!course) return res.status(404).send('No course found with the given ID.');
    res.send(course);
  } catch (error) {
    res.status(400).send(error.message);
  }
});

app.delete('/api/courses/:id', async (req, res) => {
  try {
    const course = await Course.findByIdAndDelete(req.params.id);
    if (!course) return res.status(404).send('No course found with the given ID.');
    res.send(course);
  } catch (error) {
    res.status(500).send(error.message);
  }
});

// 启动服务器
const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Listening on port ${port}...`));
```

### 3. 运行应用程序

在终端中运行以下命令来启动你的应用：

```bash
node server.js
```

现在，你应该能够通过访问 `http://localhost:3000/api/courses` 来与你的 API 交互。你可以使用 Postman 或者任何 HTTP 客户端来测试这些 API 端点。

### 4. 测试 API

- **创建课程**：发送 POST 请求到 `/api/courses`，请求体可以是：
  ```json
  {
    "name": "React Course",
    "author": "John Doe",
    "tags": ["frontend", "javascript"],
    "isPublished": true
  }
  ```

- **获取所有课程**：发送 GET 请求到 `/api/courses`。

- **更新课程**：发送 PUT 请求到 `/api/courses/{id}`，其中 `{id}` 是你想更新的课程ID，请求体可以包含任何需要更新的字段。

- **删除课程**：发送 DELETE 请求到 `/api/courses/{id}`，其中 `{id}` 是你想删除的课程ID。

这个示例展示了如何使用 Mongoose 在 Node.js 中构建一个简单的 RESTful API。

## 进阶

当你已经掌握了 Mongoose 的基本使用方法后，可以进一步探索一些进阶功能，以提高你的应用程序的效率和功能性。以下是一些进阶特性和最佳实践：

### 1. **虚拟属性（Virtuals）**
虚拟属性是不存储在数据库中的属性，但可以在模型实例上访问。这在需要基于现有数据计算新值时非常有用。

```javascript
const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  date: { type: Date, default: Date.now },
  isPublished: Boolean
});

courseSchema.virtual('info').get(function() {
  return `${this.name} by ${this.author}`;
});

const Course = mongoose.model('Course', courseSchema);
```

### 2. **中间件（Middleware）**
Mongoose 提供了多种类型的中间件，包括预处理和后处理中间件，用于在保存或更新文档前后执行自定义逻辑。

```javascript
// 预处理中间件
courseSchema.pre('save', function(next) {
  if (this.isNew) {
    this.date = Date.now();
  }
  next();
});

// 后处理中间件
courseSchema.post('save', function(doc) {
  console.log(`Document saved: ${doc._id}`);
});
```

### 3. **验证（Validation）**
利用 Mongoose 内置的验证机制来确保数据的一致性和完整性。

```javascript
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    minlength: 3,
    maxlength: 50
  },
  email: {
    type: String,
    required: true,
    unique: true,
    validate: {
      validator: function(v) {
        return /^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/.test(v);
      },
      message: 'Please enter a valid email'
    }
  }
});

const User = mongoose.model('User', userSchema);
```

### 4. **聚合管道（Aggregation Pipelines）**
利用 MongoDB 的强大聚合框架来进行复杂的数据分析和转换。

```javascript
Course.aggregate([
  { $match: { isPublished: true } },
  { $group: { _id: '$author', count: { $sum: 1 } } },
  { $sort: { count: -1 } }
]).then(result => {
  console.log(result);
}).catch(err => {
  console.error(err);
});
```

### 5. **引用与关联（References and Populating）**
通过引用和填充来管理文档间的关联关系。

```javascript
const authorSchema = new mongoose.Schema({ name: String });
const Author = mongoose.model('Author', authorSchema);

const courseSchema = new mongoose.Schema({
  name: String,
  author: { type: mongoose.Schema.Types.ObjectId, ref: 'Author' }
});

const Course = mongoose.model('Course', courseSchema);

// 创建一个作者
const author = new Author({ name: 'John Doe' });
await author.save();

// 创建一个课程并关联到作者
const course = new Course({ name: 'React Course', author: author._id });
await course.save();

// 查询课程并填充作者信息
Course.findOne({ name: 'React Course' })
  .populate('author')
  .then(course => {
    console.log(course);
  }).catch(err => {
    console.error(err);
  });
```

### 6. **分页与排序（Pagination and Sorting）**
实现分页和排序功能，以优化大量数据的展示。

```javascript
app.get('/api/courses', async (req, res) => {
  const page = parseInt(req.query.page) || 1;
  const limit = parseInt(req.query.limit) || 10;
  const skip = (page - 1) * limit;

  try {
    const courses = await Course.find()
      .skip(skip)
      .limit(limit)
      .sort({ date: -1 }); // 按日期降序排序
    res.send(courses);
  } catch (error) {
    res.status(500).send(error.message);
  }
});
```

### 7. **性能优化**
- 使用 `lean()` 方法来获取纯 JavaScript 对象，而不是 Mongoose 文档，以减少内存占用。
- 确保索引被正确设置，特别是在经常查询的字段上。
- 尽量避免使用 `.find()` 和 `.update()` 的 `{}` 来匹配所有文档，而是指定具体的查询条件。

### 8. **安全性**
- 在生产环境中使用环境变量来管理敏感信息，如数据库连接字符串。
- 使用 HTTPS 来保护数据传输过程中的安全。
- 对用户输入进行严格的验证和清理，防止 SQL 注入等攻击。

这些进阶特性可以帮助你构建更加强大和高效的应用程序。

## 补充

我们可以进一步补充一些关于 Mongoose 的进阶内容，以帮助你更好地理解和使用这个强大的库。以下是一些额外的进阶特性和最佳实践：

### 1. **自定义方法（Methods）和静态方法（Statics）**

- **实例方法**：你可以为文档实例添加自定义方法，这些方法可以在任何模型实例上调用。
- **静态方法**：这些是直接在模型类上定义的方法，可以通过模型本身调用。

```javascript
const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  date: { type: Date, default: Date.now },
  isPublished: Boolean
});

// 实例方法
courseSchema.methods.getInfo = function() {
  return `${this.name} by ${this.author}`;
};

// 静态方法
courseSchema.statics.findByName = function(name) {
  return this.find({ name: new RegExp(name, 'i') });
};

const Course = mongoose.model('Course', courseSchema);

// 使用实例方法
const course = new Course({ name: 'React Course', author: 'John Doe' });
console.log(course.getInfo()); // 输出: React Course by John Doe

// 使用静态方法
Course.findByName('React')
  .then(courses => console.log(courses))
  .catch(err => console.error(err));
```

### 2. **查询助手（Query Helpers）**

Mongoose 允许你为查询对象添加自定义方法，这可以简化常见查询模式。

```javascript
courseSchema.query.byAuthor = function(author) {
  return this.where({ author: new RegExp(author, 'i') });
};

// 使用查询助手
Course.find().byAuthor('John Doe').exec()
  .then(courses => console.log(courses))
  .catch(err => console.error(err));
```

### 3. **嵌套子文档（Nested Subdocuments）**

有时你需要在文档中嵌入其他文档。Mongoose 支持这种嵌套结构。

```javascript
const reviewSchema = new mongoose.Schema({
  rating: Number,
  comment: String,
  createdAt: { type: Date, default: Date.now }
});

const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  reviews: [reviewSchema]
});

const Course = mongoose.model('Course', courseSchema);

// 添加一个评论
const course = await Course.findById(someCourseId);
course.reviews.push({ rating: 5, comment: 'Great course!' });
await course.save();
```

### 4. **预处理和后处理中间件（Pre and Post Hooks）**

除了 `save` 中间件，你还可以为其他操作设置中间件，如 `findOneAndUpdate`, `remove` 等。

```javascript
courseSchema.pre('findOneAndUpdate', function(next) {
  this.options.runValidators = true; // 在更新时运行验证
  next();
});

courseSchema.post('remove', function(doc) {
  console.log(`Document removed: ${doc._id}`);
});
```

### 5. **索引（Indexes）**

为了提高查询性能，你可以在经常查询的字段上创建索引。

```javascript
const courseSchema = new mongoose.Schema({
  name: String,
  author: String,
  tags: [String],
  date: { type: Date, default: Date.now },
  isPublished: Boolean
}, {
  indexes: [
    { fields: { name: 1 }, options: { unique: true } },
    { fields: { author: 1, 'tags.0': 1 }, options: { sparse: true } }
  ]
});
```

### 6. **插件（Plugins）**

Mongoose 提供了丰富的插件系统，可以扩展其功能。例如，`mongoose-autopopulate` 插件可以帮助自动填充引用。

```bash
npm install mongoose-autopopulate
```

```javascript
const autopopulate = require('mongoose-autopopulate');

const courseSchema = new mongoose.Schema({
  name: String,
  author: { type: mongoose.Schema.Types.ObjectId, ref: 'Author', autopopulate: true }
});

courseSchema.plugin(autopopulate);

const Course = mongoose.model('Course', courseSchema);
```

### 7. **事务（Transactions）**

如果你需要执行多个操作并确保它们要么全部成功，要么全部失败，可以使用事务。

```javascript
const session = await mongoose.startSession();
session.startTransaction();

try {
  const course = new Course({ name: 'New Course', author: 'John Doe' });
  await course.save({ session });

  const user = new User({ name: 'New User' });
  await user.save({ session });

  await session.commitTransaction();
} catch (error) {
  await session.abortTransaction();
  throw error;
} finally {
  session.endSession();
}
```

### 8. **错误处理和日志记录**

在生产环境中，良好的错误处理和日志记录机制是必不可少的。

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});

// 使用 winston 或其他日志库来记录日志
const winston = require('winston');
const logger = winston.createLogger({
  transports: [
    new winston.transports.Console(),
    new winston.transports.File({ filename: 'combined.log' })
  ]
});

app.use((req, res, next) => {
  logger.info(`${req.method} ${req.url}`);
  next();
});
```

通过这些进阶特性，你可以构建更复杂、更高效的应用程序。

## 查询模式

Mongoose 提供了丰富的查询模式，可以帮助你更高效地与 MongoDB 进行交互。以下是一些常用的查询模式和示例：

### 1. **基本查询**
- **查找所有文档**：
  
  ```javascript
  Course.find().then(courses => console.log(courses));
  ```
  
- **根据条件查找文档**：
  ```javascript
  Course.find({ isPublished: true }).then(courses => console.log(courses));
  ```

- **根据 ID 查找单个文档**：
  ```javascript
  Course.findById(someCourseId).then(course => console.log(course));
  ```

- **使用 OR 查询**：
  ```javascript
  Course.find({ $or: [{ name: 'React' }, { author: 'John Doe' }] })
    .then(courses => console.log(courses));
  ```

### 2. **分页与排序**
- **分页**：
  ```javascript
  const page = 1;
  const limit = 10;
  const skip = (page - 1) * limit;
  
  Course.find()
    .skip(skip)
    .limit(limit)
    .then(courses => console.log(courses));
  ```

- **排序**：
  ```javascript
  Course.find()
    .sort({ date: -1 }) // 按日期降序排序
    .then(courses => console.log(courses));
  ```

### 3. **聚合查询**
- **简单的聚合**：
  ```javascript
  Course.aggregate([
    { $match: { isPublished: true } },
    { $group: { _id: '$author', count: { $sum: 1 } } },
    { $sort: { count: -1 } }
  ]).then(result => {
    console.log(result);
  });
  ```

- **使用管道操作符**：
  ```javascript
  Course.aggregate([
    { $match: { isPublished: true } },
    { $project: { name: 1, author: 1, _id: 0 } },
    { $sort: { name: 1 } }
  ]).then(result => {
    console.log(result);
  });
  ```

### 4. **嵌套查询**
- **查找并填充关联文档**（假设 `Course` 和 `Author` 之间有引用关系）：
  ```javascript
  Course.find()
    .populate('author') // 假设 author 字段是一个 ObjectId 引用
    .then(courses => console.log(courses));
  ```

- **多级填充**：
  ```javascript
  Course.find()
    .populate({
      path: 'author',
      populate: {
        path: 'department'
      }
    })
    .then(courses => console.log(courses));
  ```

### 5. **条件查询**
- **比较操作符**：
  ```javascript
  Course.find({ rating: { $gt: 4 } }) // 查找评分大于 4 的课程
    .then(courses => console.log(courses));
  
  Course.find({ rating: { $gte: 4, $lte: 5 } }) // 查找评分在 4 到 5 之间的课程
    .then(courses => console.log(courses));
  ```

- **逻辑操作符**：
  ```javascript
  Course.find({ $and: [{ isPublished: true }, { rating: { $gt: 4 } }] })
    .then(courses => console.log(courses));
  
  Course.find({ $or: [{ isPublished: true }, { rating: { $gt: 4 } }] })
    .then(courses => console.log(courses));
  ```

- **存在性检查**：
  ```javascript
  Course.find({ tags: { $exists: true } }) // 查找有 tags 字段的文档
    .then(courses => console.log(courses));
  ```

### 6. **文本搜索**
- **全文搜索**：
  ```javascript
  Course.createIndexes({ title: 'text' }); // 创建全文索引
  
  Course.find({ $text: { $search: 'react' } })
    .then(courses => console.log(courses));
  ```

### 7. **更新查询**
- **更新单个文档**：
  ```javascript
  Course.findByIdAndUpdate(someCourseId, { $set: { isPublished: false } }, { new: true })
    .then(updatedCourse => console.log(updatedCourse));
  ```

- **批量更新**：
  ```javascript
  Course.updateMany({ isPublished: false }, { $set: { isPublished: true } })
    .then(result => console.log(result));
  ```

- **原子更新**（如递增、添加到数组等）：
  ```javascript
  Course.findByIdAndUpdate(someCourseId, { $inc: { views: 1 } }, { new: true })
    .then(updatedCourse => console.log(updatedCourse));
  
  Course.findByIdAndUpdate(someCourseId, { $push: { tags: 'new tag' } }, { new: true })
    .then(updatedCourse => console.log(updatedCourse));
  ```

### 8. **删除查询**
- **删除单个文档**：
  ```javascript
  Course.findByIdAndDelete(someCourseId)
    .then(deletedCourse => console.log(deletedCourse));
  ```

- **批量删除**：
  
  ```javascript
  Course.deleteMany({ isPublished: false })
    .then(result => console.log(result));
  ```

这些查询模式覆盖了 Mongoose 中最常见的操作。通过组合这些模式，你可以构建出非常强大且灵活的数据查询功能。

## 注意事项

在使用 Mongoose 进行数据库操作时，有一些重要的注意事项可以帮助你避免常见的陷阱，并确保你的应用程序更加健壮和高效。以下是一些关键的注意事项：

### 1. **连接管理**
- **单一连接实例**：确保在整个应用中只创建一个 Mongoose 连接实例。多次连接可能会导致资源浪费。
- **错误处理**：始终为连接添加错误处理逻辑，以确保在连接失败时能够正确处理。
- **关闭连接**：在应用退出时，确保关闭 Mongoose 连接，以释放资源。

```javascript
// 单一连接实例
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydatabase', {
  useNewUrlParser: true,
  useUnifiedTopology: true
}).then(() => console.log('Connected to MongoDB...'))
  .catch(err => console.error('Could not connect to MongoDB...', err));

// 在应用退出时关闭连接
process.on('SIGINT', () => {
  mongoose.connection.close(() => {
    console.log('Mongoose connection closed due to application termination');
    process.exit(0);
  });
});
```

### 2. **模式验证（Schema Validation）**
- **定义清晰的模式**：确保你的 Schema 定义清晰且包含所有必要的字段和验证规则。
- **使用内置验证器**：利用 Mongoose 内置的验证器来确保数据的一致性和完整性。
- **自定义验证器**：对于复杂验证需求，可以编写自定义验证函数。

```javascript
const courseSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    minlength: 3,
    maxlength: 50
  },
  author: {
    type: String,
    required: true
  },
  isPublished: Boolean,
  tags: [String]
});

// 自定义验证
courseSchema.path('name').validate(function(value) {
  return value.toLowerCase() !== 'test';
}, 'Name cannot be "test"');

const Course = mongoose.model('Course', courseSchema);
```

### 3. **查询性能**
- **索引**：为经常查询的字段创建索引，以提高查询性能。
- **分页**：使用 `skip` 和 `limit` 来实现分页，但注意 `skip` 的性能问题，特别是在大数据集上。
- **投影**：使用 `$project` 操作符来限制返回的字段，减少传输的数据量。

```javascript
// 创建索引
courseSchema.index({ name: 1, author: 1 });

// 分页查询
const page = 1;
const limit = 10;
const skip = (page - 1) * limit;

Course.find()
  .skip(skip)
  .limit(limit)
  .then(courses => console.log(courses));

// 投影
Course.find({}, { name: 1, author: 1, _id: 0 })
  .then(courses => console.log(courses));
```

### 4. **安全性**
- **防止注入攻击**：不要直接将用户输入传递给查询条件，而是使用参数化查询或正则表达式。
- **数据加密**：对于敏感信息（如密码），使用加密技术存储。
- **环境变量**：将数据库连接字符串等敏感信息存储在环境变量中，而不是硬编码在代码里。

```javascript
// 使用环境变量
const dbUrl = process.env.DB_URL || 'mongodb://localhost:27017/mydatabase';
mongoose.connect(dbUrl, {
  useNewUrlParser: true,
  useUnifiedTopology: true
});

// 防止注入攻击
const searchQuery = req.query.search;
Course.find({ name: { $regex: new RegExp(searchQuery, 'i') } })
  .then(courses => console.log(courses));
```

通过遵循这些注意事项，你可以确保你的 Mongoose 应用程序更加健壮、安全和高效。