# ps命令

ps命令是process status的缩写, 用于列出系统中当前正在运行哪些进程, 就是执行ps命令那个时刻那些进程的快照,使用该命令可以确定有哪些进程 正在运行 和 运行的状态、进程是否结束、进程有没有僵死、哪些进程占用了过多的资源等等。总之大部分信息都是可以通过执行该命令得到的

`ps aux` 查看当前所有系统进程

    ps可以判断当前服务和进程, 但有时服务虽然存在, 但其实已经无响应了
    所以用ps判断服务是否正常运行不一定准
   
---

## ps头部
 
`USER` 进程的当前用户
`PID` process ID的缩写, 就是进程号
`PPID` 父进程ID
`VSIZE` vitrual size 进程虚拟地址空间大小
`RSS` 进程正在使用的物理内存大小
`WCHAN` 进程如果处于休眠状态的化, 在内核中的地址
`PC` program counter
`NAME` 进程的名称

## ps参数

`-a` 列出所有用户
`-u` 列出状态
`-x` 列出更详细的信息

---


### ps常见用法

`ps -aux | grep "xxx"` 查看特定的进程
`ps -ef | grep "xxx" ` 查看特定进程

`ps -aux --sort -pcpu | head ` 对后台占用cpu的进程进行排序
`ps -aux --sort -pmem | head` 对后台占用内存最多的进程进行排序

`ps aux | head -n 1 ; ps aux | sort -k 3 -rn | head`
查看最耗费cpu的前几个进程

> 结合watch命令对占用cpu最高的进程进行动态监测
`watch -n 1 'ps -aux --sort -pcpu | head -5'`
每隔1秒刷新，输出占用cpu最高的五个进程

> 同时对cpu和内存进行监测
`watch -n 1 'ps -aux --sort -pcpu,+pmem | head -5'`

---

