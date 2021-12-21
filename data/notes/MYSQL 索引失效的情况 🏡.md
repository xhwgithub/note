---
attachments: [Clipboard_2021-12-20-11-42-22.png, Clipboard_2021-12-20-11-55-59.png, Clipboard_2021-12-20-11-56-21.png, Clipboard_2021-12-20-11-57-34.png, Clipboard_2021-12-20-11-57-55.png, Clipboard_2021-12-20-11-58-29.png, Clipboard_2021-12-20-11-59-02.png, Clipboard_2021-12-20-13-01-37.png, Clipboard_2021-12-20-13-01-41.png, Clipboard_2021-12-20-13-01-59.png, Clipboard_2021-12-20-13-02-16.png, Clipboard_2021-12-20-13-02-30.png, Clipboard_2021-12-20-13-02-43.png, Clipboard_2021-12-20-13-26-54.png, Clipboard_2021-12-20-13-27-07.png, Clipboard_2021-12-20-13-27-18.png, Clipboard_2021-12-20-13-27-30.png, Clipboard_2021-12-20-13-27-42.png, Clipboard_2021-12-20-13-27-53.png, Clipboard_2021-12-20-13-28-05.png, Clipboard_2021-12-20-13-28-20.png]
tags: [数据库]
title: "MYSQL 索引失效的情况 \U0001F3E1"
created: '2021-12-20T03:42:05.731Z'
modified: '2021-12-21T06:08:13.628Z'
---

# MYSQL 索引失效的情况 :house_with_garden:
全值匹配（索引最佳）
  `explain select * from user where name = 'zhangsan' and age = 20 and pos = 'cxy' and phone = '18730658760';`
  ![](@attachment/Clipboard_2021-12-20-11-55-59.png)

和索引顺序无关，MySQL底层的优化器会进行优化，调整索引的顺序
  `explain select * from user where name = 'zhangsan' and age = 20 and pos = 'cxy' and phone = '18730658760';`
  ![](@attachment/Clipboard_2021-12-20-11-56-21.png)

* 1、违反最左前缀法则
如果索引有多列，要遵守最左前缀法则
即查询从索引的最左前列开始并且不跳过索引中的列
  `explain select * from user where age = 20 and phone = '18730658760' and pos = 'cxy';`
  ![](@attachment/Clipboard_2021-12-20-11-57-34.png)

* 2、在索引列上做任何操作
如计算、函数、（自动or手动）类型转换等操作，会导致索引失效从而全表扫描
` explain select * from user where left(name,5) = 'zhangsan' and age = 20 and phone = '18730658760';`
![](@attachment/Clipboard_2021-12-20-11-57-55.png)

* 3、索引范围条件右边的列
索引范围条件右边的索引列会失效
` explain select * from user where name = 'zhangsan' and age > 20 and pos = 'cxy';`
![](@attachment/Clipboard_2021-12-20-11-58-29.png)

* 4、尽量使用覆盖索引
只访问索引查询（索引列和查询列一致），减少select*
` explain select name,age,pos,phone from user where age = 20;` 
![](@attachment/Clipboard_2021-12-20-11-59-02.png)

* 5、使用不等于（!=、<>）
 mysql在使用不等于（!=、<>）的时候无法使用索引会导致全表扫描（除覆盖索引外）
  `explain select * from user where age != 20;`
  ![](@attachment/Clipboard_2021-12-20-13-01-37.png)
  `explain select * from user where age <> 20;`
  ![](@attachment/Clipboard_2021-12-20-13-01-41.png)

* 6、like 以通配符开头（'% abc'）
1. 索引失效
` explain select * from user where name like '%zhangsan';`
  ![](@attachment/Clipboard_2021-12-20-13-01-59.png)
2. 索引生效
  `explain select * from user where name like 'zhangsan%';`
  ![](@attachment/Clipboard_2021-12-20-13-02-16.png)

* 7、字符串不加单引号索引失效
  `explain select * from user where name = 2000;`
  ![](@attachment/Clipboard_2021-12-20-13-02-30.png)

* 8、or 连接
少用or
  `explain select * from user where name = '2000' or age = 20 or pos ='cxy';`
  ![](@attachment/Clipboard_2021-12-20-13-02-43.png)

* 9、order by
1. 正常（索引参与了排序）
  `explain select * from user where name = 'zhangsan' and age = 20 order by age,pos;` 备注：索引有两个作用：排序和查找
  ![](@attachment/Clipboard_2021-12-20-13-26-54.png)

2. 导致额外的文件排序（会降低性能）
  `explain select name,age from user where name = 'zhangsan' order by pos;//违反最左前缀法则`
  ![](@attachment/Clipboard_2021-12-20-13-27-07.png)
  `explain select name,age from user where name = 'zhangsan' order by pos,age;//违反最左前缀法则`
  ![](@attachment/Clipboard_2021-12-20-13-27-18.png)
  `explain select * from user where name = 'zhangsan' and age = 20 order by created_time,age;//含非索引字段`
  ![](@attachment/Clipboard_2021-12-20-13-27-30.png)

* 10、group by
1. 正常（索引参与了排序）
`explain select name,age from user where name = 'zhangsan' group by age;` 备注：分组之前必排序（排序同order by）
![](@attachment/Clipboard_2021-12-20-13-27-42.png)

2. 导致产生临时表（会降低性能）
  `explain select name,pos from user where name = 'zhangsan' group by pos;//违反最左前缀法则`
  ![](@attachment/Clipboard_2021-12-20-13-27-53.png)
  `explain select name,age from user where name = 'zhangsan' group by pos,age;//违反最左前缀法则`
  ![](@attachment/Clipboard_2021-12-20-13-28-05.png)
  `explain select name,age from user where name = 'zhangsan' group by age,created_time;//含非索引字段`
  ![](@attachment/Clipboard_2021-12-20-13-28-20.png)


![](@attachment/Clipboard_2021-12-20-11-42-22.png)

