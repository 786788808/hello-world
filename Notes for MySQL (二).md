#### 1. str_to_date(str,format) 将字符串str转换为日期型数据，format是日期型数据的格式  
format:
%Y: 年，4 位
%y: 年，2 位

```
select str_to_date('2020/11/11','%Y/%m/%d') as new_date;   
```
![](https://ftp.bmp.ovh/imgs/2020/12/780698d29d073850.png)  
https://www.runoob.com/mysql/mysql-functions.html  
>
#### 2. date_format(date,format) 按format指定的格式显示date
```
select date_format('2020-11-12 10:20:30','%Y-%m-%d') as new_date;
```
![](https://ftp.bmp.ovh/imgs/2020/12/4cb7001cc05337c9.png)    
>
#### 3. datediff(d1,d2) 计算日期 d1->d2 之间相隔的天数       
```
select datediff('2020-11-11','2020-11-12') as diff_date;	
```
![](https://ftp.bmp.ovh/imgs/2020/12/a14dbd79c039095a.png)   
