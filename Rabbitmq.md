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

![image-20200319203404997](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319203404997.png)



#### 2.Direct(处理路由键)

![image-20200319203715278](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319203715278.png)



![image-20200319203838069](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319203838069.png)



#### 3.Topic exchange

![image-20200319204543395](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319204543395.png)

### 5.routing 路由选择  通配符模式



### 6.Topics 主题

### 7.手动和自动确认

![image-20200319200053833](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319200053833.png)

### 8.消息应答与持久化

![image-20200319200055133](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319200055133.png)





![image-20200319200706191](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200319200706191.png)

### 9.rabbitmq的延迟队列

## 二.Spring AMQP Spring-Rabbit



## 三.场景demo  MQ实现搜索引擎DIH增量



## 四.场景demo 未支付订单30分钟 取消



## 五.大数据应用 类似百度统计 cnzz架构消息队列