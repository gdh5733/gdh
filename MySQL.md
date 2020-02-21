# Mysql数据库

## 索引优化

```
1.最佳左前缀法则
2.不在索引列上做任何操作(计算，函数（自动or手动)类型转换，会导致索引失效而转向全表扫描
3.存储引擎不能使用索引中范围条件右边的列
4.尽量使用覆盖索引(只访问索引的查询（索引列和查询列一致）)，减少select *
5.mysql在使用不等于的时候（！=或者<>的时候无法使用索引会导致全表扫描）
6.is null ,is not null 也无法使用索引

7.like 以通配符开头('%abc...') mysql索引失效会变成全表扫描的操作

8.字符串不加单引号索引失效

9.少用or，用它来连接的时候会索引失效
```

## 索引优化列子

假设index(a,b,c)

Where 语句 | 索引是否被使用
---|---
where a= 3 | Y ,使用到a
where a= 3 and b = 5| Y,使用到a,b
where a= 3 and b = 5 and c= 4 | Y,使用到a,b,c
where b= 3 或者 where b =3 and c=4 或者 where c= 4| N
where a= 3 and c =5| 使用到a,但是c不可以，b中间断了
where a= 3 and b>4 and c= 5 | 使用到a和b，c不能用在范围后,b断了
where a= 3 and b like 'kk%' and c= 4|Y，使用到a,b,c
where a= 3 and b like '%kk' and c= 4 |Y,只用到a
where a= 3 and b like '%kk%' and c= 4 | Y,只用到a
where a= 3 and b like 'k%kk%' and c= 4 | Y,使用到a,b,c 

## [优化总结口诀]


```
全值匹配我最爱,最左前缀要遵守

带头大哥不能死,中间兄弟不能断

索引列上少计算,范围之后全失效

LIKE百分写最后,覆盖索引不写星

不等空值还有or,索引失效要少用
```

## 查询优化的步骤

```
1.观察，至少跑一天，看看生产的慢SQL情况

2.开启慢查询日志，设置阀值，比如超过5秒中的就是慢SQL,并将它抓取出来

3.explain + 慢SQL分析

4.show profile

5.运维经理 or DBA，进行SQL数据库服务起的参数调优


总结:
1. 慢查询的开启并捕获
2. explain + 慢SQL分析
3. show  profile 查询SQL在MYsql 服务器里面的执行细节和生命周期情况
4. SQL数据库服务器的参数调优
```

## 小表驱动大表

```
优化原则: 小表驱动大表,即小的数据集驱动大的数据集

#######################原理(RBO)############################
select * from A where id in (select id from B)
等价于:
for select * from B
for select * from A where A.id = B.id

当B表的数据集必须小于A表的数据集时,用in优于exists。

select * from A where exits (select 1 from B where B.id = A.id)
等价于
for select * from A
for select * from B where  B.id = A.id

当A表的数据集系小于B表的数据集时,用exists优于in。
注意: A表与B表的ID字段应建立索引。

exists
select... FROM table where exists (subquery)

该语法可以理解为: 将主查询的数据,放到子查询中做条件验证,根据验证结果（true 或 false）来决定主查询的数据结果是否得以保留。


提示:

1.exists(subquery) 只返回TRUE或FALSE，因此子查询中的select * 也可以是select 1 或其它,官方说法是实际执行时会忽略select清单,因此没有区别
2.exists子查询的实际执行过程可能经过了优化而不是我们理解上的逐条对比,如果担忧效率问题,可进行实际检验以确定是否有效率问题.
3.exists 子查询往往也可以用条件表达式,其他子查询或者JOIN来替代,何种最优
需要具体问题具体分析
```

## ORDER BY 优化

```
order by子句,尽量使用Index方式排序,避免使用FileSort方式排序
尽可能在索引列上完成排序操作,遵照索引建立的最佳左前缀
filesort 和 index , index效率高

order by满足两种情况,会使用Index方式完成排序
-> 1.order by 语句使用所以最左前列
   2.使用where子句与order by 子句条件列组合满足索引最左前列


如果不再索引列上,filesort有两种算法: 
mysql就要启动双路排序和单路排序
->

优化策略

```

## GROUP BY

```
1.group by 实质是先排序后进行分组,遵照索引建的最佳左前缀

2.当无法使用索引列,增大max_length_for_sort_data参数的设置+增大sort_buffer_size参数的设置

3.where高于having,能写在where限定的条件就不要去having限定了
```

## 慢查询日志

```
日志分析工具

mysqldumpslow

列如: 得到返回记录集最多的10个SQL
1.mysqldumpslow -s r -t 10/var/lib/mysql/slow.log

批量数据脚本
```

## SHOW PROFILE

```
查看一个SQL 执行的完整生命周期

结论: 当Status列出现以下的时候  需要优化

1.converting HEAP to MyISAM 查询结果太大,内存都不够用了往磁盘上搬了

2.Creating tmp table 创建临时表
-> 拷贝数据到临时表
-> 用完在删除
3.Copying to tmp table on disk 把内存中临时表复制到磁盘,危险!!!

locked


```









