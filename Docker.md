### Docker重要命令



#### 容器高级命令

1.查看守护式容器

~~~dockerfile
docker run -d 容器名
~~~



2.查看容器日志

~~~dockerfile
docker logs -f -t --tail 容器ID

-t 是加入时间戳
-f 跟随最新的日志打印
--tail 数字 显示最后多少条
~~~



3.查看容器内运行的进程

~~~dockerfile
docker top 容器ID
~~~



4.查看容器内部细节

~~~dockerfile
docker inspect 容器ID
~~~



5.进入正在运行的容器并以命令行交互

~~~dockerfile
docker exec -it 容器ID /bin/bash

docker attach 容器ID

上述两个区别  
         attach
         直接进入容器启动命令的终端,不会启动新的进程
         
         exec
         是在容器中打开新的终端,并且可以启动新的进程
        

~~~



6.从容器内拷贝文件到主机上

~~~
docker cp 容器ID:容器内路径  
~~~



#### 镜像高级命令

~~~dockerfile
docker commit提交容器副本使之成为一个新的镜像

docker commit -m "提交的描述信息" -a="作者" 容器ID 要创建的目标镜像名:[标签名]

~~~

