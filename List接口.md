### List集合中常用的方法

~~~java
void add(int index,Object ele): 在index位置插入ele元素

boolean addAll(int index,Collection eles): 从index位置开始将eles中的所有元素添加进来

Object get(int index): 获取指定index位置的元素
 
int indexOf(Object obj): 返回obj在当前集合中首次出现的位置

int lastIndexOf(Object obj): 返回obj在当前集合中末出现的位置

Object remove(int index): 移除指定index位置的元素,并返回此元素

Object set(int index,Object ele): 设置指定index位置的元素  
    
List sublist(int fromIndex,int toIndex): 返回从fromIndex 到toIndex位置的子集合
~~~

