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



#### 授权

```mysql
GRANT privileges ON `databasename`.`tablename` TO 'username'@'host';
# eg:
# GRANT ALL ON `test`.* TO 'admin'@'%';
# GRANT SELECT ON `test`.`user` TO 'admin'@'%';
# GRANT UPDATE ON `test`.* TO 'admin'@'%';
```

> + privileges 用户的操作权限（如SELECT，UPDATE，INSERT等，见附录，给予所以权限使用ALL）
> + databasename 数据库名
> + tablename 数据表名

​	**注意:用以上命令授权的用户不能给其它用户授权,如果想让该用户可以授权,用以下命令:**

```mysql
GRANT privileges ON `databasename`.`tablename` TO 'username'@'host' WITH GRANT OPTION;
```



#### 撤销用户权限

```mysql
REVOKE privilege ON `databasename`.`tablename` FROM 'username'@'host';
```

> 说明参考授权部分