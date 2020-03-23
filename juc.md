### 一.同步工具

#### 1.CountDownLatch

~~~java
package com.alan.demo.utils.juc.同步工具;

import java.util.concurrent.CountDownLatch;

/**
 * @Description
 * CountDowmLatch demo 练习
 * 比如 六个同学 走完了之后  班长最后关门走人
 * 主要功能
 * 让一些线程阻塞直到另一些线程完成一系列操作后才被唤醒
 * CountDownLatch 主要有两个方法,当一个或多个线程调用await方法时,调用线程会被阻塞
 * 其它线程调用countDown方法会将计数器减1(调用countDown方法的线程不会阻塞)
 * 当计数器的值变为零时,因调用await方法被阻塞的线程会被唤醒
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/10
 */

public class CountDowmLatchDemo {

    private static final int COUNT = 6;


    public static void main(String[] args) throws InterruptedException {
        closeDoor();
    }


    public static void closeDoor() throws InterruptedException {
        CountDownLatch countDownLatch = new CountDownLatch(COUNT);
        for (int i = 0; i < 6; i++) {
            new Thread(() -> {
                System.out.println(Thread.currentThread().getName() + "\t上完自习,离开教室");
                countDownLatch.countDown(); //数量减减  直到减为零  主线程执行
            }, String.valueOf(i)).start();
        }

        countDownLatch.await();
        System.out.println(Thread.currentThread().getName() + "\t班长关门走人!");

    }
}

~~~





#### 2.CyclicBarrier

~~~java
package com.alan.demo.utils.juc.同步工具;

import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

/**
 * @Description
 * CyclicBarrier 的字面意思是可循环使用(Cyclic)的屏障(Barrier)。
 * 它要做的事情是，让一组线程到达一个屏障(也可以叫同步点)时被阻塞，直到最后一个线程到达屏障时，屏障才会开门，
 * 所有被屏障拦截的线程才会继续干活。CyclicBarrier默认的构造方法是CyclicBarrier(int parties)，
 * 其参数表示屏障拦截的线程数量，每个线程调用await方法告诉CyclicBarrier我已经到达了屏障，然后当前线程被阻塞。
 * <p>
 * <p>
 * 人到齐了才能开会
 * 集齐龙珠才能召唤神龙
 * </p>
 * CyclicBarrier的字面意识是可循环(Cyclic) 使用的屏障(Barrier)
 * 它要做的事情是,让一组线程到达一个屏障(也可以叫同步点) 时被阻塞,直到最后一个线程到达屏障时,屏障才会开门,
 * 所有被屏障拦截的线程才会继续干活,线程进入屏障通过CyclicBarrier的await()方法。
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/18
 */

public class CyclicBarrierDemo {

    public static void main(String[] args) {
        CyclicBarrier cyclicBarrier = new CyclicBarrier(7, () -> {
            System.out.println("召唤神龙!");
        });

        for (int i = 0; i < 7; i++) {
            final int tempInt = i;
            new Thread(() -> {
                System.out.println(Thread.currentThread().getName() + "\t 收集到第: " + tempInt + "龙珠");
                try {
                    //先到的被阻塞
                    cyclicBarrier.await();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } catch (BrokenBarrierException e) {
                    e.printStackTrace();
                }
            }, String.valueOf(i)).start();
        }
    }
}

~~~



#### 3.Semaphore

~~~java
package com.alan.demo.utils.juc.同步工具;
import java.util.concurrent.Semaphore;
import java.util.concurrent.TimeUnit;

