## It's for SQL Server CDC   
### 1.下载并安装SQL Server,sql server management studio  
(*free free*, 不需要装破解版，安装教程后面补上)    
https://www.microsoft.com/en-us/sql-server/sql-server-downloads    
https://learn.microsoft.com/zh-cn/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16  
![image](https://user-images.githubusercontent.com/32427537/197346596-9bdfe1a7-3d85-4a51-8737-63103bbd2bf5.png)  
![image](https://user-images.githubusercontent.com/32427537/197346710-5bf32a43-bd29-482b-819e-be70382251cd.png)

### 2.建立新Database，新table 
新建Database Hush_DEMO,  
![image](https://user-images.githubusercontent.com/32427537/197347605-f1275482-d208-45b5-b427-49a1c34e87a0.png)


USE Hush_DEMO 
GO 
SELECT [name], database_id, is_cdc_enabled  
FROM sys.databases       
GO  
![image](https://user-images.githubusercontent.com/32427537/197348157-a2738028-676e-4614-bd18-4e00e2190ebd.png)


create table dbo.student  --创建表student
(sno char(4) primary key,
sname char(8),
sage int,
ssex char(2),
sdept char(20)
);


create table dbo.course  --创建表course
(cno char(4) primary key,
cname char(8),
cpno char(4),
ccredit int
);


create table dbo.sc  --创建表sc
(sno char(4) primary key,
cno char(4),
grade int
);


### 3.enable CDC(Database level and table level)
#### 3.1 Database level
`GO`   
`EXEC sys.sp_cdc_enable_db`  
`GO`  

验证:  
`GO`  
`SELECT [name], database_id, is_cdc_enabled`      
`FROM sys.databases`            
`GO`       
 
![image](https://user-images.githubusercontent.com/32427537/197348245-44875e69-d08b-472e-8d43-fd304601bae3.png)  

#### 3.2 Table level

