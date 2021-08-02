## PLSQL篇
### 1.1 PL/SQL定义
PL/SQL(Procedure Language/SQL)是Oracle对sql语言的过程化扩展。  
其在SQL命令语句中增加了过程处理语句(分支、循环等),使SQL语言具有过程处理语句。  

### 1.2 程序结构  
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
- 运行方式：
    - 在 Plsql Developer 工具的 Test Window 创建，执行，然后在 DBMS Output 可以看到输出结果。也可以在 CMD 执行  
    - 在 CMD 窗口敲 sqlplus,输入用户、密码。然后运行代码set serveroutput on;  
- 每一个命令语句结束后面必须加分号  

e.g.1: 举个简单的例子，打印 Hello,world!  
这里不需要声明任何变量，只要最关键的 Begin 部分就行。    
```
## test window
Begin
  DBMS_output.put_line('Hello,world!');   --DBMS:Database Management System
End;
```
```
## sqlplus（CMD 开启）
set serveroutput on;  --有输出，要先开启输出选项
Begin
  DBMS_output.put_line('Hello,world!');   --DBMS:Database Management System
End;
/
```

e.g.2: 对 emp_cp 表进行一些 DML 操作  
这里不涉及声明变量部分，DML 操作可以直接在 Begin 执行部分直接进行  
```sql
BEGIN
  INSERT INTO emp_cp
  SELECT * FROM emp WHERE deptno=10;
  --
  UPDATE emp_cp SET empno = 888888888888 WHERE empno=7782;
  --
  DELETE FROM emp_cp WHERE empno=7934;
END;
```

### 1.4 变量
PLSQL编程中常见的变量分为两大类：      
1.普通数据类型(char, varchar2, date, number, boolean, long)  --PLSQL 中有 boolean，但是原本 Oracle 中没有该数据类型，一般用 char(1) 或 number(1) 表示    
2.特殊变量类型(引用型变量，记录型变量)    

声明变量或常量必须指明变量的数据类型,也可以声明变量时对变量初始化,变量声明必须在声明部分。  
声明变量：  
变量名 变量数据类型(变量长度) [ :=初始值]  
	代码演示：声明变量或常量（使用 CONSTANT 关键字声明常量）

声明变量：    
变量名 变量类型(变量长度)  

e.g.:  
```sql
Declare
  v_name varchar2(123);  -- 一定要记住分号;
  v_weight number(4,1);
Begin
  …
End;
```

###

1.PL/SQL介绍
	Oracle PL/SQL语言（Procedural Language/SQL）是结合了结构化查询与Oracle自身过程控制为一体的强大语言，
	PL/SQL不但支持更多的数据类型，拥有自身的变量声明、赋值语句，而且还有条件、循环等流程控制语句。过
	程控制结构与SQL数据处理能力无缝的结合形成了强大的编程语言，可以创建过程和函数以及程序包。

	
	
  
