# 一.单点登录流程

![image-20200322151908758](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200322151908758.png)



## 1.第一次单点登录的关键三处



![image-20200322152348149](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200322152348149.png)

## 2.第二次没有登录的其它客户端登录



![image-20200322154535234](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200322154535234.png)



## 3.核心

![image-20200322154926649](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200322154926649.png)



## 4.理解文章

https://zhuanlan.zhihu.com/p/35738376





# 二.单点登录业务介绍

![image-20200327001131617](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200327001131617.png)



## 1.单点登录流程描述



![image-20200327003237258](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200327003237258.png)





![image-20200327003952895](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200327003952895.png)



~~~java
1.当用户访问的业务模块,需要登录的时候,先去判断cookies中是否有token

2.如果cookie 中有token,无token
    2.1 无token: 认为,没有登录: 则跳转到 登录,或者扫码页面！
    2.2 输入用户名密码与后台数据库进行匹配！
        2.2.1 匹配正确生成token,并放入cookie中,携带token,继续访问其它业务模块
    2.3 如果有token,则继续访问业务！     
        
        
        
        
~~~





## 2.JWT描述

![image-20200327130149393](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200327130149393.png)



![image-20200327130223784](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200327130223784.png)





## 3.设置cookie跨域

![image-20200327180925900](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200327180925900.png)

