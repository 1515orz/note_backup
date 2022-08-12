# yum在线管理

_yum可以自动从服务器下载依赖的包,自动解决依赖性的问题,既可以上网下载,也可以本地解决_但是redhat在红帽子需要收费

* yum不是包，是(在线)管理命令

## ip地址配置和网络yum源
_setup 仅限红帽_
* `service network restart` 重启网络服务

`vi /etc/yum.repos.d/CentOS-Base.repo` 进入文件修改yum源
* [base] 容器名称,一定要放在[]中
* name 容器说明,可以自己随便写
* mirrorlist 镜像站点,这个可以注释掉
* baseurl 我们的yum**源服务器**地址,默认是CentOS官方的yum源服务器,是可以使用的,如果你觉得慢可以改成你喜欢的yum源地址
* enabled 此容器是否生效,如果不写或写成enable = 1 都是生效,写成enable = 0就是不生效
* gpgkey 如果是1是指RPM的数字证书生效,如果是0则不生效
* 数字证书的公钥文件保存位置,不用修改



