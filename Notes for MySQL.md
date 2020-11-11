#### 背景：记录易错点、记不牢的用法
![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605002521399&di=72e676fa3edc82057487583ddeaca248&imgtype=0&src=http%3A%2F%2Fwx1.sinaimg.cn%2Flarge%2Fbf976b12gy1g3b987cv7ag208c07k0td.gif)

```MySQL
# 删除一列：
Alter Table `all_orders_amazon_copy1` Drop Column `下单日期`;   
	
# 删除多列：

Alter Table `all_orders_amazon_copy1`  
			Drop Column `下单日期`,   
			Drop Column `下单时间`; 
			
# 新增单列：
alter table `all_deliveries_amazon_copy1`
    add column `下单日期` varchar(30) comment '太平洋时间' after `purchase-date`;

# 新增多列：  
例一：  
alter table `all_deliveries_amazon_copy1`
    add column `下单日期` varchar(30) comment '太平洋时间' after `purchase-date`,
    add column `下单时间` varchar(30) comment '太平洋时间' after `purchase-date`;
例二：  
alter table `sku_pure_copy1`
add column `listing_birth` date after `FNSKU`,
add column `status` enum('在售','下架') not null comment '销售状态' after `listing_birth`;  
例三：
alter table `sku_adv`
add column `curr_status` enum('开启','暂停', '0000') not null default '0000' comment '0000代表不清楚，暂时没统计';

# 更改列的数据类型：  
alter table `all_orders_amazon_copy1`
    modify Column `下单时间` TIME Comment '太平洋时间';

# 更改一整列的数据：
update `all_orders_amazon_copy1`
    set `下单日期`= left(`purchase-date`,10);

# 更改多列的数据：  
例一：  
update `all_deliveries_amazon_copy1`
	set `下单日期` = LEFT(`purchase-date`,10),
	    `下单时间` = MID(`purchase-date`,12,8);  
例二：  
update `sku_adv`
set `店铺` = trim(`店铺` ),
	  `SKU` = trim(`SKU`);

# 聚集函数 count()
selet count(*), select count(1) 与 select count(column_name)的区别：
说明：这三个都是用来数行数的，但是前两个包含null值，后者不含null值，所以前两者算出来的结果大于等于第三个算出来的结果，按需求选择使用咯。前两者的速度问题，留以后填补**    
select count(*) from `all_deliveries_amazon_copy1`;  # 24737
select count(1) from `all_deliveries_amazon_copy1`;  # 24737
select count(`purchase-date`) from `all_deliveries_amazon_copy1`;   # 24593

# 聚集函数 sum() 忽略 null 值
select sum(`quantity`) from `all_orders_amazon`;

# 聚集函数 max() 忽略 null 值
select max(`price`) from `all_orders_amazon`;

# 聚集函数 min() 忽略 null 值
select min(`price`) from `all_orders_amazon`;

# 聚集函数 avg() 忽略 null 值
select avg(`price`) from `all_orders_amazon`;

# 清空表数据：
（1）Truncate Table `sku_pure`;  
把表的数据清除，保留表结构，如果你用了Innodb引擎，并且有自增列，该自增列从1开始咯（不会在原来基础上继续叠加下去）  
（2）Delete From `sku_pure` Where `sku_id`= '2';  
也是清除表数据，可以用where来限定条件，但是如果用了Innodb引擎，并且有自增列，该自增列将在原有基础上继续叠加下去，不管你删了谁，自增列曾经出现过谁，就不会二次出现这个自增号

# 删除一整张表：  
Drop table `sku_pure`;

# 通配符：  
"%" 代表任何字符出现任意次（0次到正无穷）【注意：不匹配null值】；"\_" 代表任意字符出现 1 次（只可以1次，不多不少）  
select * from `all_orders_amazon` where `店铺` like 'US%';  # 店铺自变量里，以US字符开头的店铺的样本都会被输出  
select * from `all_orders_amazon` where `店铺` like 'US\_';  # 店铺自变量里，以US字符开头，而且只有三个字符才会被输出  

# 去重：distinct
select distinct `店铺` from `all_orders_amazon` where `店铺` like 'US_';  # 查看符合上述条件的店铺

# 把另一张表的数据copy到A表：   
(1)insert into table_A select …… from another_table(需要创建table_A,然后才可以把另一张表的数据放进去，稍微有点麻烦）    
(2)select…… into table_A from another_table(不需要创建A表，你可以直接创建一张新表，然后把另一张的数据直接放到新表里，简直不要太爽！But，在mysql里用不了呀。然后百度到第3个    
(3）create table table_A (select * from another_table)  
insert into `new_payment`
select * from `old_payment`;


# 删除特定的行数据：
delete from `payment` where `店铺`='UK11';

# case when then else end
a.简单函数：
case 列名
　　　　when   条件值1   then  选择项1
　　　　when   条件值2    then  选项2.......
　　　　else     默认值
    end
举个栗子：
select
case `item status`  
　　　　when 'unshipped' then '1'  
　　　　when 'shipped' then '2'  
　　　　when 'canceled' then '3'  
　　　　else 'missing_value'  
end  
from `all_orders`;  
b.搜索函数
case  
　　　　when  列名= 条件值1   then  选择项1
　　　　when  列名=条件值2    then  选项2.......
　　　　else    默认值 
end
举个栗子：
update `all_orders`  
set `customer_type`=  
case   
　　　　when `price`>30 then '1'  
　　　　when `price`<10 then '2'  
　　　　else '3'  
end  

# order by 自定义顺序
一般order by 用默认的asc（升序），或者用desc(降序），但是在应用中，有需要自定义顺序的case,
select * from table_name order by field(column_name,'T','A','Y','L','O','R') 指定列以 T A Y L O R的顺序排列
栗子：
select * 
from sku_pure 
order by field(`店铺`,'US1','US15','US14','UK11','US11'); 指定店铺的排序

# 查看数据表列数：
SELECT count(*)
FROM information_schema. COLUMNS
WHERE table_schema = '数据库名字'
AND table_name = '数据表名字';

栗子：
SELECT count(*)
FROM information_schema. COLUMNS
WHERE table_schema = 'database_1'
AND table_name = 'database_1_table_1';

# 把A表(旧表)数据select出来，然后放进B表(新表)：
create table select from 和 insert into table select from都是用来复制表，两者的主要区别为：

create table table_B as select * from table_A; 要求目标表不存在，因为在插入时会自动创建。
insert into table_B select * from table_A; 要求目标表存在，相当于复制插入。


# 之前看书的时候过了一下列别名，但是没有仔细去看，刷题的时候偶尔会遇到相关题目,于是小记一下：
Sql执行顺序：
(1)    FROM <left_table>
(2)    ON <join_condition>
(3)    <join_type> JOIN <right_table>
(4)    WHERE <where_condition>       # where 过滤的是行记录； where 后面不加聚合函数
(5)    GROUP BY <group_by_list>
(6)    HAVING <having_condition>     # having 过滤的是组，必须有group by才有having
(7)    SELECT
(8)    DISTINCT <select_list>
(9)    ORDER BY <order_by_condition>
(10)   LIMIT <limit_number>

在第7步，select的时候才出现别名，所以前面是根本用不了别名的。但是MySQL特殊一点，在group by后就可以用了，记住即可。
```
