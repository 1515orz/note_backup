# 文件搜索命令find

_最好少用搜索,而是规划好自己的目录结构,因为会占用大量资源_
++使用find命令时,搜索范围越小越好,条件越精准越好,尽量不要在服务器负载大时使用++
### find语法
`find` [搜索范围] [匹配条件]

### find选项
_find的选项非常多,我们只需要了解常用的即可_
**直接使用find / [文件名] 代表在根目录下搜索**

++根据文件名查找++
`-name` find /etc -name init  
**在linux中的搜索默认是精准全匹配搜索,而windows是模糊搜索**
#### 在linux中使用模糊搜索,使用`通配符`
_EXP_
* find /etc -name *init*
* find /etc -name init???

#### 不区分大小写搜索
++在linux中搜索是区分大小写的++
`-iname` 在搜索时不区分大小写

#### 根据文件大小查找
++一个数据块是512字节,0.5k++
`-size [+/-]`  查找一定大小的文件,+/- 代表大于/小于,但是在查找时要使用数据块进行换算，_减号代表几分钟前,加号代表几分钟内_
_EXP_ 100MB = 102400KB = 204800(数据块)
**查找大于100MB的文件**
find / -size +204800

#### 根据所有者查找
`-user` find /home -user 1515 _查找1515下的所有文件_

#### 根据时间属性查找
`-amin` 访问时间 access  _cat,more,less,tail等操作_
`-cmin` 文件属性 change  _ls -l 看到的就是文件属性_(change)
`-mmin` 文件内容 modify  _文件内容被改变时间_(modified)
**在etc下查找5分钟内被修改过的属性的文件和目录**
`find` /etc -cmin -5

####  逻辑判断选项
**多条件判断的连接符**
`-a`and逻辑,需要两个条件都满足
`-o`or逻辑,两个条件满足任意一个即可
**在etc/ 下查找大于80MB同时小于100MB的文件**
_EXP_ find .etc -size +163840 -a -size -204800
_EXP_find /etc -name init* -a -type d  ++在etc/下查找以init开头的文件夹++
`-type`根据文件类型查找`f 文件`,`d 目录`,`l 软连接文件`




**对搜索结果执行操作**
`-exec/-ok [command] {} \；`  _在/etc下查找inittab文件并显示详细信息，不要忘记分号；_
* find /etc -name initttab -exec ls -l {} \  _-exec也可以换成-ok_
* 如果换成-ok 会有一个询问确认的环节，一个一个问你要不要执行_在执行删除的时候可以使用,进行二次确认_
**根据i节点查找**
`-inum` 可以直接查找i节点的文件,每个文件都会有一个独特的i节点++可以用于寻找硬链接++

#### 总结
* find
* -name
* -iname
* 通配符
* -size + / -
* -user     -group
* -amin   -cmin  -mmin
* -type   f d l
* -inum
* -a   -o
* -exec / -ok {} \;


















