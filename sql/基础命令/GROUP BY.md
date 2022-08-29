#  GROUP BY 

    GROUP BY 可以按分类显示数据
* 得到每个客户分别的销售总额，默认按group by 的排序
```
SELECT 
	client_id,
	SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id
```
## 基本特点

数据默认是使用`GROUP BY`后的数据排序,不过我们使用`ORDER BY`

    GROUP BY 子句永远在FROM 和 WHERE 之后，并且在ORDER BY 之前

`GROUP BY` **不能使用别名，只能使用数据中的列名!**

## 多排分组

`GROUP BY state, city`
此时数据会按多列分组, 可以得到`state`和`city`的分组

    一般来说, 当时进行数据分组, 并且SELECT列中有聚合函数
    一般使用所有列进行GROUP BY
 