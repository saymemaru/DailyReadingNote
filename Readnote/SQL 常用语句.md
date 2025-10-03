# SQL常用语句(SQLite)

创建并打开数据库

```sql
.open testdb.db
```

附加数据库，选择该数据库以进行其他操作

```sql
ATTACH DATABASE 'testdb.db' as 'TEST'
```

显示附加的数据库

```sql
.database
```

在数据库中创建表

```sql
CREATE TABLE testdb.testtable
 (
   ID INT PRIMARY KEY     NOT NULL,
   NAME           TEXT    NOT NULL,
   AGE            INT     NOT NULL,
   ADDRESS        CHAR(50),
   SALARY         REAL
);
```

>NOT NULL 表示字段不能为空

列出附加数据库中的所有表

```sql
.tables
```

删除表

```sql
DROP TABLE dtestdb.testtable
```

在表中创建记录

```sql
INSERT INTO testdb.testtable (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (1, 'Paul', 32, 'California', 20000.00 );

INSERT INTO testdb.testtable (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (2, 'Allen', 25, 'Texas', 15000.00 );

INSERT INTO testdb.testtable (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (3, 'Teddy', 23, 'Norway', 20000.00 );
```

从表中获取符合条件的对应字段的数据

```sql
SELECT ID, NAME, SALARY 
FROM testdb.testtable 
WHERE AGE >= 25 AND SALARY >= 65000testtable;
```

更新符合条件的对应字段的数据

```sql
UPDATE testdb.testtable 
SET ADDRESS = 'Texas' 
WHERE ID = 6;
```

删除符合条件的对应字段的数据

```sql
DELETE FROM testdb.testtable WHERE ID = 7;
```

查找匹配通配符指定模式的文本值（不分大小写）

```sql
WHERE SALARY LIKE '200%'	查找以 200 开头的任意值
WHERE SALARY LIKE '%200%'	查找任意位置包含 200 的任意值
WHERE SALARY LIKE '_00%'	查找第二位和第三位为 00 的任意值
WHERE SALARY LIKE '2_%_%'	查找以 2 开头，且长度至少为 3 个字符的任意值
WHERE SALARY LIKE '%2'	查找以 2 结尾的任意值
WHERE SALARY LIKE '_2%3'	查找第二位为 2，且以 3 结尾的任意值
WHERE SALARY LIKE '2___3'	查找长度为 5 位数，且以 2 开头以 3 结尾的任意值
```

查找匹配通配符指定模式的文本值（区分大小写）
```sql
WHERE SALARY GLOB '200*'	查找以 200 开头的任意值
WHERE SALARY GLOB '*200*'	查找任意位置包含 200 的任意值
WHERE SALARY GLOB '?00*'	查找第二位和第三位为 00 的任意值
WHERE SALARY GLOB '2??'	查找以 2 开头，且长度为 3 个字符的任意值，例如，它可能匹配 "200"、"2A1"、"2B2" 等值。
WHERE SALARY GLOB '*2'	查找以 2 结尾的任意值
WHERE SALARY GLOB '?2*3'	查找第二位为 2，且以 3 结尾的任意值
WHERE SALARY GLOB '2???3'	查找长度为 5 位数，且以 2 开头以 3 结尾的任意值
```

在表开头偏移2条记录，从第3位开始提取 3 个记录（limit限制数量）

```sql
SELECT * 
FROM testdb.testtable 
LIMIT 3 OFFSET 2;
```

> * 表示选中所有字段

选中字段按升序ASC/降序DESC排列

```sql
SELECT select_list
FROM testdb.testtable 
ORDER BY
    column_1 ASC,
    column_2 DESC;
```

```sql
SELECT * 
FROM testdb.testtable 
LIMIT 3 OFFSET 2;
```