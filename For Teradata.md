1.搜寻表，模糊匹配搜索（如果用dbc.table，可能表名会显示不全，所以用tablesV）  
`select *
from dbc.tablesV
where databaseName like '%DB01%'
AND TableName like '%table01%';`

2.现有一视图 view_02，想要知道它最底层用到的表  
table_01 <-- view_01 <--view_02
`show select * from DB01.view_02;`  
会将这个view怎么建立起来的，全部show出来，免去了一步一步摸索的过程。  

3.