/**
 * @Description Semaphore  的主要作用是协调对有限资源(公共资源)的访问
 *
 * <p>
 * 抢车位 比如说 6个汽车 抢占三个车位
 * (通过信号量Semaphore来控制 --> 主要通过发放许可证的方式)
 *
 * </p>
 *
 * <p>
 * semaphore有一个许可证的概念，在我们创建semaphore的时候，可以指定该semaphore中的许可证permit的总数量。
 *
 * </p>
 *
 * <p>
 * 假定Semaphore总共有N个permits，那么acquire()方法会为当前线程获取一个许可证,这时Semaphore中总共可用的许可证就少一个。还剩下N-1个。
 * 只有获取了许可证的线程才允许执行。
 * </p>
 *
 * <p>
 *  Semaphore.acquire()方法：  可能获取许可证成功，也可能获取许可证失败。
 * 1.如果获取许可证成功，那么当前线程就有了运行的许可。
 * 2.如果获取许可证失败，那么当前线程就会被阻塞住。处于Waiting状态，并不断自旋获取锁，只有在获取许可证成功的情况下，才能运行，否则将一直阻塞住。
 * </p>
 *
 * <p>
 * <p>
 *  一个线程获取了许可证，当用完之后，就需要释放，Semaphore提供了release()方法来释放一个许可证：
 * semaphore.release()方法会使：
 * 1.semaphore中可用的许可证数增加。
 *
 * </p>
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/18
 */

public class SemaphoreDemo {


    public static void main(String[] args) {
        //模拟三个停车位  参数3 相当于拥有的许可证
        Semaphore semaphore = new Semaphore(3);

        //模拟六部汽车
        for (int i = 0; i <= 6; i++) {
            new Thread(() -> {
                try {
                    //占到车位 (即当前线程获得到了许可证)
                    semaphore.acquire();
                    System.out.println(Thread.currentThread().getName() + "\t抢到车位");
                    TimeUnit.SECONDS.sleep(3);
                    System.out.println(Thread.currentThread().getName() + "\t停车3秒后离开车位");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } finally {
                    //释放车位(即当前线程释放许可证)
                    semaphore.release();
                }
            }, String.valueOf(i)).start();
        }
    }
}

~~~



#### 4.LockSupport

~~~java
package com.alan.demo.utils.juc.同步工具;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.LockSupport;
import java.util.concurrent.locks.ReentrantLock;

/**
 * @Description 两个线程
 * 第一个线程需要 从1到26  第二个线程需要从A到Z  交替打印 顺序输出  (多种方法实现)
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/8
 */

public class T02_00_LockSupport {

    static Thread t1 = null, t2 = null;

    /*给自定以自旋锁使用*/
    enum ReadyToRun {T1, T2}

    /*给自定义自旋锁使用*/
    static volatile ReadyToRun r = ReadyToRun.T1;

    public static void main(String[] args) {
        m1();//使用LockSupport 方法实现
    }


    /**
     * 使用LockSupport方法实现
     */
    private static void m1() {
        char[] aI = "1234567".toCharArray();
        char[] aC = "ABCDEFG".toCharArray();

        t1 = new Thread(() -> {
            for (char c : aI) {
                System.out.println(c);
                LockSupport.unpark(t2);//叫醒T2
                LockSupport.park();//T1阻塞
            }
        }, "t1");

        t2 = new Thread(() -> {
            for (char c : aC) {
                LockSupport.unpark(t2);//t2阻塞
                System.out.println(c);
                LockSupport.unpark(t1);//叫醒t1
            }
        }, "t2");
    }

