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




### 3.enable CDC(Database level and table level)
验证
`select is_cdc_enabled, * from sys.databases where name='Hush_DEMO'`  
`GO`  
![image](https://user-images.githubusercontent.com/32427537/197347165-3f7953c7-6e8e-4f19-8302-cfb62e9d324d.png)

### 
