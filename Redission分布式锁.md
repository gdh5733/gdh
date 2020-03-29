# 1.读写锁(RReadWriteLock)



~~~java
package com.alan.seckill.service.impl;
import org.redisson.api.RLock;
import org.redisson.api.RReadWriteLock;
import org.redisson.api.RedissonClient;
import org.springframework.beans.factory.annotation.Autowired;
import java.util.UUID;

/**
 * @Description 分布式读写锁
 * 描述: 当用户读到了正在修改商品信息的数据
 * 读操作将会等待写操作完成
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/25
 */

public class RedissonLockService {


    @Autowired
    RedissonClient redisson;


    private String hello = "hello";


    /**
     * 读锁(共享锁)
     * 有写锁的情况下,写锁以后读都不可以
     *
     * @return
     */
    private String read() {
        RReadWriteLock helloValue = redisson.getReadWriteLock("helloValue");
        RLock readLock = helloValue.readLock();
        readLock.lock();
        String a = hello;
        readLock.unlock();
        return a;
    }


    /**
     * 写锁(排他锁),也可以叫独占锁
     *
     * @return
     */
    private String write() throws InterruptedException {
        RReadWriteLock helloValue = redisson.getReadWriteLock("helloValue");
        RLock writeLock = helloValue.writeLock();
        writeLock.lock();
        Thread.sleep(5000);
        hello = UUID.randomUUID().toString();
        writeLock.unlock();
        return hello;
    }
}

~~~



# 2.CountDownLatch(门栓)

~~~java
package com.atguigu.gulimall.seckill.service.impl;
import org.redisson.api.RCountDownLatch;
import org.redisson.api.RedissonClient;
import org.springframework.beans.factory.annotation.Autowired;

/**
 * @Description 分布式中的CountDownLatch锁
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/25
 */

public class RedissonCountLatchLockService {

    @Autowired
    RedissonClient redisson;


    //学生往出走
    public Boolean gogogo() {

        //num 为Redis中的
        RCountDownLatch downLatch = redisson.getCountDownLatch("num");

        downLatch.countDown();
        // TODO SOMETHING
        System.out.println("溜了...");
        return true;
    }

    //学生走完了 班长要关门了
    public Boolean suomen() throws InterruptedException {
        RCountDownLatch downLatch = redisson.getCountDownLatch("num");

        //相当于给value 赋值为10 ,也可以在服务器直接赋值
        downLatch.trySetCount(10);

        downLatch.await();
        // TODO SOEMTHING
        System.out.println("我要锁门...");
        return true;
    }
}

~~~









# 3.Sempore（信号量）

~~~java
package com.atguigu.gulimall.seckill.service.impl;

import org.redisson.api.RSemaphore;
import org.redisson.api.RedissonClient;
import org.springframework.beans.factory.annotation.Autowired;

/**
 * @Description 分布式系统Sempore线程同步工具的使用
  秒杀可以使用该锁
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/25
 */

public class RedissonSemporeLockService {

    @Autowired
    RedissonClient redisson;

    //抢占车位
    public Boolean tc() throws InterruptedException {

        //tcc 参数为redis中的key  value设置了3(可以理解为3个车位) 每获取一个车位减少一个
        RSemaphore semaphore = redisson.getSemaphore("tcc");

        semaphore.acquire();

        return true;
    }

    //释放车位
    public Boolean rc() {
        RSemaphore semaphore = redisson.getSemaphore("tcc");
        semaphore.release();
        return true;
    }
}

~~~



