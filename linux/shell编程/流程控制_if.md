# 流程控制_if


## 单分支 IF 语句

    IF语句类似于 [ 判断命令 ] && echo yes || echo no
    
> 单分支if条件语句

```
if [ 条件判断式 ];then # if和then放在一起需要号分隔
    main
if

# 或者这样写
if [ 条件判断式 ]
    then
        main
if
```

* 单分支条件语句需要注意的几个点
> if语句使用fi结尾, 和一般语言使用大括号结尾不同
>` [ 条件判断式 ]`就是使用`test`命令判断, 所以中括号和条件判断式之间必须有空格
> then后面根符合条件之后执行的程序, 可以放在[]之后, 用`;`分隔, 也可以换行写入, 就不用`;`了

### IF 例子

统计根分区使用率
```
# 把根分区使用率作为变量赋予变量rate
rate=$(df -h | grep "dev/sda1" | awk '{print $5}' | cut -d "%" -f1)

# 如果超过阈值则报警
if [ $rate -ge 80 ]
        then
            echo "Warning /dev/sda1 is full!!"
fi

```
> 定时命令
> 将需要重复执行的行为写入脚本, 定时执行, 省下大多数工作量

## 双分支 IF 条件语句

```
if [ 条件判断式 ]
    then
        main1
    else
        main2
if
```

### 双分支例子

> 备份`/etc`目录

```
#!/bin/bash

date=$(date +%y%m%d) # 赋值date变量
size=$(du -sh /etc)  # 赋值size变量

if [ -d /tmp/dbback ] # 如果文件夹存在
        then
                echo "Date is : $date" > /tmp/dbback/db.txt
                echo "Size is : #size" >> /tmp/dbback/db.txt
                cd /tmp/dbback
                # 将/etc目录和db.txt打包到一起
                tar -zcf etc_$date.tar.gz /etc db.txt &>/dev/null
                rm -rf /tmp/dbback/db.txt  # 删除打包之前的日志文件
        else  # 假如不存在/tmp/dbback这个目录
                mkdir /tmp/dbback/db.txt
                # 下面的步骤和上面相同
                echo "Date is : $date" > /tmp/dbback/db.txt
                echo "Size is : #size" >> /tmp/dbback/db.txt
                cd /tmp/dbback
                tar -zcf etc_$date.tar.gz /etc db.txt &>/dev/null
                rm -rf /tmp/dbback/db.txt
fi
```

> 判断是否启动apache
> 可以用于判断所有服务, 定期检查服务是否宕机并重新启动
> 有些时候服务虽然存在, 但是已经不能响应了, 建议使用`nmap`命令

**一个常用的检测服务脚本**

```
#!/bin/bash
# 判断apache服务宕了没, 并自动重启
  
# 将nmap扫描的apache服务状态赋值给port
port=$(nmap -sT localhost | grep tcp | grep http | awk '{print $2}')

# 判断服务是否启动, 执行分支结果 
if [ $port == "open" ] # 一定要加空格!!
        then    
                # 输出信息并记录到日志(覆写成功日志)
                echo "$(date) apache2 is ok!" >> /tmp/autostart-acc.log
else    
        # 重启服务, 用绝对路径, 不用service命令
        /etc/rc.d/init.d/apache2 start &>/dev/null
        # 输出信息并记录到日志
        echo "$(date) restart apache2" >> /tmp/autostart-err.log
fi
# 可以定时执行, 比较常用使用
```



## 多分支if语句

```
if [ 条件判断1 ]
    then
        条件成立时,执行main1
elif [ 条件判断2 ]
    then
        条件成立时, 执行main2
else
    所有条件都不成立, 执行main3
fi # 记得加fi
```

### 多分支案例

```
#!/bin/bash

# 脚本判断用户输入的是什么文件

# 接受键盘的输入, 并赋予变量file
read -p "Please input a filename: " file

# 判断file变量是否为空
if [ -z "$file" ]
        then
                echo "error, please input a filename"
                exit 1 # exit是必要的, 否则脚本会继续执行
 # 判断file是否存在, 取反
        elif [ ! -e "$file" ]
                then
                        echo "Your input is not a file"
                        exit 2
        elif [ -f "$file" ]
            then
                echo "$file is a regular file!"
        elif [ -d "$file" ]
            then
                echo "$file is a directory"
        else
                echo "$file is a other file"
fi
```

### 案例小结

* 程序进入报错时, 一定要添加退出(返回错误码)
* 可以定义date变量`date=$(date +%y%m%d)`作为"年月日"的数字格式
* 为新文件命名时, 增加$date的标识字, 可以避免覆盖操作
* 做字符串判断操作时, 一定要两头加空格
* 记得在最后加`fi`