    /**
     * 使用synchronized wait() notify() 实现
     */
    private static void m2() {
        final Object obj = new Object();
        char[] aI = "1234567".toCharArray();
        char[] aC = "ABCDEFG".toCharArray();

        new Thread(() -> {
            synchronized (obj) {
                for (char c : aI) {
                    System.out.println(c);
                    try {
                        obj.notify();
                        obj.wait();//释放锁
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                obj.notify();//因为最后总有一个线程是阻塞的状态
            }
        }, "t1").start();


        new Thread(() -> {
            synchronized (obj) {
                for (char c : aC) {
                    System.out.println(c);
                    try {
                        obj.notify();
                        obj.wait();//释放锁
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                obj.notify();
            }
        }, "t2").start();

    }

    /**
     * 使用Condition多个等待队列实现
     */
    private static void m3() {

        char[] aT = "1234567".toCharArray();
        char[] aC = "ABCDEFG".toCharArray();
        Lock lock = new ReentrantLock();

        Condition conditionT1 = lock.newCondition();

        Condition conditionT2 = lock.newCondition();

        new Thread(() -> {
            lock.lock();
            try {

                for (char c : aT) {
                    System.out.println(c);
                    conditionT2.signal();
                    conditionT1.await();
                }
                conditionT2.signal();
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                lock.unlock();
            }

        }, "t1").start();


        new Thread(() -> {
            lock.lock();
            try {

                for (char c : aC) {
                    System.out.println(c);
                    conditionT1.signal();
                    conditionT2.wait();
                }
                conditionT1.signal();

            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                lock.unlock();
            }
        }, "t2").start();
    }

    /**
     * 使用自定以自旋锁的方式实现
     */
    public void m4() {

        char[] aT = "1234567".toCharArray();
        char[] aC = "ABCDEFG".toCharArray();

        new Thread(() -> {
            for (char c : aT) {
                while (r != ReadyToRun.T1) {
                }
                System.out.println(c);
                r = ReadyToRun.T2;
            }
        }, "t1").start();

        new Thread(() -> {
            for (char c : aC) {
                while (r != ReadyToRun.T2) {
                }
                System.out.println(c);
                r = ReadyToRun.T1;
            }
        }, "t2").start();

    }
}

~~~



#### 5.Exchanger

~~~java
package com.alan.demo.utils.juc.同步工具;

import java.util.concurrent.Exchanger;

/**
 * @Description Exchaneger 同步工具  两个线程交换 装备
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/7
 */

public class T12_TestExchanger {

    static Exchanger<String> exchanger = new Exchanger<>();

    public static void main(String[] args) {

        new Thread(() -> {

            String s = "T1";
            try {
                s = exchanger.exchange(s);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + " " + s);
        }, "t1").start();


        new Thread(() -> {
            String s = "T2";
            try {
                s = exchanger.exchange(s);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + " " + s);
        }, "t2").start();

    }

}

~~~



### 二.并发容器

~~~java
package com.alan.demo.utils.juc.并发容器;

import com.google.common.util.concurrent.ThreadFactoryBuilder;

import java.util.*;
import java.util.concurrent.*;

/**
 * @Description 并发集合类不安全的问题  以及使用安全的并发容器
 * 笔记
 * 1.最好用写时复制来解决ArrayList add数据的时候 照成的不安全  List<String> list = new CopyOnWriteArrayList<>();
 * 往一个容器添加元素的时候,不直接往当前容器Object[]添加,而是先将当前容器Obejct[]进行Copy,复制出一个新的容器Obejct[] newElements
 * 然后新的容器Object[] newElments里添加元素,添加完元素之后,再将原容器的引用指向新的容器 setArray(newElements); 这样做的好处是
 * 可以对CopyOnWrite容器进行迸发的读,而不需要加锁,因为当前容器不会添加任何元素,所以CopyOnWrite容器也是一种读写分离的思想,读和写不同的容器
 * <p>
 * <p>
 * <p>
 * public boolean add(E e) {
 * synchronized (lock) {
 * Object[] elements = getArray();
 * int len = elements.length;
 * Object[] newElements = Arrays.copyOf(elements, len + 1);
 * newElements[len] = e;
 * setArray(newElements);
 * return true;
 * }
 * }
 * <p>
 * <p>
 * <p>
 * java.util.ConcurrentModificationException  并发修改异常
 * <p>
 * <p>
 * 1 故障现象
 * java.util.ConcurrentModificationException
 * 并发争抢修改导致,参考我们的花名册签名情况。
 * 一个人正在写入,另外一个同学过来抢夺,导致数据不一致异常。
 * <p>
 * <p>
 * 2 导致原因
 * <p>
 * <p>
 * 3 解决方案
 * 3.1 使用Vector 加锁
 * 3.2 Collections.synchronizedList(new ArrayList<>())
 * 3.3 List<String> list = new CopyOnWriteArrayList<>(); //写时复制
 * *
 * 4 优化建议(同样的错误不犯2次)
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/20
 */

public class ContainerNotSafeDemo {


    //核心线程数
    private static final int CORE_POOL_SIZE = 100;
    //最大线程数
    private static final int MAX_POOL_SIZE = 120;

    //线程空闲时间
    private static final Long KEEP_ALIVE_TIME = 1L;
    //队列容量
    private static final int QUEUE_CAPACITY = 500;


    public static void main(String[] args) {


    }


    /**
     * 并发容器map不安全
     */
    private static void mapIsNotSafe() {
        ThreadFactory threadFactory = new ThreadFactoryBuilder().setNameFormat("demo-pool-%d").build();

        //安全
        Map<String, String> map = new ConcurrentHashMap<>();

//安全        Map<String,String> map1 = Collections.synchronizedMap(map);
// 不安全       Map<String, String> map = new HashMap<>();


        ThreadPoolExecutor executor = new ThreadPoolExecutor(
                CORE_POOL_SIZE,
                MAX_POOL_SIZE,
                KEEP_ALIVE_TIME,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),
                threadFactory,
                new ThreadPoolExecutor.CallerRunsPolicy()
        );

        executor.execute(() -> {
            map.put(Thread.currentThread().getName(), UUID.randomUUID().toString().substring(0, 8));
            System.out.println(map);
        });
        executor.shutdown();
    }

    /**
     * 并发容器set不安全
     */
    private static void setNotSafe() {

        ThreadFactory threadFactory = new ThreadFactoryBuilder().setNameFormat("demo-pool-%d").build();

        //安全
        Set<String> set = new CopyOnWriteArraySet<>();


        //不安全
//        Set<String> set = new HashSet<>();


//安全        Set<String> set = Collections.synchronizedSet(new HashSet<>());


        ThreadPoolExecutor executor = new ThreadPoolExecutor(
                CORE_POOL_SIZE,
                MAX_POOL_SIZE,
                KEEP_ALIVE_TIME,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),
                threadFactory,
                new ThreadPoolExecutor.CallerRunsPolicy()
        );

        executor.execute(() -> {
            set.add(UUID.randomUUID().toString().substring(0, 8));
            System.out.println(set);
        });

        executor.shutdown();
    }

    /**
     * 并发容器list不安全
     */
    private static void listNotSafe() {
        ThreadFactory threadFactory = new ThreadFactoryBuilder().setNameFormat("demo-pool-%d").build();

        //安全
        List<String> list = new CopyOnWriteArrayList<>();
        //不安全
//        List<String> list = new ArrayList<>();


        ThreadPoolExecutor executor = new ThreadPoolExecutor(
                CORE_POOL_SIZE,
                MAX_POOL_SIZE,
                KEEP_ALIVE_TIME,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),
                threadFactory,
                new ThreadPoolExecutor.CallerRunsPolicy()
        );

        executor.execute(() -> {
            list.add(UUID.randomUUID().toString().substring(0, 8));
            System.out.println(list);
        });

        executor.shutdown();
    }
}

~~~



### 三.死锁

~~~java
package com.alan.demo.utils.juc.死锁;


class HoldLockThread implements Runnable {

