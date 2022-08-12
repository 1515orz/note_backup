# split

### 描述
python split()通过指定分隔符对字符串进行切片,如果参数num有指定值,则分隔num+1个子字符串

### 语法
split()方法语法:
`str.split(str='',num=string.count(str))`

### 参数
`str`分隔符,默认为所有的空字符,包括空格,换行(\n),制表符(\t)等\
`num`分割次数,默认为分隔-1,即分隔所有

### 返回值
返回分割后的字符串列表

### 实例
_EXP1_
str ="Line1-abcdef \nLine2-abc \nLine4-abcd"
print(str.split()  **以空格为分隔符,包含\n**
print(str.split(‘ ’,1)  **以空格为分隔符,分隔成两个**
**OUTPUT**
1. ['Line1-abcdef',  'Line2-abc',  'Line4-abcd'] 
2. ['Line1-abcdef',  '\nLine2-abc \nLine4-abcd']
_EXP2_
txt = "Google#Runoob#Taobao#Facebook"  # 第二个参数为 1，返回两个参数列表 
x = txt.split("#", 1)  
print (x)
**OUTPUT**
['Google',  'Runoob#Taobao#Facebook']


