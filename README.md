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
- 条件查询
```sql
SELECT 字段列表 FROM 表名 WHERE 条件列表;
```
- 聚合函数

| 函数 | 功能 |
|:--:|:--:|
| count | 统计数量 |
| max | 最大值 |
| min | 最小值 |
| avg | 平均值 |
| sum | 求和 |

- 分组查询
```sql
SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件];
```
where和having区别  
1. 执行时机不同：where是分组之前进行过滤，不满足where条件，不参与分组;而having是分组之后对结果进行过滤.
2. 判断条件不同：where不能对聚合函数进行判断，而having可以.

- 排序查询（ASC-升序，DESC-降序）
```sql
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序反式1,字段2 排序反式2;
```
- 分页查询
```sql
SELECT 字段列表 FROM 表名 LIMIT 起始索引,查询记录数;
```
- 执行顺序
FROM , WHERE , GROUP BY , HAVING , SELECT , ORDER BY , LIMIT

# DCL
## 管理用户 
- 查询用户
```sql
USE mysql;
SELECT * FROM user;
```
- 创建用户
```sql
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
```
- 修改用户密码
```sql
ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
```
- 删除用户
```sql
DROP USER '用户名'@'主机名';
```

## 权限控制
| 权限 | 说明 |
|:--:|:--:|
| ALL,ALL PRIVILEGES | 所有权限 |
| SELECT | 查询权限 |
| INSERT | 插入权限 |
| UPDATE | 修改权限 |
| DELETE | 删除权限 |
| ALTER | 修改表权限 |
| DROP | 删除数据库/表/视图权限 |
| CREATE | 创建数据库/表权限 |

- 查询权限
```sql
SHOW GRANTS FOR '用户名'@'主机名';
```
- 赋予权限
```sql
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```
- 撤销权限
```sql
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```
