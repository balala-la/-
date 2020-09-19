# Oracle

## 简介



## 登录

+ 进入cmd，输入sqlplus，唤出登录界面，输入用户名密码，当出现连接到...即表示连接成功；

  ```cmd
  Microsoft Windows [版本 10.0.18363.778]
  (c) 2019 Microsoft Corporation。保留所有权利。
  
  C:\Users\lee>sqlplus
  
  SQL*Plus: Release 11.2.0.1.0 Production on 星期日 9月 6 20:17:22 2020
  
  Copyright (c) 1982, 2010, Oracle.  All rights reserved.
  
  请输入用户名:  system
  输入口令:
  
  连接到:
  Oracle Database 11g Enterprise Edition Release 11.2.0.1.0 - 64bit Production
  With the Partitioning, OLAP, Data Mining and Real Application Testing options
  ```

  

+ 登录状态下切换用户(两种方式)

  ```cmd
  SQL> conn system/zxcvbnm2017;
  已连接。
  
  SQL> conn lee
  输入口令:
  已连接。
  ```

  



## 数据库用户的CRUD

+ 用户的创建

  ```sql
  create user UserName identified by PassWord;
  ```

+ 刚创建的用户无任何权限，甚至连登录的权限都没有，所以这里需要授权

  ```sql
  grant connect to lee;   --connect角色：
  ```



+ 用户密码的修改(两种方式)

  ```sql
  passw[ord] UserName;
  
  Alter user UserName identified by PassWord;
  ```

  ```cmd
  SQL> passw    //默认是修改当前用户
  更改 LEE 的口令
  旧口令:
  新口令:
  重新键入新口令:
  口令已更改
  
  SQL> Alter user lee identified by 123456;
  用户已更改。
  ```



+ 删除用户

  ```sql
  drop user UserName [cascade];
  ```

  ```cmd
  SQL> drop user lee;
  
  用户已删除。
  ```

  

+ 锁定/解锁用户

  ```sql
  alter user UserName account lock;	--锁定用户
  alter user UserName account unlock;	--解锁用户
  ```
```
  



+ 为用户设置配置文件

  1. 创建配置文件

  ```sql
  create profile Profile_Name limit failed_login_attempts 3 password_lock_time 1;
  --用户密码错误3次时锁定账户1天
  --1分钟等于1/1440天
```

  2. 绑定用户

  ```sql
  alter user UserName profile Profile_Name;
  ```

  

## 配置数据库进行远程登录

1. 在文件夹Oracle - OraDb11g_home1下找到Net Manager，双击进入；
2. 在lee(实例名)项目下把主机名改为计算机名，LISRENER项目下同理；![image-20200907124709752](C:\Users\lee\AppData\Roaming\Typora\typora-user-images\image-20200907124709752.png)
3. 修改后点击菜单栏”文件“，点击“保存网络配置”，关闭窗口；
4. 在服务中重启Oracle server服务



## 表空间

+ 查看数据库所有用户信息

  ```sql
  select * from all_users;
  ```



+ 表空间的创建

  ```sql
  create tablespace tablespace_Name datefile "文件路径" size 30m uniform size 128k;
  
  create tablespace liwenbing_space datafile 'F:\Oracle_data\student.dbf' size 30m uniform size 128k;  --实例
  ```



+ 数据表的创建

  ```sql
   create table table_Name ( name varchar(10), num number(3) ) tablespace tablespace_Name;
   
   create table class ( name varchar(10), num number(3) ) tablespace liwenbing_space;
   --新建一个表并指定给一个表空间
  ```



+ 设置表格显示不断行

  ```sql
  set wrap off
  set wrap on --相反，设置表格显示断行
  ```

+ sql状态下清除屏幕

  ```sql
  clear screen
  ```

+ 进入dos命令

  ```sql
  host
  ```

+ 退出dos，进入sql命令下

  ```sql
  exit
  ```

+ 修改会话级日期格式

  ```sql
   Alter session set nls_date_format = 'yyyy-mm-dd';
  ```

+ 查看当前Oracle默认日期格式

  ```sql
  select * from nls_session_parameters;
  select * from nls_instance_parameters;
  select * from nls_database_parameters;
  ```

  

+ 知道表名查询在某表空间

  ```sql
  select table_name,tablespace_name from user_tables where table_name='CLASS';
  															--后面表名称需要大写
  ```

+ 查询表空间下有多少数据表

  ```sql
  select table_name,tablespace_name from user_tables where tablespace_name='LIWENBING_SPACE';
  				--此表空间名也需大写
  ```



+ 修改数据文件大小

  ```sql
  alter database datafile 'F:\Oracle_data\student.dbf' resize 15m;
  ```

+ 设置数据文件自动增长

  ```sql
  alter database datafile 'F:\Oracle_data\student.dbf' autoextend on next 10m maxsize 500m;
  ```

+ 往表空间增加数据文件

  ```sql
  alter tablespace liwenbing_space add datafile 'F:\Oracle_data\teacher.dbf' size 10m; 
  --后面不可指定uniform size
  ```



+ 查看用户具有什么样的角色权限

  ```sql
  select * from dba_role_privs where grantee='LEE';
  ```

+ 查看角色具有什么样的系统权限

  ```sql
  select * from dba_sys_privs where grantee='DBA';
  ```

  

+ 查看默认表空间是谁

  ```sql
  select * from database_properties where property_name like 'DEFAULT%';
  ```

+ 修改默认表空间

  ```sql
  alter database default tablespace liwenbing_space;
  --将表空间liwenbing_space设置为默认的永久表空间。
  ```

  

