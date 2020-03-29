## Rabbitmq

## 一.JAVA操作rabbitmq

### 1.simple 简单队列

![image-20200319193624283](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319193624283.png)



#### 1.简单队列的不足

~~~
耦合性较高,生产者--对应消费者(如果我想有多个消费者消费队列中的消息,这时候就不行了),队列名变更,这时候得同时变更
~~~



### 2.work queues  工作队列 公平分发 轮询分发

![image-20200319194137578](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319194137578.png)

#### 1.为什么会出现工作队列?

~~~
Simple 队列 是一一对应的,而且我们实际开发,生产者发送消息是毫不费力得,而消费者一般是要跟业务相结合的,消费者接收到消息之后就需要处理 可能需要花费时间,这时候队列就会挤压了很多消息
~~~



### 3.publish/subscribe 发布订阅

![image-20200319201509761](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319201509761.png)

### 4.Exchange(交换机 转发器)

![image-20200319203120974](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319203120974.png)

#### 1.Fanout(不处理路由键)

![image-20200326153546856](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326153546856.png)



#### 2.Direct(处理路由键)

![image-20200326153653674](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326153653674.png)



![image-20200319203838069](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319203838069.png)



#### 3.Topic exchange

![image-20200326153614277](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200326153614277.png)



### 5.Topics 主题

### 6.手动和自动确认

![image-20200319200053833](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319200053833.png)

### 7.消息应答与持久化

![image-20200319200055133](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319200055133.png)





![image-20200319200706191](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319200706191.png)

## 

### 8.消息确认机制

![image-20200328175000142](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200328175000142.png)





![image-20200328175248790](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200328175248790.png)





![image-20200328174126215](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200328174126215.png)





![image-20200328174624679](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200328174624679.png)



#### 1.代码

~~~java
package com.atguigu.gulimall.ware.listener;
import com.atguigu.common.to.mq.OrderTo;
import com.atguigu.common.to.mq.StockLockedTo;
import com.atguigu.gulimall.ware.service.WareSkuService;
import com.rabbitmq.client.Channel;
import org.springframework.amqp.core.Message;
import org.springframework.amqp.rabbit.annotation.RabbitHandler;
import org.springframework.amqp.rabbit.annotation.RabbitListener;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.io.IOException;

@Service
@RabbitListener(queues = "stock.release.stock.queue")
public class StockReleaseListener {

    @Autowired
    WareSkuService wareSkuService;

    @RabbitHandler
    public void handleStockLockedRelease(StockLockedTo to, Message message, Channel channel) throws IOException {

        System.out.println("收到解锁库存的消息...");
        try{
            //当前消息是否被第二次及以后（重新）派发过来了。
//            Boolean redelivered = message.getMessageProperties().getRedelivered();
            wareSkuService.unlockStock(to);
            //回复成功 只回复本条消息
            channel.basicAck(message.getMessageProperties().getDeliveryTag(),false);
        }catch (Exception e){
            channel.basicReject(message.getMessageProperties().getDeliveryTag(),true);
        }

    }

    @RabbitHandler
    public void handleOrderCloseRelease(OrderTo orderTo, Message message, Channel channel) throws IOException {
        System.out.println("订单关闭准备解锁库存...");
        try{
            wareSkuService.unlockStock(orderTo);
            channel.basicAck(message.getMessageProperties().getDeliveryTag(),false);
        }catch (Exception e){

            //回复消息处理失败,拒绝消息。并且重新入队
            channel.basicReject(message.getMessageProperties().getDeliveryTag(),true);
        }

    }

}
~~~





#### 2.延时队列(可以实现定时关单)

![image-20200328182521474](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200328182521474.png)



#### 3.延时队列实现-1



![image-20200328182849679](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200328182849679.png)



![image-20200328230353025](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200328230353025.png)



#### 4.接口幂等性

~~~java
举个列子解释

当信息确认完成以后下一步要提交订单,我们必须做放重复验证【接口幂等性】
    
接口幂等性设计:
 select:
 insert/delete/update【幂等性设计】
    
~~~





