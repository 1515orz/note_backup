mysql数据库中的3个权限表：user 、db、 host

权限表的存取过程是：

1)先从user表中的host、 user、 password这3个字段中判断连接的IP、用户名、密码是否存在表中，存在则通过身份验证；

2)通过权限验证，进行权限分配时，按照user db tables_priv columns_priv的顺序进行分配。

 

2.用户操作与授权
1.查看现有用户
select user,host from mysql.user;

2.创建用户 
--(1)创建本地登录用户test,只可服务端登录
create user 'test'@'localhost' identified by '123';
--(2)指定ip：192.118.1.1的mjj用户登录
create user 'mjj'@'192.118.1.1' identified by '123';
--(3)指定ip：192.118.1.开头的mjj用户登录
create user 'mjj'@'192.118.1.%' identified by '123';
--(4)指定任何ip的mjj用户登录 
create use 'mjj'@'%' identified by '123';

3.删除用户
drop user '用户名'@'IP地址';

4.修改用户
rename user '用户名'@'IP地址' to '新用户名'@'IP地址';

5.修改密码
set password for '用户名'@'IP地址'=Password('新密码');
set password for 'root'@'localhost' = password('123456');

6.授权命令 
-- 授予数据库的增删改查权限
grant select,update,insert ,delete on dmc_db.* to  zx_root;
-- 立即生效 
flush  privileges;
-- grant 创建、修改、删除 MySQL 数据表结构权限。
grant create ,alter,drop on testdb.* to developer@'192.168.0.%';
-- grant 操作 MySQL 外键权限。
grant references on testdb.* to developer@'192.168.0.%';
-- grant 操作 MySQL 临时表权限。
grant create temporary tables on testdb.* to developer@'192.168.0.%';
-- grant 操作 MySQL 索引权限。
grant index on testdb.* to developer@'192.168.0.%';
-- grant 操作 MySQL 视图、查看视图源代码 权限。
grant create view on testdb.* to developer@'192.168.0.%';
grant show view on testdb.* to developer@'192.168.0.%';
-- grant 操作 MySQL 存储过程、函数 权限。
grant create routine on testdb.* to developer@'192.168.0.%'; -- now, can show procedure status
grant alter routine on testdb.* to developer@'192.168.0.%'; -- now, you can drop a procedure
grant execute on testdb.* to developer@'192.168.0.%';
-- grant 作用在表中的列上：
grant select(id, se, rank) on testdb.apache_log to dba@localhost;
-- grant 作用在存储过程、函数上：
grant execute on procedure testdb.pr_add to 'dba'@'localhost'
grant execute on function testdb.fn_add to 'dba'@'localhost'
-- 注意：修改完权限以后 一定要刷新服务，或者重启服务，刷新服务用：FLUSH PRIVILEGES。
--[批量授权]
-- grant 普通 DBA 管理某个 MySQL 数据库的权限 ,其中，关键字 “privileges” 可以省略。
grant all privileges on testdb to dba@'localhost'
-- grant 高级 DBA 管理 MySQL 中所有数据库的权限。
grant all on *.* to dba@'localhost'

 

7.允许远程连接

grant all privileges on *.* to dba@'%';

FLUSH PRIVILEGES

 

8.取消权限
-- 取消来自远程服务器的mjj用户对数据库db1的所有表的所有权限
revoke all on db1.* from 'mjj'@"%";  
-- 取消来自远程服务器的mjj用户所有数据库的所有的表的权限
revoke all privileges on '*' from 'mjj'@'%';
-- 回收权限select权限,如果权限不存在会报错
revoke  select on dmc_db.*  from  zx_root;  
-- 如果想立即看到结果使用
flush  privileges ;


3.授权说明与授权原则

-- 格式：grant privileges on databasename.tablename to 'username'@'host' IDENTIFIED BY 'PASSWORD';
(1)GRANT命令说明：
-- priveleges(权限列表),可以是all priveleges, 表示所有权限，也可以是select,update,delete,insert等权限，多个权限的名词,相互之间用逗号分开。
-- on用来指定权限针对哪些库和表。
-- *.* 中前面的*号用来指定数据库名，后面的*号用来指定表名。
-- to 表示赋权予用户, 如 jack@'localhost' 表示jack用户，@接主机，可以是IP、IP段、域名以及%，%表示任何地方。
-- identified by指定用户的登录密码,该项可以省略。
-- with grant option 这个选项表示该用户可以将自己拥有的权限授权给别人。

(2)授权原则说明：
-- a、只授予能满足需要的最小权限，防止用户干坏事。比如用户只是需要查询，那就只给select权限就可以了，不要给用户赋予update、insert或者delete权限。
-- b、创建用户的时候限制用户的登录主机，一般是限制成指定IP或者内网IP段。
-- c、初始化数据库的时候删除没有密码的用户。安装完数据库的时候会自动创建一些用户，这些用户默认没有密码。
-- d、为每个用户设置满足密码复杂度的密码。
-- e、定期清理不需要的用户。回收权限或者删除用户。

(3)注意点 
设置权限时必须给出一下信息
-- 1，要授予的权限
-- 2，被授予访问权限的数据库或表
-- 3，用户名
grant和revoke可以在几个层次上控制访问权限
-- 1，整个服务器，使用grant all和revoke all
-- 2，整个数据库，使用on database.*
-- 3，特点表，使用on database.table
-- 4，特定的列
-- 5，特定的存储过程
user表中host列的值的意义
-- %              匹配所有主机
-- localhost      localhost不会被解析成IP地址，直接通过UNIXsocket连接
-- 127.0.0.1      会通过TCP/IP协议连接，并且只能在本机访问；
-- ::1            ::1就是兼容支持ipv6的，表示同ipv4的127.0.0.1
————————————————
