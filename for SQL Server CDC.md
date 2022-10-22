## It's for SQL Server CDC   
### 1.下载并安装SQL Server,sql server management studio(free free, 不需要装破解版，安装教程后面补上)    
https://www.microsoft.com/en-us/sql-server/sql-server-downloads  
https://learn.microsoft.com/zh-cn/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16  
![image](https://user-images.githubusercontent.com/32427537/197346596-9bdfe1a7-3d85-4a51-8737-63103bbd2bf5.png)  
![image](https://user-images.githubusercontent.com/32427537/197346710-5bf32a43-bd29-482b-819e-be70382251cd.png)

### 2.建立新Database，新table 
新建Database HushDB_001,
`select is_cdc_enabled, * from sys.databases where name='HushDB_001'`  
`GO`  
![image](https://user-images.githubusercontent.com/32427537/197346960-af4a31c0-b831-40a8-bc45-9cb27bbda417.png)  

### 3.enable CDC(Database level and table level)


### 
