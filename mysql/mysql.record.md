## Mysql 学习记录

[TOC]

### Mysql命令行添加用户



#### 创建用户

```mysql
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
# eg:
# CREATE USER 'admin'@'localhost' IDENTIFIED BY '123456';
# CREATE USER 'admin'@'%' IDENTIFIED BY '';
# CREATE USER 'admin'@'%';
```

> + username 将创建的用户名
> + host 指定用户可以哪个主机进行登录（本地主机可用localhost，任意主机都可登录可用通配符%）
> + password 用户登录密码（可为空，则用户不需要密码就可登录）



#### 设置、更改密码

```mysql
SET PASSWORD FOR 'username'@'host' = PASSWORD('newpassword');
# 设置当前登录用户密码
SET PASSWORD = PASSWORD('newpassword');
```



#### 删除用户

```mysql
DROP USER 'username'@'host';
```



#### 授权

```mysql
GRANT privileges ON `databasename`.`tablename` TO 'username'@'host';
# eg:
# GRANT ALL ON `test`.* TO 'admin'@'%';
# GRANT SELECT ON `test`.`user` TO 'admin'@'%';
# GRANT UPDATE ON `test`.* TO 'admin'@'%';
```

> + privileges 用户的操作权限（如SELECT，UPDATE，INSERT等，见[附录](#附录)，给予所以权限使用ALL）
> + databasename 数据库名
> + tablename 数据表名

​	**注意:用以上命令授权的用户不能给其它用户授权,如果想让该用户可以授权,用以下命令:**

```mysql
GRANT privileges ON `databasename`.`tablename` TO 'username'@'host' WITH GRANT OPTION;
```



#### 查看权限

```mysql
SHOW GRANTS FOR ‘pig’@'%’; 
```



#### 撤销权限

```mysql
REVOKE privilege ON `databasename`.`tablename` FROM 'username'@'host';
```

> 说明参考授权部分
>
> 该部分功能需要验证下



#### 刷新，生效设置

```mysql
FLUSH PRIVILEGES;
```



### 附录

#### MySQL用户操作权限

```mysql
ALTER
Allows use of ALTER TABLE. 
    
ALTER ROUTINE 
Alters or drops stored routines. 
    
CREATE
Allows use of CREATE TABLE. 
    
CREATE ROUTINE 
Creates stored routines. 
    
CREATE TEMPORARY TABLE
Allows use of CREATE TEMPORARY TABLE. 
    
CREATE USER
Allows use of CREATE USER, DROP USER, RENAME USER, and REVOKE ALL PRIVILEGES. 
    
CREATE VIEW
Allows use of CREATE VIEW. 
    
DELETE
Allows use of DELETE. 
    
DROP
Allows use of DROP TABLE. 
    
EXECUTE
Allows the user to run stored routines. 
    
FILE 
Allows use of SELECT… INTO OUTFILE and LOAD DATA INFILE. 
    
INDEX
Allows use of CREATE INDEX and DROP INDEX. 
    
INSERT
Allows use of INSERT. 
    
LOCK TABLES 
Allows use of LOCK TABLES on tables for which the user also has SELECT privileges. 
    
PROCESS 
Allows use of SHOW FULL PROCESSLIST. 
    
RELOAD 
Allows use of FLUSH. 
    
REPLICATION 
Allows the user to ask where slave or master 
    
CLIENT 
servers are. 
    
REPLICATION SLAVE 
Needed for replication slaves. 
    
SELECT
Allows use of SELECT. 
    
SHOW DATABASES 
Allows use of SHOW DATABASES. 
    
SHOW VIEW
Allows use of SHOW CREATE VIEW. 
    
SHUTDOWN 
Allows use of mysqladmin shutdown. 
    
SUPER 
Allows use of CHANGE MASTER, KILL, PURGE MASTER LOGS, and SET GLOBAL SQL statements. Allows mysqladmin debug command. Allows one extra connection to be made if maximum connections are reached. 
    
UPDATE
Allows use of UPDATE. 
    
USAGE 
Allows connection without any specific privileges.
```



### 参考

+ [原文](https://my.oschina.net/stategrace/blog/202377)

