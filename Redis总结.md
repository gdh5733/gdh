## Redis 

### Redis的五大数据类型



![image-20200304121825226](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304121825226.png)





### 常见数据类型操作命令

1.key

![image-20200304123808800](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304123808800.png)





2.String![image-20200304124725275](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304124725275.png)



![image-20200304125726005](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304125726005.png)



3.List

![image-20200304143729369](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304143729369.png)

   参考连接 https://www.cnblogs.com/xinhuaxuan/p/9252111.html

4.Set

![image-20200304145321203](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304145321203.png)

参考链接 https://www.cnblogs.com/xinhuaxuan/p/9256738.html



5.Hash

![image-20200304153017220](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304153017220.png)



![image-20200304153309524](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304153309524.png)

参考链接  https://www.cnblogs.com/xinhuaxuan/p/9256763.html



6.ZSet

![image-20200304154056149](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304154056149.png)



参考链接 https://www.cnblogs.com/xinhuaxuan/p/9296525.html







### redis缓存清除策略（redis.conf）

![image-20200304161652227](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304161652227.png)





### redis.conf常用配置介绍

![image-20200304162049422](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162049422.png)

![image-20200304162242814](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162242814.png)





![image-20200304162153102](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162153102.png)

![image-20200304162704211](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162704211.png)



![image-20200304162847477](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304162847477.png)





### Redis的持久化

RDB

![image-20200304164049476](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304164049476.png)



AOF

![image-20200304183237348](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304183237348.png)



### 小总结



![image-20200304195147351](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304195147351.png)

### 性能建议

![image-20200304195237178](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304195237178.png)





### Redis的事务

~~~
可以一次执行多个命令,本质是一组命令的集合,一个事务中的所有命令都会序列化,按顺序的
串行化执行而不被其它命令插入,不许加塞
~~~





![image-20200304223048788](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200304223048788.png)



事务小总结: 

![image-20200305130317975](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305130317975.png)







[Redis总结文档](https://mp.weixin.qq.com/s?__biz=MzAxNjk4ODE4OQ==&mid=2247487588&idx=3&sn=92ce1df4e9d62d257d45a7eee8f0c7d3&chksm=9bed3116ac9ab80086276faf208074bdd38f6aa8d6b4b93d7aa67c7688f4086de3416bbdb758&scene=0&xtrack=1&key=8be65ffce19453078887e71002be67c2abfc71c5fbf3566726df6168d0b2764022ec2baf7fd4cea59684a273f7a6464e7251db27d2a7c99c3e73ebea1be70a7ca16cc8a4f96992fe2cf2d898a137e58e&ascene=1&uin=MjQ1MzYyMTQxMw%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&exportkey=A0MuMYx8mplEdEg%2Bi3FY5Oc%3D&pass_ticket=OEZ1aKxM4vH0f%2FcoizUcJlDT%2BY5Qp3Y7a7ZM29%2FtKlrVKPq6v%2F3gjMCEYkXa9pA0)

[Redis使用场景](https://www.cnblogs.com/benjieqiang/p/11475651.html)

