## 📌 char  和 varchar 区别

> CHAR是**定长**，VARCHAR是**变长**

👉 一句话：

> CHAR快但浪费空间，VARCHAR省空间但稍慢

------

## 📌SQL语句（统计人数 + 条件查询）

```
-- 统计人数
SELECT COUNT(*) FROM 表名;

-- 选出课程编号不为XX的学生学号
SELECT 学号 FROM 表名 WHERE 课程编号 != 'XX';
```

------

## 📌删除重复数据（保留1条）

```
DELETE FROM 表名
WHERE id NOT IN (
  SELECT MIN(id) FROM 表名 GROUP BY 所有字段
);
```

👉 核心：

> 分组保留最小id，其余删除

------

## 📌 数据库事务

> 事务是一组操作，要么全部成功，要么全部失败

- 特性：ACID（原子性、一致性、隔离性、持久性）

------

## 📌数据库连接泄露

> 连接使用后未关闭，导致连接池耗尽

👉 结果：

> 系统无法获取新连接，性能下降甚至崩溃

------

## 📌 MySQL删除语句

```
DELETE FROM 表名 WHERE 条件;
```

------

## 📌 左连接（LEFT JOIN）

> 以左表为主，右表没有匹配也返回NULL

👉 场景：

> 查询“主表全部 + 从表部分”（如：所有用户及订单）

------

## 📌查询 / 更新某一列

```
-- 查询
SELECT 列名 FROM 表名;

-- 更新
UPDATE 表名 SET 列名 = 新值 WHERE 条件;
```

------

## 📌多表查询

```
SELECT a.*, b.*
FROM A a
JOIN B b ON a.id = b.id;
```

------

## 📌Redis

> Redis是基于内存的**高性能键值数据库**

特点：

- 高性能（内存）
- 支持多数据结构（String、List、Set、Hash）
- 常用于缓存、分布式锁、计数器

------

## 📌 基本SQL语句

```
SELECT * FROM 表;
INSERT INTO 表 VALUES (...);
UPDATE 表 SET 列=值 WHERE 条件;
DELETE FROM 表 WHERE 条件;
```

------

## 📌MySQL密码丢失 / 建表 / 授权

### 重置密码

> 跳过权限表启动，修改mysql.user表

------

### 建表

```
CREATE TABLE 表名 (
  id INT PRIMARY KEY,
  name VARCHAR(50)
);
```

------

### 授权

```
GRANT ALL PRIVILEGES ON 数据库.* TO 'user'@'%' IDENTIFIED BY '密码';
```

------

## 📌COUNT vs SUM

- COUNT：统计行数
- SUM：求和

👉 区别：

- COUNT(*)：统计所有行（包括NULL）
- COUNT(列)：不统计NULL

------

## 📌 s_name表（简单查询）

```
SELECT s_name FROM 表名;
```

------

## 📌聚类查询（GROUP BY）

> 按某列分组统计

```
SELECT 列名, COUNT(*)
FROM 表名
GROUP BY 列名;
```

------

## 📌 总成绩前10名

```
SELECT *
FROM 表名
ORDER BY 总成绩 DESC
LIMIT 10;
```

------

## 📌 事务 vs 主键 vs 外键

- 事务：保证操作一致性
- 主键：唯一标识一行数据
- 外键：建立表与表之间关系

------

## 📌缓存技术

> 用空间换时间，提高访问速度

- 常见：Redis
- 场景：热点数据、减少数据库压力

## 📌数据库用MySQL吗？平时SQL怎么写

> 常用MySQL，SQL主要是CRUD + 多表关联 + 分组统计。

👉 关键词：
 SELECT / INSERT / UPDATE / DELETE / JOIN / GROUP BY / ORDER BY

------

## 📌数据库优化

> 优化核心：**减少IO + 提高查询效率**

- 建索引（最重要）
- 避免全表扫描
- 合理SQL（避免子查询、select *）
- 分库分表
- 使用缓存（Redis）

👉 一句话：

> 索引 + SQL优化 + 架构优化

------

## 📌幻读

> 一个事务中，两次查询结果不一致（多了或少了数据）

👉 原因：

- 其他事务插入数据

👉 解决：

- 可重复读 / 加锁

------

## 📌MyBatis优势 + 事务

### 优势

- 简化JDBC
- 支持动态SQL
- 易维护

### 事务

> 通常交给Spring管理（声明式事务）