# sql server
### 1.查询数据库大小、空间使用情况  
`EXEC sp_spaceused;`    
`EXEC sp_spaceused @updateusage = N'TRUE';` --更具实时性的写法    
<img width="272" alt="屏幕截图 2022-05-21 175701" src="https://user-images.githubusercontent.com/32427537/169646440-d7ba2126-da3e-4d34-9cc7-96af9c8be5b7.png">  

### 2.查看sql server 版本
`select @@version;`

### 3.查看数据库状态
`select * from sys.databases;`  
`SELECT name FROM SYS.MASTER_FILES;`  
注意：对于 tempdb，sys.master_files显示初始 tempdb 大小。 这些值用作在启动 tempdb 时创建 tempdb 的SQL Server。 因此，tempdb 增长时，不会反映在视图中。 若要获取 tempdb 文件的当前大小，请查询 tempdb.sys.database_files。（官网说明）
`SELECT * FROM sys.database_file;`  
查询

