---
title: Mysql命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Mysql,Database]
---
MySQL是一个广泛使用的开源关系型数据库管理系统。以下是MySQL中一些常用的命令，涵盖数据库和数据表的管理、数据操作以及用户权限管理等方面：

### 连接与登出
- **连接MySQL服务器**  
  ```bash
  mysql -u 用户名 -p
  ```
  输入命令后，会提示输入用户密码。

- **退出MySQL**  
  在MySQL命令行中输入：
  ```sql
  quit
  ```

### 数据库操作
- **显示所有数据库**  
  ```sql
  show databases;
  ```

- **创建数据库**  
  ```sql
  create database 数据库名;
  ```

- **选择数据库**  
  ```sql
  use 数据库名;
  ```

- **删除数据库**  
  ```sql
  drop database 数据库名;
  ```

### 数据表操作
- **显示当前数据库的所有表**  
  ```sql
  show tables;
  ```

- **创建表**  
  示例创建一个用户表：
  ```sql
  create table users (
    id int primary key,
    username varchar(50),
    password varchar(50)
  );
  ```

- **查看表结构**  
  ```sql
  describe 表名;
  ```

- **插入数据**  
  ```sql
  insert into 表名 (列1, 列2, ...) values (值1, 值2, ...);
  ```

- **更新数据**  
  ```sql
  update 表名 set 列名 = 新值 where 条件;
  ```

- **删除数据**  
  ```sql
  delete from 表名 where 条件;
  ```

- **删除表**  
  ```sql
  drop table 表名;
  ```

### 数据查询
- **基本查询**  
  ```sql
  select * from 表名;
  ```

- **条件查询**  
  ```sql
  select * from 表名 where 条件;
  ```

### 用户管理与权限
- **添加新用户**  
  ```sql
  create user '新用户名'@'localhost' identified by '密码';
  ```

- **授予权限**  
  ```sql
  grant 权限列表 ON 数据库名.表名 TO '用户名'@'访问来源';
  ```
  例如，授予所有权限：
  ```sql
  grant all privileges on *.* to '用户名'@'%' identified by '密码';
  ```

- **撤销权限**  
  ```sql
  revoke 权限列表 ON 数据库名.表名 FROM '用户名'@'访问来源';
  ```

- **刷新权限**  
  ```sql
  flush privileges;
  ```

### 事务控制
- **开始事务**：

  ```sql
  START TRANSACTION;
  ```

  或者

  ```sql
  BEGIN;
  ```

- **提交事务**：

  ```sql
  COMMIT;
  ```

  当事务被提交后，所有的更改将被永久保存到数据库中。

- **回滚事务**：

  ```sql
  ROLLBACK;
  ```

  如果事务过程中发生错误，可以通过回滚来撤销所有已执行的操作。

- **设置保存点**：

  ```sql
  SAVEPOINT savepoint_name;
  ```

  可以在事务中设置保存点，这样就可以选择性地回滚到某个特定的保存点，而不是整个事务。

- **回滚到保存点**：

  ```sql
  ROLLBACK TO SAVEPOINT savepoint_name;
  ```

- **释放保存点**：

  ```sql
  RELEASE SAVEPOINT savepoint_name;
  ```

  释放一个保存点，使其不再可用。

### 查询优化

#### 使用 EXPLAIN 分析查询

```sql
EXPLAIN SELECT * FROM table_name WHERE condition;
```

#### 创建和优化索引

```sql
CREATE INDEX idx_column ON table_name(column_name);
ANALYZE TABLE table_name;
OPTIMIZE TABLE table_name;
```

### 性能优化

#### 调整 MySQL 配置文件

编辑 `my.cnf` 或 `my.ini` 文件，调整以下参数：

```ini
[mysqld]
innodb_buffer_pool_size = 2G
query_cache_size = 64M
max_connections = 150
```

### 日志管理
- **开启查询日志**  
  编辑 `my.cnf` 或 `my.ini` 文件，添加或修改以下内容：
  ```ini
  [mysqld]
  general_log = 1
  general_log_file = /path/to/general.log
  ```
  开启查询日志可以帮助你记录所有的SQL语句，对于调试和性能分析非常有用。

- **开启慢查询日志**  
  编辑 `my.cnf` 或 `my.ini` 文件，添加或修改以下内容：
  ```ini
  [mysqld]
  slow_query_log = 1
  slow_query_log_file = /path/to/slow.log
  long_query_time = 2
  ```
  慢查询日志可以记录执行时间超过指定秒数的SQL语句，这对于找出性能瓶颈很有帮助。

### 高级查询

#### 子查询
子查询可以在 `SELECT`、`FROM`、`WHERE` 和 `HAVING` 子句中使用，用于嵌套查询。
```sql
-- 查找某个部门中工资最高的员工
SELECT * FROM employees 
WHERE salary = (SELECT MAX(salary) FROM employees WHERE department_id = 10);
```