    private String lockA;

    private String lockB;

    public HoldLockThread(String lockA, String lockB) {
        this.lockA = lockA;
        this.lockB = lockB;
    }

    @Override
    public void run() {
        synchronized (lockA) {
            System.out.println(Thread.currentThread().getName() + "\t 自己持有:" + lockA + "\t 尝试获得" + lockB);

            synchronized (lockB) {
                System.out.println(Thread.currentThread().getName() + "\t 自己持有:" + lockB + "\t 尝试获得" + lockA);
            }
        }
    }
}


/**
 * @Description 死锁是指两个或两个以上的进程在执行过程中
 * 因争夺资源而造成的一种互相等待的现象,
 * 入无外力干涉那它们都将无法推进下去
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/30
 */


public class DeadLock {

    public static void main(String[] args) {

        String lockA = "lockA";
        String lockB = "lockB";

        new Thread(new HoldLockThread(lockA, lockB), "ThreadAAA").start();

        new Thread(new HoldLockThread(lockB, lockA), "ThreadBBB").start();

        /**
         * Linux ps -ef|grep   ls -l
         * window下的java运行程序 也有类似ps的查看进程的命令,但是目前我们需要查看的只是java
         * jps = java ps     jps -l
         *
         * 然后jstack 线程ID    查看堆栈信息
         */

    }
}

~~~



### 四.生产者消费者

##### 1.阻塞队列实现

~~~java
package com.alan.demo.utils.juc.生产者消费者;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicInteger;

/**
 * @Description 3.0版本  阻塞队列
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/18
 */

/***
 * 资源
 */
class MyRescource {

