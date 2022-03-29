# Learn_Mysql
Mysql

# SQL
- SQL分类

| 分类 | 全称 | 说明 |
|:--:|:--:|:--:|
| DDL | Data Definition Language | 数据定义语言，用来定义数据库对象(数据库，表，字段) |
| DML | Data Manipulation Language | 数据操作语言，用来对数据库表中的数据进行增删改 |
| DQL | Data Query Language | 数据查询语言，用来查询数据库表中的记录 |
| DCL | Data Control Language | 数据控制语言，用来创建数据库用户，控制数据库的访问权限 |

<hr>

# DDL

## 查询
- 查询所有数据库
```sql
SHOW DATABASES;
```
  - 查询当前数据库
```sql
SELECT DATABASE();
```
- 创建
```sql
CREATE DATABASE [IF NOT EXIST] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
```
- 删除
```sql
DROP DATABASE [IF EXISTS] 数据库名;
```
- 使用
```sql
USE 数据库名;
```
## 表操作 - 查询
- 查询当前数据库所有表
```sql
SHOW TABLES;
```
- 查询表结构
```sql
DESC 表名;
```
- 查询指定表的建表语句
```sql
SHOW CREATE TABLE 表名;
```
## 表操作 - 创建
```sql
CREATE TABLE 表名(
  字段1 字段1类型 [COMMENT 字段1注释],
  字段2 字段2类型 [COMMENT 字段2注释],
  字段3 字段3类型 [COMMENT 字段3注释],
  ...  ...
  字段n 字段n类型 [COMMENT 字段n注释]
)[COMMENT 表注释];
```
## 表操作 - 修改
- 添加字段
```sql
ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];
```
- 修改数据类型
```sql
ALTER TABLE 表名 MODIFY 字段名 新数据类型;
```
- 修改字段名和字段类型
```sql
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型 [COMMENT 注释] [约束];
```
- 删除字段
```sql
ALTER TABLE 表名 DROP 字段名;
```
- 修改表名
```sql
ALTER TABLE 表名 RENAME TO 新表名;
```
- 删除表
```sql
DROP TABLE [IF EXISTS] 表名;
```
- 删除指定的表，并重新创建该表
```sql
TRUNCATE TABLE 表名;
```

<hr>

# DML
## 添加数据
- 给指定字段添加数据
```sql
INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1,值2,...);
```
- 给全字段赋值
```sql
INSERT INTO 表名 VALUES(值1,值2,...);
```
- 批量添加数据
```sql
INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1,值2,...),(值1,值2,...),(值1,值2,...);
```
```sql
INSERT INTO 表名 VALUES(值1,值2,...),(值1,值2,...),(值1,值2,...);
```
## 修改数据
```sql
UPDATE 表名 SET 字段名1=值1,字段名2=值2,... [WHERE 条件];
```

<hr>

# DQL
```sql
SELECT
  字段列表
FROM
  表名列表
WHERE
  条件列表
GROUP BY
  分组字段列表
HAVING
  分组后条件列表
ORDER BY
  排序字段列表
LIMIT
  分页参数
```
- 基本查询
```sql
SELECT 字段名1,字段名2,... FROM 表名;
```
```sql
SELECT * FROM 表名;
```
- 设置别名
```sql
SELECT 字段1 [AS 别名1,字段2 [AS 别名2],... FROM 表名;
```
- 去除重复记录
```sql
SELECT DISTINCT 字段列表 FROM 表名;
```
