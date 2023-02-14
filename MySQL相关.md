MySQL相关

CREATE DATABASE IF NOT EXISTS accessdb DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
grant all privileges on db_one.* to 'lufafen'@'%';
FLUSH PRIVILEGES;
SHOW GRANTS FOR 'lufafen'@'%';
REVOKE ALL ON mytest.* FROM 'lufafen'@'%';
ALTER user 'root'@'localhost' IDENTIFIED BY '123456'; --初始化密码修改

mysql5.7 忘记root密码
1、修改MySQL的配置文件（默认为/etc/my.cnf）,在[symbolic-links=0]下添加一行skip-grant-tables
2、保存配置文件后，重启MySQL服务 service mysqld restart
3、再次进入MySQL命令行 mysql -uroot -p,输入密码时直接回车，就会进入MySQL数据库了，这个时候按照常规流程修改root密码即可。
mysql -uroot -p
mysql> use mysql;
mysql> update user set authentication_string=password('新密码') where user='root' and Host='localhost';
mysql> flush privileges;
mysql> quit;
mysql5.7 修改密码

--使用mysqladmin在命令行修改密码
mysqladmin -u username -h hostname -p password "new-password"
-- 修改MySQL库的user表
UPDATE mysql.user SET authentication_string = PASSWORD("new-password");
FLUSH PRIVILEGES;
--使用set语句修改密码
-- 1.修改当前用户密码：
SET PASSWORD = PASSWORD("new-password");
-- 2.修改其他用户密码：
SET PASSWORD FOR 'user'@'hostname' = PASSWORD("new-password");
--使用ALTER USER语句修改用户密码
--修改当前用户密码（USER()为获取当前连接用户的函数）：
ALTER USER USER() IDENTIFIED BY 'new-password';