    Logger logger = LoggerFactory.getLogger(getClass());
    private volatile boolean FLAG = true;//默认开启, 进行生产+消费

    private AtomicInteger atomicInteger = new AtomicInteger();

    BlockingQueue<String> blockingQueue = null;

    public MyRescource(BlockingQueue<String> blockingQueue) {
        this.blockingQueue = blockingQueue;
        logger.info(blockingQueue.getClass().getName());
    }

    /**
     * 生产者
     *
     * @throws Exception
     */
    public void myProd() throws Exception {
        String data;
        boolean retValue;
        while (FLAG) {
            data = atomicInteger.incrementAndGet() + "";
            retValue = blockingQueue.offer(data, 2L, TimeUnit.SECONDS);
            if (retValue) {
                System.out.println(Thread.currentThread().getName() + "\t 插入队列" + data + "成功");
            } else {
                System.out.println(Thread.currentThread().getName() + "\t 插入队列" + data + "失败");
            }
            TimeUnit.SECONDS.sleep(1);
        }
        System.out.println(Thread.currentThread().getName() + "\t 大老板叫停了,表示flag=false,生产动作结束");
    }

    /**
     * 消费者
     *
     * @throws Exception
     */
    public void myConsumer() throws Exception {
        String result = null;
        while (FLAG) {
            result = blockingQueue.poll(2L, TimeUnit.SECONDS);
            if (null == result || result.equalsIgnoreCase("")) {
                FLAG = false;
                System.out.println(Thread.currentThread().getName() + "\t 超过两秒钟没有取出蛋糕,消费退出");
            }
            TimeUnit.SECONDS.sleep(1);
            System.out.println(Thread.currentThread().getName() + "\t 消费队列蛋糕" + result + "成功");
        }


    }

    public void stop() throws Exception {
        this.FLAG = false;
    }

}


public class ProdConsumer_BlockQueueDemo {


