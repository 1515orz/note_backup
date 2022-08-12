# zfill

### 描述
zfill()方法返回指定长度的字符串,元字符右对齐，前面填充0

### 语法
`str.zfill(width)`

### 参数
width -- 指定字符串的长度. 原字符串右对齐,前面填充0

### 实例
str =  “this is string example....wow!!!“
print str.zfill(40) 
print str.zfill(50)

_OUTPUT_
00000000this  is  string example....wow!!!
000000000000000000this  is  string example....wow!!!
