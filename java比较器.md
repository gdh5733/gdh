### 自然排序



```java
package com.alan.demo.utils.compare;
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

/**
 *
 *
 * 自然排序
 *
 * @Description 一.说明: Java中的对象,正常情况下,只能进行比较: == 或 !=。 不能使用> 或<的
 * 但在开发场景中,我们需要对多个对象进行排序,言外之意,就需要比较对象的大小。如何实现?
 * 使用两个接口中的任何一个: Comparable或Comparator
 * 二. Comparable接口的使用
 * 1.像String,包装类等实现了Comparable接口,重写了compareTo(boj)方法,给出了比较两个对象
 * 2.像String,包装类重写compareTo()方法以后,进行了从小到大的排列
 * 3.重写compareTo(obj)的规则:
 * 如果当前对象this大于形参对象的obj,则返回正整数,
 * 如果当前对象this小于形参对象obj,则返回负整数
 * 如果当前对象this等于形参对象obj,则返回零。
 * 4.对于自定义类来说,如果需要排序,我们可以自定义类实现Comparable接口,重写comapreTo
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/12
 */

@Setter
@Getter
@ToString
public class CompareToTest {


    /**
     * Student使用自定义排序 实现了Comparable
     */
    @Setter
    @Getter
    @ToString
    class Student implements Comparable {
        int age;
        String name;

        @Override
        public int compareTo(Object o) {
            Student stu = (Student) o;
            if (this.age < stu.age) {
                return 1;
            }
            return -1;
        }
    }
    

    public void test1() {

        Student student = new Student();
        student.setAge(10);
        student.setName("alan");

        Student student1 = new Student();
        student1.setAge(30);
        student1.setName("jack");

        Student student2 = new Student();
        student2.setAge(20);
        student2.setName("mike");

        List<Student> val = new ArrayList<>();
        val.add(student);
        val.add(student1);
        val.add(student2);

        Collections.sort(val);

        System.out.println(val);

    }


    public static void main(String[] args) {

        CompareToTest val = new CompareToTest();
        val.test1();
     
    }
}

```





### 定制排序

~~~java
package com.alan.demo.utils.compare;

import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

/**
 * @Description 定制排序
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/12
 */

public class CompareTest {

    /**
     * Comparator接口的使用
     * 1.背景:
     * 当元素的类型没有实现java.lang.Comparable接口而又不方便修改代码,
     * 或者实现了java.lang.Comparable接口的排序规则不适合当前的操作,
     * 那么可以考虑使用Comparator的对象排序
     * 2.重写compare(Object,Object)方法,比较o1和o2的大小:\
     * 如果方法返回正整数,则表示o1大于o2;
     * 如果返回0,表示相等;
     * 返回负整数,表示o1小于o2。
     */


    @Setter
    @Getter
    @ToString
    class Car {
        int age;
        String band;
    }

    public void test2() {
        Car car = new Car();
        car.setAge(10);
        car.setBand("奥迪");

        Car car1 = new Car();
        car1.setAge(30);
        car1.setBand("保时捷");

        Car car2 = new Car();
        car2.setBand("奔驰");

        List<Car> val = new ArrayList<>();
        val.add(car);
        val.add(car1);
        val.add(car2);

        //注意该处用到的是Comparator 而不是Compareable
        Collections.sort(val, new Comparator<Car>() {
            @Override
            public int compare(Car o1, Car o2) {
                return o1.getAge() - o2.getAge();
            }
        });

        System.out.println(val);
    }
}

~~~