    public static void main(String[] args) throws Exception {
        MyRescource myRescource = new MyRescource(new ArrayBlockingQueue<>(10));
        new Thread(() -> {
            System.out.println(Thread.currentThread().getName() + "\t 生产线程启动");
            try {
                myRescource.myProd();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }, "Prod").start();



        new Thread(() -> {
            System.out.println(Thread.currentThread().getName() + "\t 消费线程启动");
            try {
                myRescource.myConsumer();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }, "Consumer").start();

        //暂停一会线程
        try {
            TimeUnit.SECONDS.sleep(5);
            System.out.println();
            System.out.println();
            System.out.println();
            System.out.println("5秒钟时间到,大老板main线程叫停,活动叫停");
            myRescource.stop();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

~~~



##### 2.传统实现方式

~~~java
package com.alan.demo.utils.juc.生产者消费者;

import com.google.common.util.concurrent.ThreadFactoryBuilder;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ThreadFactory;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

//资源类
class ShareData {

    private int number = 0;
    private Lock lock = new ReentrantLock();
    private Condition condition = lock.newCondition();


    /**
     * 加
     *
     * @throws Exception
     */
    public void increment() throws Exception {

        lock.lock();
        try {
            //1 判断
            while (number != 0) {
                //等待,不能生产
                condition.await();
            }

            //2 干活
            number++;
            System.out.println(Thread.currentThread().getName() + "\t" + number);
            //3 通知唤醒
            condition.signal();

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }

    }

    /**
     * 减
     *
     * @throws Exception
     */
    public void decrement() throws Exception {

        lock.lock();
        try {
            //1 判断
            while (number == 0) {
                //等待,不能生产
                condition.await();
            }

            //2 干活
            number--;
            System.out.println(Thread.currentThread().getName() + "\t" + number);
            //3 通知唤醒
            condition.signal();

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }

    }
}


/**
 * @Description 题目: 一个初始值为零的变量,两个线程对其交替操作,一个加1 一个减1 来五轮
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/18
 */

public class ProdConsumer_TraditionDemo {

    //核心线程数
    private static final int CORE_POOL_SIZE = 2;
    //最大线程数
    private static final int MAX_POOL_SIZE = 2;

    //线程空闲时间
    private static final Long KEEP_ALIVE_TIME = 1L;
    //队列容量
    private static final int QUEUE_CAPACITY = 500;


    public static void main(String[] args) {
        ThreadFactory threadFactory = new ThreadFactoryBuilder().setNameFormat("demo-pool-%d").build();
        ShareData shareData = new ShareData();


        ThreadPoolExecutor executor = new ThreadPoolExecutor(
                CORE_POOL_SIZE,
                MAX_POOL_SIZE,
                KEEP_ALIVE_TIME,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),
                threadFactory,
                new ThreadPoolExecutor.CallerRunsPolicy()
        );
        executor.execute(() -> {
            for (int i = 0; i < 5; i++) {
                try {
                    shareData.increment();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        });


        executor.execute(() -> {
            for (int i = 0; i < 5; i++) {
                try {
                    shareData.decrement();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        });
        executor.shutdown();


        try {
            TimeUnit.SECONDS.sleep(Integer.MAX_VALUE);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

~~~





##### 3.Condition方式实现

~~~java
package com.alan.demo.utils.juc.生产者消费者;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * @Description 使用Lock 实现 三个线程 按顺序打印    A线程 5次 B线程 10次  C线程 15   打印10轮
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/18
 */

/**
 * 资源类
 */
class ShareResource {

    private int number = 1;//定义标识位

    private Lock lock = new ReentrantLock();

    public Condition c1 = lock.newCondition();

    public Condition c2 = lock.newCondition();

    public Condition c3 = lock.newCondition();


    /**
     * 打印五次
     */
    public void print5() {
        lock.lock();
        try {

            //判断
            while (number != 1) {
                c1.await();
            }

            for (int i = 0; i < 5; i++) {
                System.out.println(Thread.currentThread().getName() + "\t" + i);
            }
            number = 2;//改变标志位
            c2.signal();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    /**
     * 打印十次
     */
    public void print10() {
        lock.lock();
        try {
            //判断
            while (number != 2) {
                c2.await();
            }

            for (int i = 0; i < 10; i++) {
                System.out.println(Thread.currentThread().getName() + "\t" + i);
            }
            number = 3;
            c3.signal();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    /**
     * 打印十五次
     */
    public void print15() {
        lock.lock();
        try {
            //判断
            while (number != 3) {
                c3.await();
            }

            for (int i = 0; i < 10; i++) {
                System.out.println(Thread.currentThread().getName() + "\t" + i);
            }
            number = 1;
            c1.signal();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

}


public class SynAndReentrantLockDemo {

    public static void main(String[] args) {
        ShareResource shareResource = new ShareResource();

        new Thread(() -> {
            for (int i = 0; i < 10; i++) {
                shareResource.print5();
            }
        }, "A").start();


        new Thread(() -> {
            for (int i = 0; i < 10; i++) {
                shareResource.print10();
            }
        }, "B").start();


        new Thread(() -> {
            for (int i = 0; i < 15; i++) {
                shareResource.print15();
            }
        }, "C").start();
    }
}

~~~



### 五.读写锁

#### 1.案例

~~~java
package com.alan.demo.utils.juc.读写锁;

import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.ReentrantReadWriteLock;

/**
 * @Description 读写锁
 * <p>
 * 多个线程同时读一个资源类没有任何问题,所以为了满足并发量,读取共享资源应该可以同时进行。
 * 但是
 * 如果有一个线程想去写共享资源来,就不应该再有其它线程可以对该资源进行读或写
 * 小总结:
 * <p>
 * 读 -读能共存
 * 读 -写不能共存
 * 写-写不能共存
 * <p>
 * 写操作: 原子+独占,整个过程必须是一个完整的统一体,中间不许被分割,被打断
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/1
 */

//资源类
class Mycache {


    volatile Map<String, Object> map = new HashMap<>();

    private ReentrantReadWriteLock rwLock = new ReentrantReadWriteLock();


    public void put(String key, Object value) {

        rwLock.writeLock().lock();
        try {
            System.out.println(Thread.currentThread().getName() + "\t 正在写入: " + key);
            //暂停一会线程
            TimeUnit.SECONDS.sleep(2);
            map.put(key, value);
            System.out.println(Thread.currentThread().getName() + "\t 写入完成: ");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            rwLock.writeLock().unlock();
        }

    }

    public void get(String key) {

        rwLock.readLock().lock();
        try {
            System.out.println(Thread.currentThread().getName() + "\t 正在读取: " + key);

            //暂停一会线程

            TimeUnit.SECONDS.sleep(2);

            Object result = map.get(key);

            System.out.println(Thread.currentThread().getName() + "\t 读取完成: " + result);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            rwLock.readLock().unlock();
        }
    }

}

public class ReadWriteLock {

    public static void main(String[] args) {
        Mycache mycache = new Mycache();

        //写
        for (int i = 1; i <= 5; i++) {
            final int tempInt = i;
            new Thread(() -> {
                mycache.put(tempInt + "", tempInt + "");
            }, String.valueOf(i)).start();
        }

        //读
        for (int i = 1; i <= 5; i++) {
            final int tempInt = i;
            new Thread(() -> {
                mycache.get(tempInt + "");
            }, String.valueOf(i)).start();
        }
    }
}

~~~



#### 2.案例

~~~java
package com.alan.demo.utils.juc.读写锁;

import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

/**
 * @Description 读写锁
 * 首先启动读线程，此时number为0；然后某个时刻写线程修改了共享资源number数据，读线程再次读取最新值！
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/2/19
 */

public class ReadWriteLockDemo {


    public static void main(String[] args) throws InterruptedException {
        ReadWrite rwd = new ReadWrite();
        //启动100个读线程
        for (int i = 0; i < 100; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    rwd.get();
                }
            }, "Read").start();
        }

        //写线程
        new Thread(new Runnable() {
            @Override
            public void run() {
                rwd.set((int) (Math.random() * 101));
            }
        }, "Write").start();

    }
}

class ReadWrite {
    //模拟共享资源--Number
    private int number = 0;
    // 实际实现类--ReentrantReadWriteLock，默认非公平模式
    private ReadWriteLock readWriteLock = new ReentrantReadWriteLock();

    //读
    public void get() {
        //使用读锁
        readWriteLock.readLock().lock();
        try {
            System.out.println(Thread.currentThread().getName() + " : " + number);
        } finally {
            readWriteLock.readLock().unlock();
        }
    }

    //写
    public void set(int number) {
        readWriteLock.writeLock().lock();
        try {
            this.number = number;
            System.out.println(Thread.currentThread().getName() + " : " + number);
        } finally {
            readWriteLock.writeLock().unlock();
        }
    }
}
~~~



### 六.CAS

#### 1.cas是什么?

~~~java
package com.alan.demo.utils.juc.CAS;

import java.util.concurrent.atomic.AtomicInteger;

/**
 * @Description 1. CAS 是什么? ===>compareAndSet
 * 比较并交换
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/19
 */

public class CASDemo {


    public static void main(String[] args) {
        AtomicInteger atomicInteger = new AtomicInteger(5);

        atomicInteger.getAndIncrement();

        System.out.println(atomicInteger.compareAndSet(5, 2019) + "\t current data " + atomicInteger.get());
        System.out.println(atomicInteger.compareAndSet(6, 2020) + "\t current data " + atomicInteger.get());

    }
}

~~~



#### 2.手写自旋锁

~~~java
package com.alan.demo.utils.juc.CAS;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicReference;

/**
 * @Description 手写自旋锁
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/20
 */

public class SpinLockDemo {

    //原子引用线程
    AtomicReference<Thread> atomicReference = new AtomicReference<>();


    //上锁
    public void myLock() {
        Thread thread = Thread.currentThread();
        System.out.println(Thread.currentThread().getName() + "\t come in O(n_n)O");

        while (!atomicReference.compareAndSet(null, thread)) {

        }
    }

    //解锁
    public void myUnlock() {
        Thread thread = Thread.currentThread();
        atomicReference.compareAndSet(thread, null);
        System.out.println(Thread.currentThread().getName() + "\t invoked myUnLock()");
    }

    public static void main(String[] args) throws InterruptedException {
        SpinLockDemo spinLockDemo = new SpinLockDemo();

        new Thread(() -> {
            //暂停一会线程
            try {

                spinLockDemo.myLock();
                TimeUnit.SECONDS.sleep(5);
                spinLockDemo.myUnlock();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }, "AA").start();

        TimeUnit.SECONDS.sleep(1);

        new Thread(() -> {
            spinLockDemo.myLock();
            spinLockDemo.myUnlock();
        }, "BB").start();
    }
}
~~~





### 七.可重入锁

#### 1.案例

~~~java
package com.alan.demo.utils.juc.可重入锁;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * @Description 可重入锁 落地实现
 * synchronized  和 ReentrantLock 都是可重入锁
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/1
 */


//资源类
class Phone {

    public synchronized void sendSMS() {
        System.out.println(Thread.currentThread().getId() + "\t invoked sendSMS()");
        sendEmail();
    }

    private synchronized void sendEmail() {
        System.out.println(Thread.currentThread().getId() + "\t ######invoked sendEmail()");
    }


    public void get() {
        System.out.println(Thread.currentThread().getId() + "\t invoked sendSMS()");

        Lock lock = new ReentrantLock();
        lock.lock();
        try {
            set();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    private void set() {
        System.out.println(Thread.currentThread().getId() + "\t ######invoked sendEmail()");
    }

}

public class ReenterLockDemo {

    public static void main(String[] args) {
        Phone phone = new Phone();

        new Thread(() -> {
            //线程操作资源类
            phone.sendSMS();
        }, "A").start();

        try {
            TimeUnit.SECONDS.sleep(5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        new Thread(() -> {
            //线程操作资源类
            phone.sendSMS();
        }, "B").start();

        System.out.println("-----------------------------以上是synchronized实现的可重入锁----------------------------------");


        System.out.println("-----------------------------以下是ReentrantLock实现的可重入锁---------------------------------");
        try {
            TimeUnit.SECONDS.sleep(5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        new Thread(() -> {

            Lock lock = new ReentrantLock();
            lock.lock();
            try {
                phone.get();
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                lock.unlock();
            }

        }, "C").start();
    }
}
~~~



#### 2..案例

~~~java
package com.alan.demo.utils.juc.可重入锁;

/**
 * @Description 可重入锁   就是说某个线程已经获得某个锁,可以再次获取锁而不会出现死锁
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/6
 */

public class WhatReentrant {

    public static void main(String[] args) {
        new Thread(new Runnable() {
            @Override
            public void run() {
                synchronized (this) {
                    System.out.println("第1次获取锁,这个锁是: " + this + "线程名称是: " + Thread.currentThread().getName());
                    int index = 1;
                    while (true) {
                        synchronized (this) {
                            System.out.println("第" + (++index) + "次获取锁，这个锁是：" + this + "线程名称是: " + Thread.currentThread().getName());
                        }
                        if (index == 10) {
                            break;
                        }
                    }
                }
            }
        }).start();
    }
}
~~~







### 八.AQS

~~~
是实现自旋锁的框架
~~~







