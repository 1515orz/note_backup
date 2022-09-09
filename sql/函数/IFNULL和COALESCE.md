# IFNULL和COALESCE

`IFNULL(值1,值2)` 假如值1为NULL, 则返回值2(值2可以为NULL)

```sql
SELECT 
	order_id,
	IFNULL(shipper_id,'Not assigned')
FROM orders 
```
> IFNULL 相当于单分支 IF...ELSE

---

>`COALESCE(值1, 值2, 值3)`
 COALESCE可以提供一堆值, 并返回第一个非空值, 如果全为空, 最后返回NULL

```sql
SELECT 
	order_id,
	COALESCE(shipper_id,comments,'Not assigned') AS shipper
FROM orders 
```

## 总结

    IFNULL 可以将NULL内容替换为其他内容,
    COALESCE 可以提供一堆值,这个函数会返回这堆值中的第一个非空值     
    例:(shipper_id,comments,'Not assigned'....)
