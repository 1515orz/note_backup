# splitlines


### 描述
splitlines()按照行('\r', '\r\n', \n')分隔,返回一个包含隔行作为元素的列表,如果参数keepends为False,不包含换行符,如果为True,则保留换行符 

### 语法
`str.splitlines([keepends])`

### 参数
* keepends -- 在输出时是否保留换行符(‘\r’,‘\n’,‘\r\n’)
* 默认为False,不包含换行符,==如果为True,保留换行符==

### 实例
_EXP_
str1 = ‘ab c\n\nde fg\rkl\r\n’
print(str1.splitlines())

str2 = ‘ab c\n\nde fg\rkl\r\n’
print(str2.splitlines(True))

__OUTPUT_
1. ['ab c',  '',  'de fg',  'kl']
2. ['ab c\n',  '\n',  'de fg\r',  'kl\r\n']
