# HAVING子句

`HAVING` 子句可以在`GROUP BY` 子句之后筛选数据
解决 `WHERE`不能筛选还未创建的列的问题

> WHRER 可以在分组之前进行筛选数据，HAVING 可以在分组之后筛选数据

> 区别：`WHERE` 是指定**数据中的列** `HAVING` 能指定**SELECT没选中的列，即使是新创建的**

>WHERE ...
GROUP BY ...
HAVING ...



```
SELECT 
	client_id,
    	SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id
HAVING total_sales > 500
```

    