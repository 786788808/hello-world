# SQL语句类型
SQL语句主要划分为以下几类：

- 1 DDL(Data Definition Language): 数据定义语言，定义对数据库对象(库、表、列、索引)的操作  
包括：CREATE、DROP、ALTER、RENAME、 TRUNCATE等
  
- 2 DML(Data Manipulation Language): 数据操作语言，定义对数据库记录的操作  
包括：INSERT、DELETE、UPDATE等
  
- 3 DCL(Data Control Language): 数据控制语言，定义对数据库、表、字段、用户的访问权限和安全级别  
包括：GRANT、REVOKE等
  
- 4 TCL(Transaction Control Language): 事务控制语言  
包括：COMMIT、ROLLBACK、SAVEPOINT等
  
- 5 DQL(Data Query Language): 数据查询语言  
最常用的SELECT，毕竟总不能每天都在建表删表建库删库等，学习重点在这里。    

### 3. DCL(Data Control Language): 数据控制语言，定义对数据库、表、字段、用户的访问权限和安全级别  
主要是GRANT（授权）命令、REVOKE（撤销）命令。      
一般用户也没有这个权限执行，只有大佬有权限。      
语法：GRANT/REVOKE  + 权限  +  TO/FROM  + 用户名称     

举例子：    
-- 1.授权BI用户查询scott的emp表(管理员)    
GRANT SELECT ON scott.emp TO BI;    
-- 2.回收权限(管理员)    
REVOKE SELECT ON scott.emp FROM BI;     

### 4. TCL(Transaction Control Language): 事务控制语言 
主要是 Commit 和 Rollback。    
什么时候要用到Commit 和 Rollback命令呢？那当然是做DML操作的时候啦！    
平时我们在做DML操作（包括insert插入、update更新、delete删除)的时候，即对数据表的数据进行行级别的操作的时候，只要你的操作在没有 COMMIT 和 ROLLBACK 前,都还在本机的 SESSION 中,还没有更新至数据库。是因为数据库怕你操作错误，所以数据库是没有保存 DML 操作后的结果的。只有你Commit或rollback后，才会将结果保存到数据库。    
如果确认无误则可以commit（提交），如果有误（或反悔）可以rollback（回滚）。  

记住，只有DML语言才有commit这一操作。因为，DDL是默认提交的，你执行后就直接对数据库进行了操作，根本回滚不了。  
