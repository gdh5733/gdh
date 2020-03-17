### Collections常用方法

~~~java
package com.alan.demo.utils.collections;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

/**
 * @Description Collections 工具类常用方法:
 * <p>
 * 1.排序
 * 2.查找,替换操作
 * 3.同步控制(不推荐，需要线程安全的集合类型时请考虑使用 JUC 包下的并发集合)
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/2/4
 */

public class CollectionsUtil {

    public static void main(String[] args) {
        test1();
    }

    /**
     * 排序操作
     * void reverse(List list)//反转
     * void shuffle(List list)//随机排序
     * void sort(List list)//按自然排序的升序排序
     * void sort(List list, Comparator c)//定制排序，由Comparator控制排序逻辑
     * void swap(List list, int i , int j)//交换两个索引位置的元素
     * void rotate(List list, int distance)//旋转。当distance为正数时，将list后distance个元素整体移到前面。当distance为负数时，将 list的前distance个元素整体移到后面。
     */


    public static void test1() {
        ArrayList<Integer> arrayList = new ArrayList<Integer>();
        arrayList.add(-1);
        arrayList.add(3);
        arrayList.add(3);
        arrayList.add(-5);
        arrayList.add(7);
        arrayList.add(4);
        arrayList.add(-9);
        arrayList.add(-7);

        System.out.println("原始数组:");
        System.out.println(arrayList);
        // void reverse(List list)：反转
        Collections.reverse(arrayList);
        System.out.println("Collections.reverse(arrayList):");
        System.out.println(arrayList);


        Collections.rotate(arrayList, 4);
        System.out.println("Collections.rotate(arrayList, 4):");
        System.out.println(arrayList);


        // void sort(List list),按自然排序的升序排序
        Collections.sort(arrayList);
        System.out.println("Collections.sort(arrayList):");
        System.out.println(arrayList);

        // void shuffle(List list),随机排序
        Collections.shuffle(arrayList);
        System.out.println("Collections.shuffle(arrayList):");
        System.out.println(arrayList);

        // void swap(List list, int i , int j),交换两个索引位置的元素
        Collections.swap(arrayList, 2, 5);
        System.out.println("Collections.swap(arrayList, 2, 5):");
        System.out.println(arrayList);


        // 定制排序的用法
        arrayList.sort(new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2.compareTo(o1);
            }
        });

        System.out.println("定制排序后：");
        System.out.println(arrayList);

    }

    /**
     * int binarySearch(List list, Object key)//对List进行二分查找，返回索引，注意List必须是有序的
     * int max(Collection coll)//根据元素的自然顺序，返回最大的元素。 类比int min(Collection coll)
     * int max(Collection coll, Comparator c)//根据定制排序，返回最大元素，排序规则由Comparatator类控制。类比int min(Collection coll, Comparator c)
     * void fill(List list, Object obj)//用指定的元素代替指定list中的所有元素。
     * int frequency(Collection c, Object o)//统计元素出现次数
     * int indexOfSubList(List list, List target)//统计target在list中第一次出现的索引，找不到则返回-1，类比int lastIndexOfSubList(List source, list target).
     * boolean replaceAll(List list, Object oldVal, Object newVal), 用新元素替换旧元素
     */
    public static void tes2() {

        ArrayList<Integer> arrayList = new ArrayList<Integer>();
        arrayList.add(-1);
        arrayList.add(3);
        arrayList.add(3);
        arrayList.add(-5);
        arrayList.add(7);
        arrayList.add(4);
        arrayList.add(-9);
        arrayList.add(-7);
        ArrayList<Integer> arrayList2 = new ArrayList<Integer>();
        arrayList2.add(-3);
        arrayList2.add(-5);
        arrayList2.add(7);
        System.out.println("原始数组:");
        System.out.println(arrayList);

        System.out.println("Collections.max(arrayList):");
        System.out.println(Collections.max(arrayList));

        System.out.println("Collections.min(arrayList):");
        System.out.println(Collections.min(arrayList));

        System.out.println("Collections.replaceAll(arrayList, 3, -3):");
        Collections.replaceAll(arrayList, 3, -3);
        System.out.println(arrayList);

        System.out.println("Collections.frequency(arrayList, -3):");
        System.out.println(Collections.frequency(arrayList, -3));

        System.out.println("Collections.indexOfSubList(arrayList, arrayList2):");
        System.out.println(Collections.indexOfSubList(arrayList, arrayList2));

        System.out.println("Collections.binarySearch(arrayList, 7):");
        // 对List进行二分查找，返回索引，List必须是有序的
        Collections.sort(arrayList);
        System.out.println(Collections.binarySearch(arrayList, 7));
    }

}

~~~

