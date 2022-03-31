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

# 约束
## 分类
| 约束 | 描述 | 关键字 |
|:--:|:--:|:--:|
| 非空约束 | 限制该字段的数据不能为null | NOT NULL |
| 唯一约束 | 保证该字段的所有数据都是唯一，不重复的 | UNIQUE |
| 主键约束 | 主键是一行数据的唯一标识，要求非空唯一 | PRIMARY KEY |
| 默认约束 | 保存数据时，如果未指定该字段的值，则采用默认值 | DEFAULT |
| 外键约束 | 用来让两张表的数据之间建立连接，保证数据的一致性和完整性 | FOREIGN KEY |

## 外键约束
- 添加外键
```sql
CREATE TABLE 表名(
    字段名 数据类型
    ... ... 
    [CONSTRAINT] [外键名称] FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名)
)
```
```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名);
```
- 外键约束下的删除/更新行为

| 行为 | 说明 |
|:--:|:--:|
| NO ACTION | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。(与RESTRICT一致) |
| RESTRICT | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。(与NO ACTION一致) |
| CASCADE | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有,则删除/更新外键在子表中的记录 |
| SET NULL | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中的数据为null |
| SET DEFAULT | 父表有变更时，子表将外键列设置成一个默认的值(Innodb不支持) |

- 语法
```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段) REFERENCES 主表名(主表字段名) ON UPDATE CASCADE ON DELETE CASCADE;
```

# 多表查询
- 一对多(多对一)
  - 案例：部门与员工的关系
  - 关系：一个部门对应多个员工，一个员工对应一个部门
  - 实现：在多的一方建立外键，指向一的一方的主键

- 多对多
  - 案例：学生和课程的关系
  - 关系：一个学生可以选择多门课程，一门课程也可以共多个学生选择
  - 实现：建立第三张中间表，中间表至少包含两个外键，分别关联两方的主键
  
- 一对一
  - 案例：用户与用户详情的关系
  - 关系：一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其他详情字段放在另一张表中，以提高操作效率
  - 实现：在任意一方加入外键，关联另外一方的主键，并且设置外键为唯一的(UNIQUE)

## 多表查询分类
- 连接查询
  - 内连接：相当于查询A,B交集部分数据
  - 外连接：
    - 左外连接：查询左表的所有数据，以及两张表交集部分数据
    - 右外连接：查询右表的所有数据，以及两张表交集部分数据
  - 自连接：当前表与自身的连接查询，自连接必须使用表别名
- 子查询

### 连接查询-内连接
- 隐式内连接
```sql
SELECT 字段列表 FROM 表1,表2 WHERE 条件;
```
- 显式内连接
```sql
SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 连接条件...;
```
### 连接查询-外连接
- 左外连接
```sql
SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件;
```
- 右外连接
```sql
SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件;
```
### 连接查询-自连接
```sql
SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件;
```
