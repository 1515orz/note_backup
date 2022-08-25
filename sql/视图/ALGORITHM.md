# ALGORITHM

mysql中视图知识点补充
  
>查看表结构
DESC name;

>修改表结构, 添加一列, 添加到bName列的后面
ALTER TABLE name ADD author VARCHAR(50) AFTER bName;

>修改表结构, 添加一列, 并且放在最前面
ALTER TABLE name ADD publish VARCHAR(40) FIRST;

>修改列
ALTER TABLE name CHANGE publish publishers VARCHAR(60) FIRST;

>删除列
ALTER TABLE name DROP publishers;

---


## 视图的ALGORITHM

`ALGORITHM = MERGE/TEMPTABLE/UNDEFINED`

>MERGE:当使用视图时, 会把查询视图的语句和创建视图的语句合并起来, 形成一条语句, 最后再从基表中查询

>TEMPTABLE:当使用视图时, 会把创建视图的语句的查询结果当成一张临时表, **再从临时表中进行筛选**

>UNDEFINED:未定义, 自动, 让系统帮你选

### 示例

> 比较TEMPTABLE和MERGE的区别
 
> 使用ALGORITHM=TEMPTABLE

```
CREATE ALGORITHM=TEMPTABLE VIEW view4 AS
SELECT bid, bName,price, bTypeId FROM book ORDER BY bTypeId ASC, price DESC; 
SELECT * FROM view4;
#查询结果为bid是3和6
```

```
#使用ALGORITHM=MERGE
CREATE ALGORITHM=MERGE VIEW view5 AS
SELECT bid, bName,price, bTypeId FROM book ORDER BY bTypeId ASC, price DESC;
SELECT * FROM view5;
#查询结果为bid是1和5
```
 



