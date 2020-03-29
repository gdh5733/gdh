## Redis 

### 一.Redis的五大数据类型



![image-20200304121825226](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304121825226.png)





### 二.常见数据类型操作命令

#### 1.key

![image-20200304123808800](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304123808800.png)





#### 2.String![image-20200304124725275](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304124725275.png)



![image-20200304125726005](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304125726005.png)



#### 3.List

![image-20200304143729369](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304143729369.png)

   参考连接 https://www.cnblogs.com/xinhuaxuan/p/9252111.html

#### 4.Set

![image-20200304145321203](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304145321203.png)

参考链接 https://www.cnblogs.com/xinhuaxuan/p/9256738.html



#### 5.Hash

![image-20200304153017220](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304153017220.png)



![image-20200304153309524](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304153309524.png)

参考链接  https://www.cnblogs.com/xinhuaxuan/p/9256763.html



#### 6.ZSet

![image-20200304154056149](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304154056149.png)



参考链接 https://www.cnblogs.com/xinhuaxuan/p/9296525.html







### 三.redis缓存清除策略（redis.conf）

![image-20200304161652227](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304161652227.png)



### 四.redis.conf常用配置介绍

![image-20200304162049422](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162049422.png)

![image-20200304162242814](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162242814.png)





![image-20200304162153102](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162153102.png)

![image-20200304162704211](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162704211.png)



![image-20200304162847477](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162847477.png)





### 五.Redis的持久化

#### 1.RDB

![image-20200304164049476](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304164049476.png)



#### 2.AOF

![image-20200304183237348](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304183237348.png)



#### 3.小总结



![image-20200304195147351](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304195147351.png)

#### 4.性能建议

![image-20200304195237178](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304195237178.png)





### 六.Redis的事务

~~~
可以一次执行多个命令,本质是一组命令的集合,一个事务中的所有命令都会序列化,按顺序的
串行化执行而不被其它命令插入,不许加塞
~~~





![image-20200304223048788](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304223048788.png)



事务小总结: 

![image-20200305130317975](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305130317975.png)





### 七.购物车（Redis实现）



![image-20200324152706730](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200324152706730.png)





![image-20200324160052359](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200324160052359.png)





#### 1.离线购物车

~~~java
离线购物车
    
只要每次看到购物车,都有一个usre-key=uuid;如果这个user-key丢了,购物车就没了.
如果我们要看购物车肯定会带上这个user-key的cookie;如果有就用自带的,没有就新建一个
以后用这个。
登录以后离线的和在线的合并了,并且清空了离线购物车里面的数据。    
~~~



~~~java
京东怎么做?

    购物车有一个cookie对应的key关联,即使没有登陆也有,登录以后进行购物车合并,
合并完后删除购物车数据;

离线购物车: 永远用cart-key=uuid;购物车数据都在redis中提升系统性能。cart:temp:uuid
    
在线购物车: cart:1={};放在redis中; cart:user:1
1) 购物车数据保存在redis中,使用分布式集合;【redisson.getMap】
2) 用户对于购物车的所有操作,都需要传入cart-key,如果用户登录了,还需要传入token    
~~~



~~~java
购物车需要提供的所有方法:
1) 添加到购物车
2) 修改购物项    
~~~



#### 2.在线购物车

~~~
在线购物车: cart:1={};放在redis中; cart:user:1
~~~



#### 3.代码（查看本地代码）





### 八.缓存问题

#### 1.缓存穿透

![image-20200325121044356](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200325121044356.png)



#### 2.缓存雪崩

![image-20200325122303418](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200325122303418.png)



#### 3.缓存击穿

![image-20200325142032651](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200325142032651.png)



### 九.缓存的使用模式

#### 1.双写一致性问题

~~~java
如何保证缓存和数据库的读写一致性？
    
利用双写+读写锁保证一致性
    
最终一致性:
下单。查看价;要完全看最新的价格,我们加读锁
商品详情页看价格;直接去缓存读取    
~~~



![image-20200326122631122](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326122631122.png)



#### 2.Cache-Aside



![image-20200326122731865](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326122731865.png)

![image-20200326122750847](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326122750847.png)

![image-20200326122820290](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326122820290.png)

![image-20200326122929817](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326122929817.png)



#### 3.Cache-As-SoR

![image-20200326130210825](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326130210825.png)



![image-20200326130237911](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326130237911.png)



#### 4.Copy-Pattern

![image-20200326133634062](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326133634062.png)





[Redis总结文档](https://mp.weixin.qq.com/s?__biz=MzAxNjk4ODE4OQ==&mid=2247487588&idx=3&sn=92ce1df4e9d62d257d45a7eee8f0c7d3&chksm=9bed3116ac9ab80086276faf208074bdd38f6aa8d6b4b93d7aa67c7688f4086de3416bbdb758&scene=0&xtrack=1&key=8be65ffce19453078887e71002be67c2abfc71c5fbf3566726df6168d0b2764022ec2baf7fd4cea59684a273f7a6464e7251db27d2a7c99c3e73ebea1be70a7ca16cc8a4f96992fe2cf2d898a137e58e&ascene=1&uin=MjQ1MzYyMTQxMw%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&exportkey=A0MuMYx8mplEdEg%2Bi3FY5Oc%3D&pass_ticket=OEZ1aKxM4vH0f%2FcoizUcJlDT%2BY5Qp3Y7a7ZM29%2FtKlrVKPq6v%2F3gjMCEYkXa9pA0)

[Redis使用场景](https://www.cnblogs.com/benjieqiang/p/11475651.html)