2.PL/SQL基础
	2.1语法结构：PL/SQL块的语法
	[DECLARE                            -- 声明部分
		 --declaration statements]①     -- 声明变量、常量、游标等（声明的内容可以不在执行部分使用）
	BEGIN                               -- 执行部分
		 --executable statements  ②     -- 对于执行部分不能去定义变量等（使用的变量、常量、游标等必须在声明的内容中）
	[EXCEPTION                          -- 异常处理
		 --exception statements]  ③
	END;                                -- 分号不能省略
	
	注意： 每一个命令语句结束后面必须加分号
	
	
	特殊符号：
	:= 赋值     v_cnt := 6;  对变量赋值为6
	.. 连续值   1..6         表示1到6的整数
	** 求幂     3**2         3的2次方为9
	


     DECLARE                            -- 声明部分
   	    -- DQL(显式游标)
     BEGIN                               -- 执行部分
		-- DDL(动态sql)
		-- DCL(动态sql)
		-- DML(直接使用)
		-- TCL(直接使用)
		-- DQL(隐式游标)
     EXCEPTION                          -- 异常处理
     END;  



    2.2声明与赋值
	声明变量或常量必须指明变量的数据类型,也可以声明变量时对变量初始化,变量声明必须在声明部分。
	变量名 数据类型[ :=初始值]
	代码演示：声明变量或常量（使用 CONSTANT 关键字声明常量）
	
	
	-- 1.没有变量/常量
    BEGIN
	  -- dml 语句可以直接运行
   	  INSERT INTO emp_cp
      SELECT * FROM emp WHERE deptno=10;
      --
   	  UPDATE emp_cp SET empno = 888888888888 WHERE empno=7782;
      --
   	  DELETE FROM emp_cp WHERE empno=7934;
   	END;
  


	-- 2.有变量/常量
	DECLARE
	  v_empno  NUMBER(4);                -- 声明变量
	  --   v_empno  NUMBER(4):=123;     -- 声明变量并赋值（后面可以被重新赋值）
	  c_deptno CONSTANT NUMBER(2):=99;   -- 声明常量并赋值（后面不能被重新赋值）
	BEGIN
	  v_empno :=123;
	  -- c_deptno :=77;  -- 常量不能被重新赋值
	  INSERT INTO emp_cp(empno,deptno) VALUES(v_empno,c_deptno);
	  COMMIT;
	END;


	-- 3.异常处理
    -- 输入两个数字变量, 计算变量的商,并打印出来
    DECLARE
      V_1 NUMBER(4);
      V_2 NUMBER(4);
    BEGIN
      V_1 :=100;
      V_2 :=&输入分母;  -- &取地址,可以从键盘输入值,如果是字符类型需要输入时加单引号
      DBMS_OUTPUT.PUT_LINE(V_1||'除以'||V_2||'='||(V_1/V_2));  -- 打印内容 
    EXCEPTION WHEN ZERO_DIVIDE  -- 异常匹配
  	  THEN DBMS_OUTPUT.PUT_LINE('分母为0！'); 
    END;


    ---- 通用异常
    DECLARE
      V_1 NUMBER(4);
      V_2 NUMBER(4);
    BEGIN
      V_1 :=100;
      V_2 :=&输入分母;  -- &取地址,可以从键盘输入值 
      DBMS_OUTPUT.PUT_LINE(V_1||'除以'||V_2||'='||(V_1/V_2));  -- 打印内容 
    EXCEPTION WHEN OTHERS  -- 通用异常处理
  	  THEN DBMS_OUTPUT.PUT_LINE(SQLERRM); 
    END;
	


		 
     练习：1.设置三个变量,  v_1、v_2、v_3, 分别将自己的姓名、性别和专业赋值给这三个变量, 并将三个变量拼接在一起打印出来！
             如打印结果：姓名：张三  性别：男  专业：统计学！
	       2.给定部门编号变量并输入值, 将emp_cp对应的部门编号的数据的人员奖金更新为100
     
###
DECLARE
  v_1 varchar2(10);
  v_2 varchar2(10);
  v_3 varchar2(10);
begin 
  v_1 :='&请输入你的姓名'
  v_2 :='&请输入你的性别，男或女'
  v_3 ：='&请输入你的专业'
  dbms_output.put_line('姓名：'||v_1||' 性别：'||v_2||' 专业：'||v_3||'!')
end;
###




####
1.
法1：
 DECLARE
              v_1 VARCHAR2(20);
              v_2 VARCHAR2(20);
              v_3 VARCHAR2(20);
            BEGIN
              -- 字符型，输入的时候加单引号
              v_1 :=&输入姓名;   ###或者v_1 :='&输入姓名'; 这种在弹出窗口不用写单引号
              v_2 :=&输入性别;
              v_3 :=&输入专业;
              DBMS_OUTPUT.PUT_LINE('姓名：'||v_1||' 性别：'||v_2||' 专业：'||v_3);
            END;
法2：
DECLARE
  v_1 varchar2(10);
  v_2 varchar2(10);
  v_3 varchar2(10);
begin 
  v_1 :='&请输入你的姓名';
  v_2 :='&请输入你的性别男或女';
  v_3 :='&请输入你的专业';
  dbms_output.put_line('姓名：'||v_1||' 性别：'||v_2||' 专业：'||v_3||'!');
end;
####

###		   
1.
DECLARE
  v_1 varchar2(20);
  v_2 varchar2(5);
  v_3 varchar2(10);
BEGIN
  v_1 :='AAA';
  v_2 :='女';
  v_3 :='应用统计学';
  DBMS_OUTPUT.PUT_LINE('姓名：'||v_1||' 性别：'||v_2||' 专业：'||v_3||'!');
END;
###

2.
####
DECLARE
  v_depnto NUMBER(4);
BEGIN
  v_depnto :=&输入部门号;
  UPDATE emp_cp SET comm=100 WHERE deptno=v_depnto;
  COMMIT;
END;
####

 


















	



