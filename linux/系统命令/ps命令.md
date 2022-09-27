# ps命令



`ps aux` 查看当前所有系统进程

    ps可以判断当前服务和进程, 但有时服务虽然存在, 但其实已经无响应了
    所以用ps判断服务是否正常运行不一定准
   
---
 
`USER` 进程的当前用户
`PID` process ID的缩写, 就是进程号
`PPID` 父进程ID
`VSIZE` vitrual size 进程虚拟地址空间大小
`RSS` 进程正在使用的物理内存大小
`WCHAN` 进程如果处于休眠状态的化, 在内核中的地址
`PC` program counter
`NAME` 进程的名称




`ps aux  | head -n 1 ; ps aux | sort -k 3 -rn | head`
查看最耗费cpu的前几个进程

ps aux | head -n 1是打印ps aux的标题栏

而ps aux | sort -k 3 -rn | head是查询ps aux将按照第三列(sort -k 3 -rn)进行降序排序， 而最后的head是提取前10个结果

---

