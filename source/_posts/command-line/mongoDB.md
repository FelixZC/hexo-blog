---
title: MongoDB命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Database]
---
以下是 MongoDB 的常用命令大全，涵盖了包括数据库和集合管理、文档操作、聚合查询、索引管理等。介绍了聚合查询的基础和高级操作符，以及数据库的备份、恢复、安全、监控、性能优化、日志管理等。这些命令对 MongoDB 的有效管理至关重要。

### 数据库管理

#### 显示所有数据库
```bash
show dbs
```

#### 切换或创建数据库
```bash
use <database_name>
```

#### 查看当前数据库
```bash
db
```

#### 删除数据库
```bash
db.dropDatabase()
```

### 集合操作

#### 显示当前数据库的所有集合
```bash
show collections
```

#### 创建集合
```bash
db.createCollection(<collection_name>)
```

#### 删除集合
```bash
db.<collection_name>.drop()
```

### 文档操作

#### 插入文档

- 插入单个文档
  ```bash
  db.<collection_name>.insertOne({ key: value })
  ```

- 插入多个文档
  ```bash
  db.<collection_name>.insertMany([{ key1: value1 }, { key2: value2 }])
  ```

#### 查询文档

- 查找所有文档
  ```bash
  db.<collection_name>.find().pretty()
  ```

- 查找特定条件的文档
  ```bash
  db.<collection_name>.find({ key: value }).pretty()
  ```

- 查找单个文档
  ```bash
  db.<collection_name>.findOne({ key: value })
  ```

- 分页查询
  ```bash
  db.<collection_name>.find().skip(10).limit(10)
  ```

- 排序
  ```bash
  db.<collection_name>.find().sort({ key: 1 })  # 升序
  db.<collection_name>.find().sort({ key: -1 }) # 降序
  ```

#### 更新文档

- 更新单个文档
  ```bash
  db.<collection_name>.updateOne({ key: value }, { $set: { new_key: new_value } })
  ```

- 更新多个文档
  ```bash
  db.<collection_name>.updateMany({ key: value }, { $set: { new_key: new_value } })
  ```

- 替换文档
  ```bash
  db.<collection_name>.replaceOne({ key: value }, { new_key: new_value })
  ```

#### 删除文档

- 删除单个文档
  ```bash
  db.<collection_name>.deleteOne({ key: value })
  ```

- 删除多个文档
  ```bash
  db.<collection_name>.deleteMany({ key: value })
  ```

### 聚合查询

#### 基本聚合
```bash
db.<collection_name>.aggregate([
  { $match: { key: value } },
  { $group: { _id: "$key", count: { $sum: 1 } } }
])
```

#### 分组和聚合
```bash
db.<collection_name>.aggregate([
  { $match: { key: value } },
  { $group: { _id: "$key", total: { $sum: "$value" } } },
  { $sort: { total: -1 } },
  { $limit: 10 }
])

```
### 聚合框架
当然可以！以下是 MongoDB 聚合框架中常用的命令和阶段的详细列表。这些命令可以帮助你实现各种复杂的数据处理和分析任务。

### 常用阶段

1. **`$match`**：用于过滤文档，类似于 SQL 中的 `WHERE` 子句。
   ```javascript
   { $match: { key: value } }
   ```

2. **`$project`**：用于选择或计算字段，类似于 SQL 中的 `SELECT` 子句。
   ```javascript
   { $project: { field1: 1, field2: 0, newField: { $add: ["$field1", "$field2"] } } }
   ```

3. **`$group`**：用于对文档进行分组，类似于 SQL 中的 `GROUP BY` 子句。
   ```javascript
   { $group: { _id: "$field", count: { $sum: 1 } } }
   ```

4. **`$sort`**：用于对结果进行排序，类似于 SQL 中的 `ORDER BY` 子句。
   ```javascript
   { $sort: { field: 1 } }  // 升序
   { $sort: { field: -1 } } // 降序
   ```

5. **`$limit`**：用于限制返回的文档数量，类似于 SQL 中的 `LIMIT` 子句。
   ```javascript
   { $limit: 10 }
   ```

6. **`$skip`**：用于跳过指定数量的文档，类似于 SQL 中的 `OFFSET` 子句。
   ```javascript
   { $skip: 10 }
   ```

7. **`$lookup`**：用于在两个集合之间进行左外连接，类似于 SQL 中的 `LEFT JOIN`。
   ```javascript
   { $lookup: { from: "other_collection", localField: "local_key", foreignField: "foreign_key", as: "new_field" } }
   ```

8. **`$unwind`**：用于展开数组字段，将每个数组元素生成一个新的文档。
   ```javascript
   { $unwind: "$array_field" }
   ```

9. **`$redact`**：用于根据条件对文档进行细粒度的控制，类似于 SQL 中的 `CASE` 语句。
   ```javascript
   { $redact: { $cond: { if: { $eq: [ "$age", 30 ] }, then: "$$KEEP", else: "$$PRUNE" } } }
   ```

10. **`$addFields`**：用于添加新的字段或修改现有字段。
    ```javascript
    { $addFields: { newField: { $add: ["$field1", "$field2"] } } }
    ```

