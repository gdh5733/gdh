### 一 .查找特定文件
```
面试常用的方式

find ~ -name "target3.java" :精确查找文件

find ~ name "target*" :模糊查找文件

find ~ -name "target" :不区分文件大小写去查找文件

man find: 更多关于find指令的使用说明
```



### 二 .时间日期类

~~~
Man date
cal
~~~



### 三.文件目录类

~~~

~~~



### 四.网络配置类





### 五.磁盘分区类

~~~
Df -h 列出文件系统的整体磁盘使用量，检查文件系统的磁盘空间占用情况
~~~



### 六. 搜索分区类



### 七. 搜索查找类

~~~
find
grep
~~~



### 八. 进程线程类

~~~
Ps  
Ps -ef   查看进程
ps-aux  查看进程

netstat -anp  显示系统目前网络情况,例如目前的连接,数据包传递数据,或是路由表的内容
   an ,按一定的顺序排列输出
   p,表示显示那个进程在调用

~~~



### 九. 压缩和解压类

~~~linux
Gzip 只能用于压缩文件

解释: 打包目录,压缩后的文件格式.tar.gz
参数:
-c 产生.tar打包文件
-v 显示详细信息
-f 指定压缩后的文件名
-z 打包同时压缩
-x 解包 .tar 文件



命令: tar上述参数+XXX.tar.gz+将要打包进去的内容(常用)
压缩: tar -zcvf XXX.tar.gz  n1.txt n2.txt
解压: tar -zxvf XXX.tar.gz




解释: 压缩文件和目录的命令,window/linux通用且可以压缩

参数: -r 压缩目录

命令: zip+参数+XXX.zip+将要压缩的内容
    
压缩: zip mypackage.zip 1.txt 2.txt
解压: unzip mypackage.zip

~~~



### 十. 性能优化类 结合JVM(重点)

~~~
如果linux系统慢了怎么办?
主要是CPU 或者是 内存的问题,硬盘问题

1.系统整机性能(Top)
解决:查看整体机器性能 使用top 命令来查看 
1.1	Cpu  
1.2	mem 内存
1.3	id =idle (cpu)空闲率  越大越好
1.4	load avage 系统平均负载（有三个参数<一分钟 五分钟 十五分钟>系统的指标  这个三个数相加除以三乘以百分之百 高于60%  说明cpu负载过重）


2.内存
Free -m 查看内存

3.硬盘
Df -h  查看剩余磁盘空间

4. CPU  
vmstat -n 2 3   主要看memory 和cpu 两个参数

5.磁盘IO
Iostat -xdk 2 3   主要看util参数  较高的话 需要具体看sql了


~~~