#### 连接
连接用于将多个表的数据合并在一起，常见的连接类型包括 `INNER JOIN`、`LEFT JOIN`、`RIGHT JOIN` 和 `FULL JOIN`。
```sql
-- 将 employees 表和 departments 表连接起来
SELECT e.first_name, e.last_name, d.department_name 
FROM employees e 
JOIN departments d ON e.department_id = d.department_id;
```

### 窗口函数

#### 1. `ROW_NUMBER()`
为每个分区中的行分配一个唯一的行号。

```sql
SELECT id, product, sale_date, amount,
       ROW_NUMBER() OVER (PARTITION BY product ORDER BY sale_date) AS row_num
FROM sales;
```

#### 2. `RANK()`
为每个分区中的行分配一个排名，相同值的行会得到相同的排名，但下一个排名会跳过相应的数字。

```sql
SELECT id, product, sale_date, amount,
       RANK() OVER (PARTITION BY product ORDER BY amount DESC) AS rank
FROM sales;
```

#### 3. `DENSE_RANK()`
为每个分区中的行分配一个排名，相同值的行会得到相同的排名，但下一个排名不会跳过。

```sql
SELECT id, product, sale_date, amount,
       DENSE_RANK() OVER (PARTITION BY product ORDER BY amount DESC) AS dense_rank
FROM sales;
```

#### 4. `LEAD()`
返回当前行之后的行的值。

```sql
SELECT id, product, sale_date, amount,
       LEAD(amount, 1, 0) OVER (PARTITION BY product ORDER BY sale_date) AS next_amount
FROM sales;
```

#### 5. `LAG()`
返回当前行之前的行的值。

```sql
SELECT id, product, sale_date, amount,
       LAG(amount, 1, 0) OVER (PARTITION BY product ORDER BY sale_date) AS prev_amount
FROM sales;
```

#### 6. `SUM()`
在窗口内计算累计和。

```sql
SELECT id, product, sale_date, amount,
       SUM(amount) OVER (PARTITION BY product ORDER BY sale_date) AS cumulative_sum
FROM sales;
```

#### 7. `AVG()`
在窗口内计算平均值。

```sql
SELECT id, product, sale_date, amount,
       AVG(amount) OVER (PARTITION BY product ORDER BY sale_date) AS rolling_avg
FROM sales;
```

#### 8. `MIN()`
在窗口内计算最小值。

```sql
SELECT id, product, sale_date, amount,
       MIN(amount) OVER (PARTITION BY product ORDER BY sale_date) AS rolling_min
FROM sales;
```

#### 9. `MAX()`
在窗口内计算最大值。

```sql
SELECT id, product, sale_date, amount,
       MAX(amount) OVER (PARTITION BY product ORDER BY sale_date) AS rolling_max
FROM sales;
```

### 聚合函数

聚合函数用于对一组行进行计算并返回单个值。以下是一些常见的聚合函数及其用法：

#### 1. `COUNT()`
计算行数。

```sql
SELECT COUNT(*) AS total_rows
FROM sales;
```

#### 2. `SUM()`
计算总和。

```sql
SELECT SUM(amount) AS total_amount
FROM sales;
```

#### 3. `AVG()`
计算平均值。

```sql
SELECT AVG(amount) AS average_amount
FROM sales;
```

#### 4. `MIN()`
计算最小值。

```sql
SELECT MIN(amount) AS min_amount
FROM sales;
```

#### 5. `MAX()`
计算最大值。

```sql
SELECT MAX(amount) AS max_amount
FROM sales;
```

#### 6. `GROUP_CONCAT()`
将多行值连接成一个字符串。

```sql
SELECT product, GROUP_CONCAT(sale_date ORDER BY sale_date SEPARATOR ', ') AS sale_dates
FROM sales
GROUP BY product;
```

### 组合使用窗口函数和聚合函数

你也可以在同一个查询中组合使用窗口函数和聚合函数。例如，计算每个产品的累计销售额，并显示总销售额：

```sql
SELECT id, product, sale_date, amount,
       SUM(amount) OVER (PARTITION BY product ORDER BY sale_date) AS cumulative_sum,
       SUM(amount) OVER () AS total_amount
FROM sales;
```

### 数据建模

#### 分区表
分区表可以将大表物理分割成更小的部分，以提高管理和查询效率。
```sql
-- 按年份范围分区
CREATE TABLE sales (
    id INT NOT NULL,
    sale_date DATE NOT NULL,
    amount DECIMAL(10, 2)
) PARTITION BY RANGE (YEAR(sale_date)) (
    PARTITION p0 VALUES LESS THAN (2010),
    PARTITION p1 VALUES LESS THAN (2015),
    PARTITION p2 VALUES LESS THAN (2020),
    PARTITION p3 VALUES LESS THAN MAXVALUE
);
```

