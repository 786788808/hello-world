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


`USE Hush_DEMO`   
`GO`   
`SELECT [name], database_id, is_cdc_enabled`    
`FROM sys.databases`         
`GO`    
![image](https://user-images.githubusercontent.com/32427537/197348157-a2738028-676e-4614-bd18-4e00e2190ebd.png)


create table dbo.student  --创建表student
(sno char(4) primary key,
sname char(8),
sage int,
ssex char(2),
sdept char(20),
StartTime datetime
);

create table dbo.course  --创建表course
(cno char(4) primary key,
cname char(8),
cpno char(4),
ccredit int,
StartTime datetime
);

create table dbo.sc  --创建表sc
(sno char(4) primary key,
cno char(4),
grade int,
StartTime datetime
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
`SELECT name, is_tracked_by_cdc from sys.tables;`    
![image](https://user-images.githubusercontent.com/32427537/197378587-e992b24e-5e2d-49a9-9150-73633dd8e5fb.png)


`GO`   
`EXEC sys.sp_cdc_enable_table`   
`@source_schema = N'dbo',`   
`@source_name   = N'student',`   
`@role_name     = NULL`   
`GO`  

![image](https://user-images.githubusercontent.com/32427537/197378622-f17f25e0-8c73-46c4-a2bb-5755dec07b46.png)
![image](https://user-images.githubusercontent.com/32427537/197378657-b74b3428-f19a-42a0-a9a4-442bbcf7e3ec.png)


Select * from CDC.dbo_sc_CT;
sp_columns dbo_sc_CT;

#### 4.operation
`BEGIN TRANSACTION;`

`insert into dbo.sc `
`values`
`('11','21',78,getdate()),`
`('111','22',88,getdate()),`  
`('110','23',98,getdate()),`  
`('119','24',108,getdate()),`  
`('22','21',79,getdate()),`  
`('27','22',89,getdate()),`  
`('222','23',99,getdate()),`  
`('227','24',109,getdate()),`  
`('33','21',59,getdate()),`  
`('333','22',69,getdate()),`  
`('339','23',59,getdate()),`  
`('336','24',79,getdate()),`  
`('44','21',78,getdate()),`  
`('444','22',88,getdate()),`  
`('448','23',98,getdate()),`  
`('445','24',108,getdate());`  

`update dbo.sc set sno = 'aaaa' where sno ='21';`  
`update dbo.sc set grade = 100 where cno ='110' and sno='23';`  
`update dbo.sc set sno = 'bbbb' where sno ='22';`  
`update dbo.sc set grade = 0 where sno ='24';`  

`COMMIT TRANSACTION;`  
 
----- 
`BEGIN TRANSACTION;`  
  
`update dbo.sc set grade =100 where cno ='21';`  
`update dbo.sc set grade =1000 where cno ='21';`  
`  
`COMMIT TRANSACTION;`  

`select * from dbo.sc;`  
`select * from cdc.dbo_sc_CT;`  
