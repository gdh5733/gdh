# Stream

## 官网地址

https://nacos.io/zh-cn/docs/quick-start-spring-boot.html

### 1.什么是SpringCloudStream?

![image-20200317142435867](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317142435867.png)



### 2.SpringCloudStream的作用

![image-20200317141956951](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317141956951.png)



### 3.编码API和常用注解

![image-20200317144151163](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317144151163.png)



### 4.SpringCloudStream标准流程套路

![image-20200317151847844](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317151847844.png)



### 5.yml配置



![image-20200317151200395](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317151200395.png)



### 6.生产者代码

![image-20200317152156137](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317152156137.png)



![image-20200317152238034](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317152238034.png)



### 7.消费者代码



![image-20200317152343891](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317152343891.png)



### 8.分组消费与持久化

#### 1.生产案例

![image-20200317153535856](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317153535856.png)



#### 2.产生的问题

##### 1）有重复消费的问题

![image-20200317153846188](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317153846188.png)

![image-20200317153915945](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317153915945.png)



##### 2）消息持久化问题

使用group及默认持久化



## Sleuth链路

下载spring-cloud-starter-zipkin jar包 并启动

   ![image-20200317161151288](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317161151288.png)





# SpringCloud alibaba

### 1.能干吗?

![image-20200317162851725](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317162851725.png)



### 2.怎么玩?

![image-20200317163131146](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317163131146.png)



### 3.注册中心对比

![image-20200317185458832](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317185458832.png)





![image-20200317185642102](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317185642102.png)



### 4.Config(配置中心)

![image-20200317194127429](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200317194127429.png)



### 5.命名空间分组和DataID三者关系

![image-20200318100113754](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318100113754.png)





![image-20200318100644737](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318100644737.png)

### 6.sentinel

#### 1.能干吗?

![image-20200318132818190](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318132818190.png)





#### 2.组成

![image-20200318135259839](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318135259839.png)





#### 3.流控规则

##### 1.基本介绍

![image-20200318143911212](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318143911212.png)

![image-20200318144140605](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318144140605.png)





##### 2.流控配置

![image-20200318144740992](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318144740992.png)



##### 3.流控关联

![image-20200318152044750](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318152044750.png)





##### 4.流控预热

![image-20200318154225866](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318154225866.png)



##### 5.排队等待



![image-20200318154734561](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318154734561.png)



![image-20200318154800159](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318154800159.png)





#### 4.降级规则

##### 1.基本介绍

![image-20200318160234762](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318160234762.png)



![image-20200318160502914](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318160502914.png)



##### 2.RT

###### 1.简单介绍

![image-20200318161003449](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318161003449.png)

###### 2.结论

![image-20200318161637920](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318161637920.png)



![image-20200318161610832](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318161610832.png)



##### 3.异常比例

###### 1.简单介绍

![image-20200318163824075](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318163824075.png)



###### 2.结论

![image-20200318163540419](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318163540419.png)



##### 4.异常数

###### 1.是什么?

![image-20200318164753765](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318164753765.png)





![image-20200318164830472](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318164830472.png)

#### 5.热点规则

##### 1.热点参数规则

![image-20200318171038868](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318171038868.png)



![image-20200318171148765](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318171148765.png)



##### 2.热点参数例外

![image-20200318180555655](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318180555655.png)



##### 3.小总结

![image-20200318181752330](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318181752330.png)



##### 4.sentinal

![image-20200318193819038](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318193819038.png)



![image-20200318193923527](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200318193923527.png)



#### 6.SentinelResource配置

##### 1.按资源名称限流+后续处理(控制台还需配置)

![image-20200319113907600](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319113907600.png)



##### 2.按照url地址限流+后续处理（控制台还需配置）

![image-20200319113929932](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319113929932.png)



##### 3.上面兜底方案面临的问题

![image-20200319114015428](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319114015428.png)



##### 4.客户自定义限流处理逻辑（控制台还需要配置）

![image-20200319114036293](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319114036293.png)





![image-20200319114058772](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319114058772.png)

##### 5.更多注解属性说明

###### 1.Fallback 与 blockHandle



~~~java
package com.atguigu.springcloud.alibaba.controller;
import com.alibaba.csp.sentinel.annotation.SentinelResource;
import com.alibaba.csp.sentinel.slots.block.BlockException;
import com.atguigu.springcloud.alibaba.service.PaymentService;
import com.atguigu.springcloud.entities.CommonResult;
import com.atguigu.springcloud.entities.Payment;
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

import javax.annotation.Resource;

/**
 * @auther zzyy
 * @create 2020-02-25 16:05
 */
@RestController
@Slf4j
public class CircleBreakerController
{
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
    //@SentinelResource(value = "fallback") //没有配置
    //@SentinelResource(value = "fallback",fallback = "handlerFallback") //fallback只负责业务异常
    //@SentinelResource(value = "fallback",blockHandler = "blockHandler") //blockHandler只负责sentinel控制台配置违规
    @SentinelResource(value = "fallback",fallback = "handlerFallback",blockHandler = "blockHandler",
            exceptionsToIgnore = {IllegalArgumentException.class})
    public CommonResult<Payment> fallback(@PathVariable Long id)
    {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/"+id,CommonResult.class,id);

        if (id == 4) {
            throw new IllegalArgumentException ("IllegalArgumentException,非法参数异常....");
        }else if (result.getData() == null) {
            throw new NullPointerException ("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }
    //本例是fallback
    public CommonResult handlerFallback(@PathVariable  Long id,Throwable e) {
        Payment payment = new Payment(id,"null");
        return new CommonResult<>(444,"兜底异常handlerFallback,exception内容  "+e.getMessage(),payment);
    }
    //本例是blockHandler
    public CommonResult blockHandler(@PathVariable  Long id,BlockException blockException) {
        Payment payment = new Payment(id,"null");
        return new CommonResult<>(445,"blockHandler-sentinel限流,无此流水: blockException  "+blockException.getMessage(),payment);
    }

    //==================OpenFeign
    @Resource
    private PaymentService paymentService;

    @GetMapping(value = "/consumer/paymentSQL/{id}")
    public CommonResult<Payment> paymentSQL(@PathVariable("id") Long id)
    {
        return paymentService.paymentSQL(id);
    }
}

~~~



#### 7.服务熔断功能



#### 8.规则持久化

##### 1.是什么?

~~~java
一旦我们重启应用,sentinel规则将消失,生产环境需要将配置规则进行持久化
~~~



##### 2.怎么玩?

~~~java
将限流配置规则持久化进Nacos保存,只要刷新8401某个rest地址,sentinel控制台
的流控规则就能看到,只要Nacos里面的配置不删除,针对8401上sentinel上的流控规则
持续有效
~~~





#### 9.分布式事务（Seata）



##### 术语介绍

###### 1.Transaction ID XID 

~~~
全局唯一的事务ID
~~~





###### 2.3个组件的概念

###### 1.Transaction Coordiator(TC)  

~~~
事务协调器,维护全局事务的运行状态,负责协调并驱动全局事务的提交或回滚
~~~



###### 2.Transaction Manager(TM)

~~~
控制全局事务的边界,负责开启一个全局事务,并最终发去全局提交或全局回滚的决议
~~~



###### 3.Resource Manager(RM)

~~~
控制分支事务,负责分支注册,状态汇报,并接收事务协调器的指令,驱动分支(本地)
事务的提交和回滚
~~~



##### 处理过程

![image-20200319140105487](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319140105487.png)