### 安全性

#### 用户权限管理
用户权限管理是确保数据库安全的重要手段。
```sql
-- 创建新用户
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';

-- 授予权限
GRANT SELECT, INSERT, UPDATE ON database_name.table_name TO 'newuser'@'localhost';

-- 撤销权限
REVOKE SELECT, INSERT, UPDATE ON database_name.table_name FROM 'newuser'@'localhost';

-- 刷新权限
FLUSH PRIVILEGES;
```

#### 数据加密
启用 SSL/TLS 加密通信可以提高数据传输的安全性。
编辑 `my.cnf` 或 `my.ini` 文件，启用 SSL/TLS：
```ini
[mysqld]
ssl-ca=/path/to/ca.pem
ssl-cert=/path/to/server-cert.pem
ssl-key=/path/to/server-key.pem
```

### 备份与恢复

#### 逻辑备份
逻辑备份是将数据库内容导出为 SQL 脚本文件。
```sh
mysqldump -u username -p database_name > backup.sql
```

#### 物理备份
物理备份是将数据库文件直接复制。
```sh
innobackupex --user=username --password=password /path/to/backup
```

#### 恢复备份
恢复备份时，首先应用日志，然后将备份文件复制回原位置。
```sh
mysql -u username -p database_name < backup.sql
innobackupex --apply-log /path/to/backup
innobackupex --copy-back /path/to/backup
```

### 高可用性和可扩展性

#### 主从复制
主从复制可以实现读写分离，提高系统可用性和性能。

##### 主服务器配置
编辑 `my.cnf` 或 `my.ini` 文件：
```ini
[mysqld]
server-id=1
log_bin=mysql-bin
binlog_do_db=database_name
```
启动二进制日志：
```sql
FLUSH LOGS;
```
查看二进制日志位置：
```sql
SHOW MASTER STATUS;
```

##### 从服务器配置
编辑 `my.cnf` 或 `my.ini` 文件：
```ini
[mysqld]
server-id=2
relay-log=mysql-relay-bin
log_bin=mysql-bin
read_only=1
```
启动复制：
```sql
CHANGE MASTER TO MASTER_HOST='master_host', MASTER_USER='replication_user', MASTER_PASSWORD='password', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=107;
START SLAVE;
```

### 监控与诊断

#### 使用 `SHOW` 命令
`SHOW` 命令可以显示当前的连接、表状态等信息。
```sql
SHOW PROCESSLIST;
SHOW TABLE STATUS LIKE 'table_name';
```

#### 使用 Performance Schema
Performance Schema 提供了详细的性能监控数据。
```sql
SELECT * FROM performance_schema.events_statements_current;
```

### 其他高级用法

#### 触发器
触发器是在特定数据操作（如插入、更新、删除）发生时自动执行的数据库对象。
```sql
-- 创建一个插入触发器
CREATE TRIGGER before_insert_trigger
BEFORE INSERT ON table_name
FOR EACH ROW
BEGIN
    -- 执行某些操作
    SET NEW.column_name = some_value;
END;
```

#### 存储过程和函数
存储过程和函数可以封装复杂的业务逻辑或重复使用的代码块。
```sql
-- 创建一个存储过程
DELIMITER //
CREATE PROCEDURE get_employee_info(IN emp_id INT)
BEGIN
    SELECT * FROM employees WHERE id = emp_id;
END //
DELIMITER ;

-- 调用存储过程
CALL get_employee_info(1);
```

#### 视图
视图是一个虚拟表，可以简化查询或保护数据。
```sql
-- 创建一个视图
CREATE VIEW employee_view AS
SELECT first_name, last_name, department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;

-- 查询视图
SELECT * FROM employee_view;
```

### 错误处理与调试
- **显示最后一条错误消息**  
  ```sql
  SHOW ERRORS;
  ```
  这可以帮助开发人员快速定位问题所在。

- **显示警告信息**  
  ```sql
  SHOW WARNINGS;
  ```
  有时候，SQL语句虽然执行成功，但是会产生一些警告信息，这些信息可能对后续的查询有影响。

### 数据导入与导出
- **数据导出**  
  使用 `mysqldump` 工具可以方便地将数据库或表导出为SQL文件。
  ```sh
  mysqldump -u username -p database_name table_name > table_name.sql
  ```

- **数据导入**  
  导入SQL文件可以使用 `mysql` 命令行工具。
  ```sh
  mysql -u username -p database_name < table_name.sql
  ```

### 总结

以上是 MySQL 命令行中的一些常用命令和高级用法。通过掌握这些命令，你可以更高效地管理和优化 MySQL 数据库。