1.想要查询某表在什么库（如果用dbc.table，可能表名会显示不全，所以用tablesV）
`select *
from dbc.tablesV
where databaseName like '%DB01%'
AND TableName like '%table01%';`

2.现有一视图 view_01，想要知道它最底层用到的表
show select * from DB01.view_01;

3.

ing~