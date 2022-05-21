# sql server
### 1.查询数据库大小、空间使用情况  
`EXEC sp_spaceused;`    
`EXEC sp_spaceused @updateusage = N'TRUE';` --更具实时性的写法    
<img width="272" alt="屏幕截图 2022-05-21 175701" src="https://user-images.githubusercontent.com/32427537/169646440-d7ba2126-da3e-4d34-9cc7-96af9c8be5b7.png">  

### 2.查看sql server 版本
`select @@version;`

