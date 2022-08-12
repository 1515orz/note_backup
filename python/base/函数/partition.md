# partition


partition()方法用来根据指定的分隔符将字符串进行分割,如果字符串包含指定的分隔符,则返回一个3元的元组,第一个为分隔符左边的字串,第二个为分隔符本身,第三个为分隔符右边的字串.

### 语法
`str.partition(str)`

### 参数
str: 指定的分隔符

### 实例 EXP
str = "www.runoob.com"
print  str.partition(".")



# repartition
str = "www.runoob.com"  print  str.rpartition(".")

输出结果为：

('www.runoob',  '.',  'com')
