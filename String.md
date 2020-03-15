### String的内存结构

~~~java
package com.alan.demo.utils.string;
/**
 * @Description String(不可变性)
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/29
 */

public class StringTest {

    public static void main(String[] args) throws InterruptedException {
//        test1();
//        test2();
        test3();
        Thread.sleep(Integer.MAX_VALUE);
    }

    /**
     * String： 字符串,使用一对""引起来表示。
     * 1.String 声明为final的,不可被继承
     * 2.String 实现了Seriallizable接口: 表示字符串是支持序列化的
     * 实现了Comparable接口： 表示String可以比较大小
     * 3.String内部定义了final char[] value 用于存储字符串数据
     * 4.String 代表不可变的字符序列  简称: 不可变性
     *
     * 体现:1.当字符串重新赋值时，需要重写指定内存区域赋值,不能使用原有的value赋值
     * 2.当对现有的字符串进行连接操作时,也需要重新指定内存区域赋值,不能使用原有的value赋值
     *
     * 5.通过字面量的方式(区别于new)给一个字符串赋值,此时的字符串声明在字符串常量池中。
     * 6.字符串常量池中是不会存储相同内容的字符串的。
     */
    public static void test1() throws InterruptedException {
        String s1 = "abc";//字面量的定义方式
        String s2 = "abc";
        s1 = "hello";

        System.out.println(s1);
        System.out.println(s2);

    }

    /**
     * 相当于在栈中创建了一个引用,然后在堆空间中创建对象,然后指向常量池中的对象
     * 比如说是 Tom
     */
    public static void test2() {
        Person p1 = new Person("Tom", 12);

        Person p2 = new Person("Tom", 12);

        System.out.println(p1.name.equals(p2.name));//true
        System.out.println(p1.name == p2.name);//true

        p1.name = "Jerry";
        System.out.println(p2.name);//Tom
    }

    /**
     * String经典面试题
     * <p>
     * 结论:
     * 1.常量与常量的拼接结果在常量池。且常量池中不会存在相同内容的常量。
     * 2. 只要其中有一个是变量,结果就在堆中
     */
    public static void test3() {
        String s1 = "javaEE";
        String s2 = "hadoop";


        String s3 = "javaEEhadoop";
        String s4 = "javaEE" + "hadoop";
        String s5 = s1 + "hadoop";
        String s6 = "javaEE" + s2;

        System.out.println(s3 == s4);//true
        System.out.println(s3 == s5);//false
        System.out.println(s3 == s6);//false
        System.out.println(s5 == s6);//false

        String s8 = s5.intern();//返回值得到的s8使用常量池中已经存在的"javaEEhadoop"
        System.out.println(s3 == s8);//true
    }

}

~~~





```java
package com.alan.demo.utils.string;

/**
 * @Description 基本数据类型传的是值
 * 引用数据类型传递的是地址
 * 但是String比较特殊 具有不可变性
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/29
 */

public class StringTest2 {

    /**
     * string经典面试题
     */
    String str = new String("good");
    char[] ch = {'t', 'e', 's', 't'};

    public void change(String str, char[] ch) {
        str = "test ok";
        ch[0] = 'b';
    }

    public static void main(String[] args) {
        StringTest2 ex = new StringTest2();
        ex.change(ex.str, ex.ch);
        System.out.println(ex.str);//good
        System.out.println(ex.ch);//best
    }
}
```





### String常用方法



~~~java
int length(): 返回字符串长度:  return value.length
    
char charAt(int index): 返回某索引的字符return value[index]
    
boolean isEmpty(): 判断是否是空的字符串: return value.length == 0
    
String toLowerCase(): 使用默认语言环境,将String中的所有字符转换为小写
    
String toUpperCase(): 使用默认语言环境,将String中的所有字符转换为小写

String trim(): 返回字符串的副本,忽略前导空白和尾部空白

boolean equals(Object obj): 比较字符串的内容是否相同
    
boolean equalsIgnoreCase(String anotherString): 与equals方法类似,忽略大小写

