

# JVM 调优相关命令



### 一.看见本领命令

#### 1.查看正在运行的java线程

~~~
1.	查看正在运行的java线程
Jps -l
~~~



#### 2.查看正在运行的java线程的 一些jvm参数

~~~
2.	查看正在运行的java线程的 一些jvm参数
Jinfo -flag PrintGCDetail  线程ID
~~~



#### 3.查看初始化jvm的一些详细参数

~~~
3.	查看初始化jvm的一些详细参数(jvm出场默认数字)
Java -XX:+PrintFlagsInitial
~~~



#### 4.主要查看修改更新的值

![image-20200305144755185](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305144755185.png)



#### 5.查看默认使用那个垃圾回收器

~~~
Java -XX:+PrintCommandLineFlags -version
~~~



![image-20200305144831412](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200305144831412.png)





### 二.JVM性能调优工具

#### 1.jps

~~~java
查看所有的jvm进程,包括进程ID,进程启动的路径等等
我自己也用PS,即 ps -ef | grep java
~~~

#### 2.jstack

~~~
观察jvm中当前所有线程的运行情况,和线程当前状态。
系统崩溃了,如果java程序崩溃生成core文件,jstack工具可以用来获得core文件的java stack 和 native stack 的信息,从而可以轻松的知道java程序是如何崩溃和在程序何处发生问题。
~~~

#### 3.jstats

~~~java
jstat利用JVM内建的指令对Java应用程序的资源和性能进行实时的命令行监控,包括对进程的classloader,compiler,gc情况;特别的,一个极强的监视内存工具,可以用来监视JVM内存内的各种堆和非堆的大小及其内存使用量,以及加载类的数量。
~~~



#### 4.jmap

~~~java
监视进程运行中的jvm物理内存的占用,该进程内存内,所有对象的情况,例如产生了哪些对象,
对象数量;系统崩溃了? jmap可以从core文件或进程中获得内存的具体匹配情况,包括Heap Size,Perm size等等
~~~



#### 5.jinfo

~~~java
观察进程运行环境参数,包括Java System属性,和JVM命令行参数
系统崩溃了? jinfo可以从core文件里面知道崩溃的Java应用程序的配置信息    
~~~



#### 使用教程

##### 1.jstat

~~~java
-class：统计class loader行为信息 
-compile：统计编译行为信息 
-gc：统计jdk gc时heap信息 
-gccapacity：统计不同的generations（包括新生区，老年区，permanent区）相应的heap容量情况 
-gccause：统计gc的情况，（同-gcutil）和引起gc的事件 
-gcnew：统计gc时，新生代的情况 
-gcnewcapacity：统计gc时，新生代heap容量 
-gcold：统计gc时，老年区的情况 
-gcoldcapacity：统计gc时，老年区heap容量 
-gcpermcapacity：统计gc时，permanent区heap容量 
-gcutil：统计gc时，heap情况
~~~



![image-20200317130251932](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130251932.png)



![image-20200317130359940](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130359940.png)



![image-20200317130442446](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130442446.png)



![image-20200317130519139](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130519139.png)





![image-20200317130639606](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130639606.png)





![image-20200317130724253](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130724253.png)



![image-20200317130800993](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130800993.png)





![image-20200317130829924](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130829924.png)

##### 2.jmap

![image-20200317130856549](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130856549.png)



![image-20200317130936766](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317130936766.png)



##### 3.jinfo

![image-20200317131145042](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317131145042.png)



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

