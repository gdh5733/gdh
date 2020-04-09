## Docker



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

~~~shell
如果是在dockerfile是在 /mydocker/Dockerfile.txt

docker build -f /mydocker/Dockerfile -t myimage:1.3.

标准语法:
docker build -t 新镜像的名字:TAG.
~~~



##### Dockerfile模板

![image-20200311183929310](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200311183929310.png)



##### Dockerfile实战

![image-20200311185150902](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200311185150902.png)





## Docker Compose（服务编排）



#### 一.服务编排

![image-20200331121818351](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200331121818351.png)



![image-20200331122008691](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200331122008691.png)

#### 二.使用docker compose编排nginx+springboot项目

##### 1.创建docker-compose目录

~~~shell
mkdir ~/docker-compose
cd ~/docker-compose
~~~



##### 2.编写docker-compose.yml文件

~~~yml
version: '3'
services:
  nginx:
    image: nginx
    ports:
     - 80:80
    links:
     - app
    volumes:
     - ./nginx/conf.d:/etc/nginx/conf.d
  app:
   image: app
   expose:
    - "8080"

~~~



##### 3.创建 ./nginx/conf.d目录

~~~shell
mkdir -p /nginx/conf.d
~~~



##### 4.在./nginx/conf.d目录下编写itheima.conf文件

~~~yml
server {
    listen 80;
    access_log off;
    
    location / {
       proxy_pass http://app:8080;
    }
}
~~~



##### 5.在~/docker-compose目录下使用docker-compose启动容器

~~~shell
docker-compose up
~~~



##### 6.测试访问

~~~shell
http://192.168.149.135/hello
~~~



## Docker私有仓库

### 一.私有仓库搭建

~~~shell
# 1.拉取私有仓库镜像
docker pull registry

#2.启动私有仓库容器
docker run -id --name=registry -p 5000:5000 registry

#3.打开浏览器 输入地址http://私有仓库服务器ip:5000/v2/_catalog,看到{"repositories":[]} 表示私有仓库 搭建成功

#4. 修改daemon.json
vim /etc/docker/daemon.json

#在上述文件中添加一个key,保存退出.此步用于让docker 信任私有仓库地址; 注意将私有仓库服务器ip修改为自己私有仓库服务器真是ip
{"insecure-registries":["私有仓库服务器ip:5000"]}
 
#5 重启docker 服务
systemctl restart docker
docker start registry

~~~



### 二.将镜像上传至私有仓库

~~~shell
# 1.标记镜像为私有仓库的镜像
docker tag centos:7 私有仓库服务器IP:5000/centos:7

# 2.上传标记的镜像
docker push 私有仓库服务器IP:5000/centos:7
~~~



列子：

![image-20200331140755082](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200331140755082.png)

