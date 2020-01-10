## 用户管理

DCL权限授予和回收

1. 使用mysql库

   `use mysql;`

2. 创建用户及密码

   `create user 用户名@ip地址 identified by '密码';`

   `create user exile@127.0.0.1 identified by '123456';`

3. 更改密码

   `set password for 用户名=password('新密码');`

4. 登录远程mysql

   `mysql -h ip地址 -u用户名 -p密码;`，这是DOS命令

5. 查看当前登录的用户

   `select user();`

   或者

   `select current_user();`

6. 删除用户

   `drop user 用户名@ip;`，删除用户

7. 赋予用户指定的权限给指定的数据库

   `grant 权限1,权限2 on 数据库名.* to 用户名@ip;`

   `grant select,insert on jsd.* to exile;`

8. 回收权限

   如果权限不存在会报错

   `revoke 权限1,权限2 on 数据库.* from 用户名@ip;`

   `revoke select,insert on jsd.* from exile;`

9. 查看用户权限

   `show grants for 用户名@IP;`

   



















