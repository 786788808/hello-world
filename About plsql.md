## PLSQL篇
#### 1.1 PL/SQL定义
PL/SQL(Procedure Language/SQL)是Oracle对sql语言的过程化扩展。  
其在SQL命令语句中增加了过程处理语句(分支、循环等),使SQL语言具有过程处理语句。

#### 1.2 程序结构
程序分为三部分：声明部分(以 Declare 开头)、执行部分(以 Begin 开头)、异常处理部分(以 Exception 开头)。    
```sql
Declare  
  --声明部分，可有可无，用于声明变量、游标  
Begin  
  --执行部分，必需部分   
Exception  
  --异常报错，可有可无  
End;  
```  
**注：**  
- 不区分大小写  
- 运行方式：在 Plsql Developer 工具的 Test Window 创建，执行，然后在DBMS Output可以看到输出结果。也可以在CMD执行
- 每一个命令语句结束后面必须加分号

e.g.: 举个简单的例子，打印 Hello,world!
这里不需要声明任何变量，只要最关键的Begin部分就行。  
```
Begin
  DBMS_output.put_line('Hello,world!');   --DBMS:Database Management System
End;
```
