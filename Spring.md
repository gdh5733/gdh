### Bean的生命周期



~~~Java
一 .Spring IOC容器可以管理bean的生命周期,Spring允许在bean生命周期内特定的时间点执行指定的任务。

二 .Spring IOC容器对bean的生命周期进行管理的过程:
1) 通过构造器或工厂方法创建bean实例
2) 为bean的属性设置值和对其他bean引用
3) 调用bean的初始化方法
5) bean 可以使用了
6) 当容器关闭时,调用bean的销毁方法
    
三 . 在配置bean时,通过init-method和destory-method 属性为bean指定初始化和销毁方法
    
四 . bean的后置处理器
 1）bean的后置处理器允许在调用初始化方法前后对bean进行额外的处理
 2）bean后置处理对IOC容器里的所有bean实例逐一处理,而非单一实例
    其典型的应用是:检查bean属性的正确性或根据特定的标准更改bean的属性
 3）bean后置处理器需要实现接口:
   org.springframework.beans.factory.config.BeanPostProcessor 在初始化方法被调用前后,Spring将把每个bean实例分别传递给上述接口的以下两个方法:

  - postProcessBeforeInitialization(Object String)
  - postProcessAfterInitialization(Object String)    
       

    
    
~~~



### Spring事务

![image-20200309111828660](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200309111828660.png)



![image-20200313114544651](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200313114544651.png)