String concat(String str): 将指定字符串连接到此字符的结尾。等价于用"+"  
    
int compareTo(String anotherString): 比较两个字符串的大小
    
String substring(int beginIndex):  返回一个新的字符串,它是此字符串的从beginIndex开始截取到最后的一个子字符串。
    
String substring(int beginIndex,int endIndex): 返回一个新的字符串,它是此字符串从beginIndex开始截取到endIndex(不包含)的一个子字符串    
~~~



~~~java
boolean endsWith(String suffix): 测试此字符串是否以指定的后缀结束

boolean startsWith(String prefix): 测试此字符串是否以指定的前缀开始
    
boolean startsWith(String prefix,int toffset): 测试此字符串从指定索引开始的子字符串是否以指定前缀开始
    
boolean contains(CharSequence s): 当且仅当此字符串包含指定的char值序列时,返回true

int indexOf(String str): 返回指定子字符串在此字符串中第一次出现的索引

int indexOf(String str,index fromIndex): 返回指定子字符串在此字符串中第一次出现处的索引,从指定的索引开始

int lastIndexOf(String str): 返回指定子字符串中最后边出现处的索引

int lastIndexOf(String str,int fromIndex): 返回指定子字符串在此字符中最后
 一次出现处的索引,从指定的索引开始反向搜索
注: indexOf和lastIndexOf方法如果未找到都是返回-1    
~~~



~~~java
String replace(char oldChae,char newChar): 返回一个新的字符串,它是通过用newChar替换此字符串中出现的所有oldChar得到的。

String replace(CharSequence target,CharSequence replacement): 使用指定的字面值替换序列替换此字符串所有匹配字面值目标序列的子字符串。

String replaceAll(String regex,String replacement): 使用给定的replacement替换此字符串所有匹配给定的正则表达式的子字符串

String replaceFirst(String regex,String replacement): 使用给定的replacement替换此字符串匹配给定的正则表达式的第一个子字符串。

boolean matches(String regex): 告知此字符串是否匹配给定的正则表达式。
    
String[] spilt(String regex): 根据给定正则表达式的匹配拆分此字符串。

String[] spilt(String regex,int limit): 根据匹配给定的正则表达式来拆分此字符串,最多不超过limit个,如果超过了,剩下的全部都放到最后一个元素中。    
~~~



~~~java
String 转换为字符数组
    
String str  = "123";
Char[] val = str.tocharArrray();
    
~~~



### StringBuffer 和StringBuilder的使用

~~~java
package com.alan.demo.utils.string;

/**
 * @Description 关于StringBuffer 和StringBuilder的使用
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/1/29
 */

public class StringBufferBuilderTest {

    /*
     String,StringBuffer,StringBuilder三者的异同?
     String: 不可变的字符序列;底层使用char[] 数组存储
     StringBuffer: 可变的字符序列 线程安全的,效率偏低
     StringBuilder: 可变的字符序列: jdk5.0新增线程不安全的,效率高;

    源码分析：
    String str = new String(); //char[] value = new char[0];
    String str1 = new String("abc");//char[] value = new char[]{'a','b','c'};

    StringBuffer sb1 = new StringBuffer();//char[] value = new char[16]; 创建一个长度为16的数组
    sb1.append('a');//value[0] = 'a';
    sb1.append('b');//value[1] = 'b';

    StringBuffer sb2 = new StringBuffer("abc");//char[] value = new char["abc".length()+16]

  扩容问题:
  如果要添加的数据底层数组装不下了,那就需要扩容底层的数组
  默认情况下,扩容为原来的2倍+2,同时将原有数组中的元素复制到新的数组中
  
    StringBuffer StringBuilder中的常用方法

    增: append(xxx)
    删: delete(int start,int end)
    改: setCharAt(int n,char ch)
    查: charAt(int n)
    插: insert(int offset,xxx)
    长度: length()
     */
    public static void main(String[] args) {

        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append("123");
        stringBuilder.append("456");
        System.out.println(stringBuilder.toString());
    }

}

~~~