11. **`$bucket`**：用于将文档分组到指定的桶中。
    ```javascript
    { $bucket: { groupBy: "$field", boundaries: [0, 10, 20, 30], default: "other", output: { count: { $sum: 1 } } } }
    ```

12. **`$bucketAuto`**：用于自动将文档分组到指定数量的桶中。
    ```javascript
    { $bucketAuto: { groupBy: "$field", buckets: 5, output: { count: { $sum: 1 } } } }
    ```

13. **`$facet`**：用于在一个聚合管道中执行多个聚合子管道。
    ```javascript
    { $facet: { facet1: [ { $match: { key: value } } ], facet2: [ { $group: { _id: "$field", count: { $sum: 1 } } } ] } }
    ```

14. **`$graphLookup`**：用于在图数据中进行递归查找。
    ```javascript
    { $graphLookup: { from: "collection", startWith: "$startField", connectFromField: "connectField", connectToField: "connectToField", as: "resultField" } }
    ```

15. **`$indexStats`**：用于获取集合的索引统计信息。
    ```javascript
    { $indexStats: {} }
    ```

16. **`$out`**：用于将聚合结果输出到另一个集合。
    ```javascript
    { $out: "output_collection" }
    ```

17. **`$merge`**：用于将聚合结果合并到另一个集合。
    ```javascript
    { $merge: { into: "output_collection", on: "_id", whenMatched: "replace", whenNotMatched: "insert" } }
    ```

18. **`$replaceRoot`**：用于替换根文档。
    ```javascript
    { $replaceRoot: { newRoot: "$field" } }
    ```

19. **`$replaceWith`**：用于替换整个文档。
    ```javascript
    { $replaceWith: { newField: "$field" } }
    ```

20. **`$sample`**：用于随机抽样文档。
    ```javascript
    { $sample: { size: 10 } }
    ```

21. **`$set`**：用于设置字段值。
    ```javascript
    { $set: { newField: { $add: ["$field1", "$field2"] } } }
    ```

22. **`$unset`**：用于移除字段。
    ```javascript
    { $unset: "field" }
    ```

23. **`$unionWith`**：用于将两个集合的结果合并在一起。
    ```javascript
    { $unionWith: "other_collection" }
    ```

### 常用操作符

1. **算术操作符**：
   - `$add`：加法
   - `$subtract`：减法
   - `$multiply`：乘法
   - `$divide`：除法
   - `$mod`：取模

2. **数组操作符**：
   - `$arrayElemAt`：获取数组中的指定元素
   - `$concatArrays`：连接多个数组
   - `$filter`：过滤数组
   - `$reduce`：对数组进行累加操作
   - `$size`：获取数组的长度
   - `$slice`：切片数组

3. **条件操作符**：
   - `$cond`：条件判断
   - `$ifNull`：如果字段为空则返回默认值
   - `$switch`：多条件判断

4. **比较操作符**：
   - `$eq`：等于
   - `$gt`：大于
   - `$gte`：大于等于
   - `$lt`：小于
   - `$lte`：小于等于
   - `$ne`：不等于

5. **逻辑操作符**：
   - `$and`：逻辑与
   - `$or`：逻辑或
   - `$not`：逻辑非

6. **字符串操作符**：
   - `$concat`：连接字符串
   - `$substr`：截取字符串
   - `$toLower`：转小写
   - `$toUpper`：转大写
   - `$trim`：去除前后空格

7. **日期操作符**：
   - `$dateFromString`：将字符串转换为日期
   - `$dateToString`：将日期转换为字符串
   - `$dayOfMonth`：获取日期的月份
   - `$year`：获取日期的年份

8. **类型转换操作符**：
   - `$convert`：类型转换
   - `$toString`：转换为字符串
   - `$toInt`：转换为整数
   - `$toDouble`：转换为浮点数

### 索引管理

#### 创建索引
```bash
db.<collection_name>.createIndex({ key: 1 })  # 升序
db.<collection_name>.createIndex({ key: -1 }) # 降序
```

#### 创建唯一索引
```bash
db.collection.createIndex({ key: 1 }, { unique: true })
```

#### 创建全文索引
```bash
db.collection.createIndex({ key: "text" })
```

#### 删除所有索引
```bash
db.collection.dropIndexes()
```

#### 创建复合索引
```bash
db.<collection_name>.createIndex({ key1: 1, key2: -1 })
```

#### 查看索引
```bash
db.<collection_name>.getIndexes()
```

#### 删除索引
```bash
db.<collection_name>.dropIndex("index_name")
```

### 其他常用命令

#### 统计集合中的文档数量
```bash
db.<collection_name>.countDocuments()
```

#### 查找并修改
```bash
db.<collection_name>.findAndModify({
  query: { key: value },
  update: { $set: { new_key: new_value } },
  new: true
})
```

#### 查看当前数据库的状态
```bash
db.stats()
```

#### 查看当前数据库的大小
```bash
db.<collection_name>.totalSize()
```

#### 查看当前数据库的操作
```bash
db.currentOp()
```

#### 查看服务器状态
```bash
db.serverStatus()
```

#### 查看服务器版本
```bash
db.version()
```

