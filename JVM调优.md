

# JVM 调优相关命令



#### 看见本领命令

1.

~~~
1.	查看正在运行的java线程
Jps -l
~~~



2.

~~~
2.	查看正在运行的java线程的 一些jvm参数
Jinfo -flag PrintGCDetail  线程ID
~~~



3.

~~~
3.	查看初始化jvm的一些详细参数(jvm出场默认数字)
Java -XX:+PrintFlagsInitial
~~~





4. 主要查看修改更新的值

![image-20200305144755185](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305144755185.png)



5.查看默认使用那个垃圾回收器

~~~
Java -XX:+PrintCommandLineFlags -version
~~~



![image-20200305144831412](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305144831412.png)





### Jvm常用基本配置参数

1.

~~~
-Xms 
~~~

![image-20200305144932293](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305144932293.png)





2.

~~~
-Mmx
~~~

![image-20200305145045363](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145045363.png)



3.

~~~
-Xss
~~~

![image-20200305145124622](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145124622.png)



4.

~~~
-Xmn
~~~

![image-20200305145201995](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145201995.png)

![image-20200305145239079](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145239079.png)



5.

~~~
-XX:+PrintGCDetails
~~~



![image-20200305145255787](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145255787.png)





![image-20200305145318138](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145318138.png)



6.

~~~
-XX:SurvivorRation
~~~

![image-20200305145455043](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145455043.png)



7.

~~~
-XX:NewRatio
~~~

![image-20200305145535842](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145535842.png)



8.

~~~
-XX:MaxTenuringThreshold
~~~

![image-20200305145607122](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305145607122.png)

![image-20200305150405797](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305150405797.png)





### Java堆



![image-20200305150431585](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305150431585.png)





### OOM

![image-20200305150454516](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305150454516.png)





### 垃圾收集器



![image-20200305150519704](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305150519704.png)



![image-20200305150536165](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305150536165.png)



![image-20200305150548552](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305150548552.png)



![image-20200305150615791](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305150615791.png)



![image-20200305150625598](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305150625598.png)



### 四大垃圾收集算法

~~~
引用计数 ->
复制拷贝->
标记清除->
标记整理 ->
~~~

