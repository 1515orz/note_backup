# grep命令

    linux 中一种强大的文本搜索工具，grep允许对文本进行模式查找，即正则表达式

`grep [字符串] [文件]` 查找匹配文件中的字符串
`-n` 显示匹配行号
`-v`  显示不包含匹配文本的所有行**相当于求反**
`-i` 忽略大小写
`--color=auto` 搜索出的关键字用颜色显示

## 模式查找

^a 行首，搜寻以a开头的行，^
ke$ 行尾，搜寻以ke结束的行，$
