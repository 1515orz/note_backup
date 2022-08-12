# yum命令


## 常用yunm命令

* 查询
`yum list` 查询所有可用软件包列表
`yum search [关键字]`  搜索服务器上所有关键字相关的包

* 安装
`yum -y install [包名]`  自动安装包
`install` 安装
`-y` 自动回答*yes*

* 升级
`yum -y update [包名]` **如果不写包名,会更新所有软件包**==如果升级了内核可能会宕机==
`update` 升级
`-y` 自动回答yes

* 卸载
`yum -y remove [包名]` yum卸载可能会误卸载掉其他支持组件/模块 ==尤其尽量不适用yum卸载==
`remove` 卸载
`-y` 自动回答yes

### 建议

    尽量手工安装,最小化安装,千万不要用yum更新,尽量不用yum卸载,但是由于可能卸载其他支持组件,存在危险性

## yum软件组管理命令

`yum grouplist` 列出所有可用的软件组列表
`yum groupinstall [软件组名]` 安装指定软件组,组名可以用`grouplist`查询出来
`tum groupremove [软件组名]` 卸载指定软件组
_如果需要安装的组名有空格,请使用双引号括起来_




