GROUP BY 可以按分类显示数据
得到每个客户分别的销售总额，默认按group by 的排序
SELECT 
	client_id,
	SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id

GROUP BY 子句永远在FROM 和 WHERE 之后，并且在ORDER BY 之前

GROUP BY 不能使用别名，只能使用数据中的列名