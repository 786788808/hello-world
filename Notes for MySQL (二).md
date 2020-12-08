函数篇：  
菜鸟教程有比较全的函数介绍https://www.runoob.com/mysql/mysql-functions.html  
这里记录一些比较常用的。  
>
#### 1. str_to_date(str,format) 将字符串str转换为日期型数据，format是日期型数据的格式  
|  format   | 描述  |
|  ----  | ----  |
| %Y  | 年，4 位 |
| %y  | 年，2 位 |
| %M  | 月名 |
| %b  | 缩写月名 |
| %m  | 月，数值(00-12) |
| %D  | 带有英文前缀的月中的天 |
| %d  | 月的天，数值(00-31) |
| %e  | 月的天，数值(0-31) |
| %H  | 小时 (00-23) |
| %h  | 小时 (01-12) |

```
select str_to_date('2020/11/11','%Y/%m/%d') as new_date;   
```
![](https://ftp.bmp.ovh/imgs/2020/12/780698d29d073850.png)  
>
#### 2. date_format(date,format) 按format指定的格式显示date
```
select date_format('2020-11-12 10:20:30','%Y-%m-%d') as new_date;
```
![](https://ftp.bmp.ovh/imgs/2020/12/4cb7001cc05337c9.png)    
>
#### 3. datediff(d1,d2) 计算日期 d1与d2 之间相隔的天数       
```
select datediff('2020-11-11','2020-11-12') as diff_date;	
```
![](https://ftp.bmp.ovh/imgs/2020/12/a14dbd79c039095a.png)   
>
#### 4. trim(str) 去除字符串str开始和结尾处的空格
```
select trim('    monday    ') AS trimmed_string;
```
![](https://ftp.bmp.ovh/imgs/2020/12/53b5745e978b58c5.png)

>
#### 5. rtrim(str) 去除字符串str右边的空格
```
select rtrim('    monday    ') as r_trimmed_string;
```
![](https://ftp.bmp.ovh/imgs/2020/12/5e90db0ad26433ce.png)
>
#### 6. ltrim(str) 去除字符串str左边的空格
```
select ltrim('    monday    ') as l_trimmed_string;
```
![](https://ftp.bmp.ovh/imgs/2020/12/2c292995bd6d7abe.png)
>
#### 7. replace(str,s1,s2) 将字符串 s2 替代字符串 str 中的字符串 s1
```
select replace('aaabbbaaa','a','0') as rep_str;
```
![](https://ftp.bmp.ovh/imgs/2020/12/468ca30869b88b91.png)  
>
#### 8. 未完







