# EleaseSearch

## 一.倒排索引



![image-20200323113946387](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323113946387.png)

## 二.Query DSL

### 1.返回部分字段



![image-20200323130215313](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323130215313.png)



### 2.match【匹配查询】

![image-20200323130244925](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323130244925.png)



### 3.match_phrase【短语精确匹配】



![image-20200323130326830](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323130326830.png)



### 4.multi_match【多字段匹配】

![image-20200323130404476](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323130404476.png)



### 5.bool【复合查询】

![image-20200323130432718](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323130432718.png)



### 6.filter【结果过滤】

![image-20200323132246314](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323132246314.png)



### 7.term【精确值的查询】

![image-20200323134134065](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323134134065.png)



### 8.使用aggs实现聚合

#### 1.案例一

![image-20200323144046554](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323144046554.png)

#### 2.案例二

![image-20200323144906131](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323144906131.png)



#### 3.案例三

![image-20200323151014616](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323151014616.png)





## 三.Mapping

#### 1.字段类型



![image-20200323153304060](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323153304060.png)





#### 2.映射



![image-20200323153352074](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323153352074.png)



##### 一.查看映射

![image-20200323153741353](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323153741353.png)





## 四.集群

### 1.Shards & Replicas（分片 & 副本）



![image-20200323180444317](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323180444317.png)

### 2.添加故障转移

![image-20200323182805318](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323182805318.png)





![image-20200323182901265](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323182901265.png)

![image-20200323182109149](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323182109149.png)



### 3.水平扩容



![image-20200323202336264](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323202336264.png)



![image-20200323202458923](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323202458923.png)

### 4.脑裂问题



![image-20200323202942400](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323202942400.png)



### 5.解决脑裂问题

![image-20200323203435026](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200323203435026.png)