#### 退出 MongoDB Shell
```bash
exit
```

### 备份和恢复

#### 备份数据库
```bash
mongodump --db <database_name> --out <backup_directory>
```

#### 恢复数据库
```bash
mongorestore --db <database_name> <backup_directory>/<database_name>
```

### 安全相关

#### 创建用户
```bash
use admin
db.createUser({
  user: "username",
  pwd: "password",
  roles: [
    { role: "readWrite", db: "database_name" }
  ]
})
```
#### 修改用户
```bash
use admin
db.changeUserPassword("username", "new_password")
```

#### 删除用户
```bash
use admin
db.dropUser("username")
```

#### 列出所有用户
```bash
use admin
db.getUsers()
```

#### 列出所有角色
```bash
use admin
db.getRoles()
```
#### 创建角色
```bash
use admin
db.createRole({
  role: "custom_role",
  privileges: [
    { resource: { db: "database_name", collection: "collection_name" }, actions: ["find", "insert"] }
  ],
  roles: []
})
```

### 监控

#### 查看当前活动的操作
```bash
db.currentOp()
```

#### 查看服务器状态
```bash
db.serverStatus()
```

#### 查看数据库状态
```bash
db.stats()
```

#### 查看集合状态
```bash
db.<collection_name>.stats()
```

当然，还有很多其他有用的 MongoDB 命令和功能。以下是更多高级命令和一些实用技巧，涵盖数据验证、复制集管理、分片、性能优化等方面。

### 数据验证

#### 设置集合级别的数据验证规则
```bash
db.runCommand({
  collMod: "collection_name",
  validator: { $jsonSchema: {
    bsonType: "object",
    required: [ "name", "email" ],
    properties: {
      name: { bsonType: "string", description: "must be a string and is required" },
      email: { bsonType: "string", pattern: "^.+@.+\..+$", description: "must be a valid email address and is required" }
    }
  }},
  validationLevel: "strict"
})
```

### 复制集管理

#### 初始化复制集
```bash
rs.initiate()
```

#### 查看复制集配置
```bash
rs.conf()
```

#### 添加成员到复制集
```bash
rs.add("hostname:port")
```

#### 查看复制集状态
```bash
rs.status()
```

#### 步骤回滚
```bash
rs.rollBack()
```

#### 重新配置复制集
```bash
cfg = rs.conf()
cfg.members[0].priority = 2
rs.reconfig(cfg)
```

#### 移除复制集成员
```bash
rs.remove("hostname:port")
```

### 分片管理

#### 启用分片
```bash
sh.enableSharding("database_name")
```

#### 分片集合
```bash
sh.shardCollection("database_name.collection_name", { shardKey: 1 })
```

#### 分配分片键
```bash
sh.enableSharding("database_name")
sh.shardCollection("database_name.collection_name", { shardKey: 1 })
```

#### 查看分片状态
```bash
sh.status()
```

### 性能优化

#### 查看慢查询
```bash
db.setProfilingLevel(2)  # 2 表示记录所有查询
db.system.profile.find().pretty()
```

#### 解释查询计划
```bash
db.collection.explain("executionStats").find({ key: value })
```

#### 优化查询
```bash
db.collection.find({ key: value }).hint({ index_key: 1 })
```

### 日志管理

#### 查看日志
```bash
tail -f /var/log/mongodb/mongod.log
```

#### 修改日志级别
```bash
db.setLogLevel(1, "query")
```

### 安全增强

#### 启用身份验证
编辑 `mongod.conf` 文件，添加以下内容：
```yaml
security:
  authorization: enabled
```

重启 MongoDB 服务：
```bash
sudo systemctl restart mongod
```

#### 创建管理员用户
```bash
use admin
db.createUser({
  user: "admin",
  pwd: "admin_password",
  roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
})
```

### 监控和诊断

#### 使用 `db.currentOp()` 查看当前操作
```bash
db.currentOp()
```

#### 使用 `db.serverStatus()` 查看服务器状态
```bash
db.serverStatus()
```

#### 使用 `db.stats()` 查看数据库统计信息
```bash
db.stats()
```

#### 使用 `db.collection.stats()` 查看集合统计信息
```bash
db.collection.stats()
```

#### 重命名集合
```bash
db.old_collection.renameCollection("new_collection")
```

### 数据导入导出

#### 导出数据
```bash
mongoexport --db database_name --collection collection_name --out file.json
```

#### 导入数据
```bash
mongoimport --db database_name --collection collection_name --file file.json
```

### 高级查询

#### 使用 `$lookup` 进行集合关联
```bash
db.collection1.aggregate([
  {
    $lookup: {
      from: "collection2",
      localField: "foreign_key",
      foreignField: "_id",
      as: "related_documents"
    }
  }
])
```

#### 使用 `$geoNear` 进行地理空间查询
```bash
db.places.createIndex({ location: "2dsphere" })

db.places.aggregate([
  {
    $geoNear: {
      near: { type: "Point", coordinates: [ -73.99279 , 40.719296 ] },
      distanceField: "dist.calculated",
      maxDistance: 2000,
      spherical: true
    }
  }
])
```
