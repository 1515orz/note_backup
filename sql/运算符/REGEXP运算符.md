# REGEXP正则表达式

正则表达式用来条件匹配更加强大,参考[基础正则表达式](../../linux/shell编程/基础正则表达式.md)
```
SELECT *
FORM table
WHERE name LIKE '%abc%' == REGEXP 'abc'
```


## 符号含义
> `^` 表示开头 `REGEXP '^abc'` 匹配'abc'开头
> `$` 表示结尾 `REGEXP '123$'` 匹配'123'结尾

> `|` 表示or，表示多个搜寻模式 
* `REGEXP 'a|b|c'`匹配同时包含'a,b,c'的字串

> `[]` 表示可以出现其中的字符，可以使用[a-h]来表示范围
* `WHERE last_name REGEXP '[gim]e'` 代表匹配包含'ge,ie,me'的数据


## 练习
```
SELECT * FROM customers
# 匹配包含'elka'或'ambur'的数据
WHERE first_name REGEXP 'elka|ambur'
# 匹配'ey'结尾或'on'结尾的数据
WHERE last_name REGEXP 'ey$|on$'
# 匹配'my'开头或者包含'se'的数据
WHERE last_name REGEXP '^my|se'
# 匹配含有'b'跟在'r'或'u'后的数据
WHERE last_name REGEXP '[ru]b' or 'br|bu'
```  


