# ONLY_FULL_GROUP_BY

    ONLY_FULL_GROUP_BY是mysql默认的一种sql模式，其作用是约束sql语句：
    要求select中的所有字段，除复合函数外，全部要出现在group by中。
    
    默认这种模式是有原因的，因为滥用gourp by可能会得到错误的结果，但是这里不做讨论。
 
## 关闭该模式
* 关闭 session级
```
SET SESSION sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
```
* 关闭 GLOBAL级
```
SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
```

## 永久关闭

    永久关闭only_full_group_by模式，这种方法需要在mysql的配置文件里修改，然后重启。

1. 找到配置文件/etc/my.cnf(或则关联文件夹找到mysql-server.cnf)
2. 在上述文件内的[mysqld]后追加sql_mode=‘STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION’
3. 保存配置文件后，重启Mysql即可。

## 关闭影响

### 开启选项

    接下来演示一下关闭与打开Session级的sql_mode.only_full_group_by属性带来的影响！
    
查看 sql_mode属性

> 查看Session级: `SELECT @@sql_mode;`
> 查看 GLOBAL级: `select @@GLOBAL.sql_mode;`

查看Session级的 sql_mode属性，结果是可以看到带有ONLY_FULL_GROUP_BY属性的，所以我们GROUP BY name会报 1055 异常

### 关闭选项

    接下来关闭Session级的 sql_mode属性
    再次select @@sql_mode;查询发现 sql_mode的值已经删除了ONLY_FULL_GROUP_BY属性
    
然后再次执行如下sql

`SELECT name,author,SUM(price) FROM  t_bookGROUP BY name `

**注意** 查询结果中，select后边的author属性由于没有使用聚合函数，所以只会返回原数据表中的第一条数据，使用时请注意！原数据如下

## 折中的选择

②：使用 ANY_VALUE() 抑制 ONLY_FULL_GROUP_BY 的影响
         如果不想关闭mysql的ONLY_FULL_GROUP_BY全局设置，仅仅想让当前sql忽略其影响，则可以使用ANY_VALUE(cloum) 忽略ONLY_FULL_GROUP_BY的影响，详见官方文档！
[官方文档](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html)

>使用 ANY_VALUE（）忽略ONLY_FULL_GROUP_BY的影响：
```
SELECT name,ANY_VALUE(author),SUM(price) FROM  `t_book`
GROUP BY name
```