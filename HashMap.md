```java
package com.alan.demo.utils.collection;
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.Map;

/**
 * @Description 1.7的 map 多线程下 具有ABA问题 比如两个线程
 * 第一个线程刚好 到达需要扩容 这时候第二个线程抢先了  （因为主要采用了头插法）
 * <p>
 * 解决方法 -->使用currentHashMap
 * @Author gaodehan
 * |----Map: 双列数据，存储key-value对的数据  ---类似于高中的函数: y=f(x)
 * |----HashMap：作为Map的主要实现类 线程不安全 效率高; 存储null的key和value
 * ----LinkedHashMap：保证在遍历map元素时,可以按照添加的顺序实现遍历
 * 原因: 在原有的HashMap底层的结构基础上,添加了一对指针,指向前一个和后一个元素。
 * 对于频繁的遍历操作,此类执行效率高于HashMap
 * ---- TreeMap 保证按照添加的key-value对进行排序,实现排序遍历,此时主要是key的自然排序
 * 和自定义排序
 * ----Hashtable：作为古老的实现类; 线程安全的,效率低;不能存储null的key和value
 * ----Properties： 常用来处理配置文件。key和value都是String类型
 * <p>
 * HashMap的底层: 数组+链表 (jdk7及之前)
 * 数组+链表+红黑树(jdk 8)
 * <p>
 * <p>
 * 面试题
 * 1.HashMap的底层原理?
 * 2.HashMap和Hashtable的异同
 * 3.CurrentHashMap 与Hashtable的异同?
 * <p>
 * 二 Map结构的理解
 * Map中的key:无序的,不可重复的,使用Set存储所有的key -->key所在类要重写equals() 和hashCode()
 * Map中的value: 无序的,可重复的,使用Collection存储所有的value
 * 一个键值对: key-value构成了一个Entry对象
 * Map中的entry：无序的,不可重复的,使用Set存储所有的entry
 * 三 HashMap的底层实现原理? 以jdk7为例说明
 * HashMap map = new HashMap();
 * 在实例化以后,底层创建了长度是16的一维数组Entry[] table;
 * map.put(key1,value1);
 * 首先,调用key1所在类的hashCode()计算key1哈希值,此哈希值经过某种算法计算之后,得到在Entry数组中得位置
 * 如果此位置上得数据为空,此时得key1-value1添加成功.-----情况1
 * 如果此位置上得数据不为空,(意味着此位置上存在一个或多个数据(以链表形式存在)).
 * 比较key1和已经存在得一个或多个数据得哈希值:
 * 如果key1的哈希值与已经存在的数据的哈希值都不同,此时key1-value1 添加成功. -----情况2
 * 如果key1的哈希值和已经存在的某一个数据(key2-value2)的哈希值相同,继续比较: 调用key1所在类的equals()方法,比较:
 * 如果equals()返回false: 此时key1-value1添加成功。------情况3
 * 如果equals()返回true: 将使用value1替换value2。
 * <p>
 * 补充:  关于情况2和情况3： 此时key1-value1和原来的数据以链表的的方式存储
 * <p>
 * 在不断的添加过程中,会涉及到扩容问题,默认的扩容方式： 扩容为原来的2倍,并将原有的数据复制过来
 * <p>
 * <p>
 * jdk8 相较于jdk7在底层实现方面的不同:
 * 1.new HashMap(): 底层没有创建一个长度为16的数组
 * 2.jdk 8底层的数组是: Node[],而非Entry[]
 * 3.首次调用put()方法时,底层创建长度为16的数组
 * 4.jdk 7底层结构只有: 数组+链表. jdk8中底层结构: 数组+链表+红黑树
 * 当数组的某一个索引位置上的元素以链表形式存在的数据个数>8 且当前数组的长度> 64
 * 此时索引位置上的所有数据改为使用红黑树存储
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/23
 */

public class MapTest {

    public static void main(String[] args) {
//        test2();
        test3();
    }

    private static void test3() {
        Map<String, String> map = new HashMap<>();
        map.put("k1", "v1");
        map.put("k2", "v2");
        map.put("k3", "v3");
        map.put("k4", "v4");
        map.forEach((k, v) -> {
            System.out.println("键为: " + k + "值为: " + v);
        });
    }


    public void test1() {
        Map map = new HashMap();
        map.put(null, 123);
    }

    /**
     * 测试LinkedHashMap 跟HashMap的主要区别是 多了一层链表
     * 能够找到插入元素的顺序
     */
    public static void test2() {
        Map<String, String> map = new LinkedHashMap<>();
        map.put("k1", "v1");
        map.put("k2", "v2");
        map.put("k3", "v3");

        map.forEach((k, v) -> {
            System.out.println("键值为: " + k + " 值为: " + v);

        });
    }

    /**
     * 谈谈你对HashMap中put/get方法的认识? 如果了解在谈谈HashMap的
     * 扩容机制? 默认大小是多少? 什么是负载因子(或填充比)? 什么是吞吐临界值(或阀值 threold)
     * <p>
     * DEFAULT_INITIAL_CAPACITY： HashMap的默认容量 16
     * MAXIMUM_CAPACITY: HashMap的最大支持量, 2^30
     * DEFAULT_LOAD_FACTOR: HashMap的默认加载因子
     * TREEIFY_THRESHOLD: Bucket中链表长度大于该默认值 转化为红黑树
     * UNTREEIFY_THRESHOLD: Bucket中红黑树存储的Node小于该默认值,转化为链表
     * MIN_TREEIFY_CAPACITY: 桶中的Node被树化时最小的hash表容量(当桶中Node的数量大到需要变红黑树时,若
     * hash表容量小于MIN_TREEIFY_CAPACITY时,此时应执行resize扩容操作这个MIN_TREEIFY_CAPACITY的值至少是
     * TREEIFY_THRESHOLD的4倍)
     * <p>
     * table: 存储元素的数组,总是2的n次幂
     * entrySet： 存储具体元素的集
     * size: HashMap中存储的键值对的数量
     * modCount: HashMap扩容和结构改变的次数。
     * threshold: 扩容的临界值, =容量*填充因子
     * loadFactor: 填充因子
     * <p>
     *
     *
     * <p>
     **/

    public static void test4() {
        Map<String, String> map = new HashMap<>();
        map.put("k1", "v1");
    }


}
```