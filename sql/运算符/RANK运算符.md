# RANK运算符

1. RANK()

        在计算排序时，若存在相同位次，会跳过之后的位次。
        例如，有3条排在第1位时，排序为：1，1，1，4······

2. DENSE_RANK()

        这就是题目中所用到的函数，在计算排序时，若存在相同位次，不会跳过之后的位次。

    例如，有3条排在第1位时，排序为：1，1，1，2······

3. ROW_NUMBER()

    这个函数赋予唯一的连续位次。
    例如，有3条排在第1位时，排序为：1，2，3，4······

```
# RANK的一种用法
SELECT 
  p.id,
  p.name,
  COUNT(s.sale) AS sale_count,
  RANK() OVER(ORDER BY COUNT(s.sale)) AS sale_rank
FROM sales s
JOIN people p
ON p.id = s.people_id
GROUP BY p.id
```