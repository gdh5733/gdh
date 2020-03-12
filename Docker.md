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





#### DockerFile 

~~~dockerfile
FROM   - 基础镜像,当前新镜像是基于那个镜像的

MAINTAINER - 镜像维护者的姓名和邮箱地址

RUN  - 容器构建时需要运行的命令

EXPOSE - 当前容器对外暴露出的端口

WORKDIR - 指定在创建容器后,终端默认登录的进来工作目录,一个落脚点

ENV - 用来构建镜像的过程中设置环境变量

ADD - 将宿主机目录下的文件拷贝进镜像且ADD命令自动处理URL和解压tar压缩包

COPY - 类似ADD,拷贝文件和目录到镜像中。将从构建上下文目录中<源路径>的文件/目录复制到新的一层的镜像内的<目标路径>位置

VOLUME - 容器数据卷,用于数据保存和持久化工作

CMD - 指定一个容器启动的时候要执行的命令,Dockerfile中可以有多个CMD指令,但只有最后一个生效,CMD，会被docker run 之后的参数替换

ENTRYPOINT - 指定一个容器启动时要运行的命令,ENTRYPOINT的目的和CMD一样,都是在指定容器启动程序及参数

ONBUILD - 当构建一个被继承的Dockerfile运行命令,父镜像在被子继承后父镜像的onbuild被触发
      

~~~



#### 自定义镜像

##### 1.编写

~~~dockerfile
在linux上创建Dockerfile.txt

=========================
FROM centos
MAINTAINER gaodehan<gaodh5733@gmail.com>

ENV MYPATH /user/local
WORKDIR $MYPATH

RUN yum -y install vim
Run yum -y install net-tools

Expose 80

CMD echo $MYPATH

CMD echo "success------------ok"
CMD echo "success------------ok"
CMD /bin/bash

~~~



##### 2.构建

~~~docker
如果是在dockerfile是在 /mydocker/Dockerfile.txt

docker build -f /mydocker/Dockerfile -t myimage:1.3.

标准语法:
docker build -t 新镜像的名字:TAG.
~~~



##### Dockerfile模板

![image-20200311183929310](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200311183929310.png)



##### Dockerfile实战

![image-20200311185150902](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200311185150902.png)









