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

- 查询
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

