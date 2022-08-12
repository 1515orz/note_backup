# dd命令

`dd if=输入文件 of=输出文件 bs=字节数 count=个数` 可以当作_磁盘拷贝命令_
`if=输入文件` 指定源文件或原设备
`of=输出文件` 指定目标文件或目标设备
`bs=字节数` 指定一次输入/输出多少字节,即把这些字节看作一个数据块
`count=个数` 指定输入/输出多少个数据块

_EXP_
`date ; dd if=/dec/zero of=root/testfiles bs=1k count=1000000 ; date`