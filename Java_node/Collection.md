# 集合

## 概述

![image-20220320130143830](../picture/image-20220320130143830.png)

1. 集合、数组都是对多个数据进行存储操作的结构，简称 Java 容器

   说明：此时的存储，主要是指内存层面的存储，不涉及持久化的存储

2. Java集合可分为两种体系，一种是Collection 和Map 体系

3. Colection 接口：单列数据，定义了存取一组对象的方法集合

   1. List：元素有序、可重复的集合 ➡动态数组

      ArrayList、LinkedList、Vector

   2. Set：元素无序、不可重复的集合

      HashSet、LinkedHashSet、TreeSet

4. Map 接口：双列数据，保存具有映射关系 "Key-Vaule " 对的集合

   HashMap、LinkedHashMap、TreeMap、Properties 

## 继承树

![image-20220320132510490](../picture/image-20220320132510490.png)

![image-20220320132518611](../picture/image-20220320132518611.png)

## collection的主要方法

```java
	@Test
	public void test1(){
        Collection coll = new ArrayList();
        //add(Object e):将元素添加进集合coll中
        coll.add("AA");
        coll.add(123);//自动装箱
        coll.add(new Date());
        //size():获取添加元素的个数
        System.out.println(coll.size());//3
       
        Collection coll1 = new ArrayList();
        coll1.add(456);//自动装箱
        coll1.add("CC");
        //addAll(Collection collection):将参数collection集合中华的元素添加进当前的集合中
        coll.addAll(coll1);
        System.out.println(coll.size());//5
        System.out.println(coll);//[AA,123,Tue Feb 19 1:54:48 GMT+08:00 2019,456,CC]
    //isEmpty()判断当前集合是否为空(非判断是否为null，而是检查是否有元素)
        System.out.println(coll.isEmpty());//false
    // clear():清空元素
        coll.clear();
        System.out.println(coll.isEmpty());//true
    }
```

##  

```java
	class Person{
         private String name;
   		 private int age;
        ..........
        //省略get/set方法和toString
    }	 
	
    public class ArraysTest {
        public static void main(String[] args) {
            Collection arr1 = new ArrayList();
            arr1.add(123);
            arr1.add(new String("W"));
            arr1.add(new Person("Unix",123));
            arr1.add(true);
            //contains(Object obj)判断当前集合是否包含obj
            System.out.println(arr1.contains(123));//true
            System.out.println(arr1.contains(new String("W")));//true ，这里底层是调用了String引用类的equals()方法
            System.out.println(arr1.contains(new Person("Unix", 123)));//false ，因为自定义类Person没有去重写equals()方法，默认equals()是比较对象的地址，所以这里new的对象与当前集合比较的是地址，因此为False
            Person p = new Person("Unix",123);
            arr1.add(p);
           System.out.println(arr1);//[123, W, Person{name='Unix', age=123}, true, Person{name='w', age=22}] 
            System.out.println(arr1.contains(p));//true 地址值相同
            //containsAll(Collection coll):判断参数里对象的值是否全部与当前对象相同
            Collection arr2 = Arrays.asList(123,"W");//Arrays的方法：返回一个带参的Collection对象
            System.out.println(arr1.containsAll(arr2));//true 传入的W是String类型，equals被系统重写过的,因此为true
            Collection arr3 = Arrays.asList(123,"W",new Person("Unix", 123));
            System.out.println(arr1.containsAll(arr3));//false 自定义类equals没有重写，如若要结果为true，自定义类重写equals即可
        }
    }
```

```java
	//@Test
		class Person{
         private String name;
   		 private int age;
        ..........
        //省略get/set方法和toString
        //省略重写equals方法
    }
	public void test2(){
        Collection coll = new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new String("Tom"));
        coll.add(false);
        //remove(Object obj)：从当前集合中移除obj元素
        coll.remove(1234);//f返回false
         System.out.println(coll);//[123,456,Person{name='Jerry', age=20},Tom,false]
        coll.remove(123);
        System.out.println(coll);//[456,Person{name='Jerry', age=20},Tom,false]
        
        //removeAll(Collection coll)：从当前集合移除coll中的所有交集元素
        Collection coll1 = Arrays.asList(123,4567);
        coll.removeAll(coll1);//[456,Person{name='Jerry', age=20},Tom,false]
        Collection coll2 = Arrays.asList(123,456,false);
        coll.removeAll(coll2);//[Person{name='Jerry', age=20},Tom]
        
        //retainAll(Collection coll)：获取当前集合和 coll 集合之间的交集并返回给当前交集
        Collection coll3 = new ArrayList();
        coll3.add(123);
        coll3.add(456);
        coll3.add(new Person("Jerry",20));
        coll3.add(new String("Tom"));
        coll3.add(false);
        Collection coll4 = Arrays.asList(123,456,789);
        coll3.retainAll(coll4);
        System.out.println(coll3);//[123,456]
        
        //equals(Object obj):要返回true，需要当前集合与参数元素都相同，注意：本 List 是有序的，当参数与当前元素相同而位置不同时会判定为假，即返回false
         Collection coll5 = new ArrayList();
        coll5.add(123);
        coll5.add(456);
        coll5.add(new Person("Jerry",20));
        coll5.add(new String("Tom"));
        coll5.add(false);
        System.out.println(coll3.equals(coll5));//true 
}
```

```java
	@Test
	public void test3(){
        Collection coll = new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new String("Tom"));
        coll.add(false);
        //hashCode()：返回当前对象的哈希值
        System.out.println(coll.hashCode());//-1200490100
        
        //集合 -----→ 数组：toArray()
        Object[] arr = coll.toArray();
        for(int i = 0;i < coll.length;i ++){
            System.out.print(arr[i]+" ");//123 456 Person{name='Jerry', age=20} Tom false
        } 
            
            //数组 -----→ 集合:调用Arrays类的静态方法asList()
           List<String>  list = Arrays.asList(new String[]{"AA,BB,CC"});
       		
            List arr1 = Arrays.asList(new int[]{123,456});
            System.out.println(arr);//[I@22927a81]如果参数是基本类型数组，则会被默认为一个元素，即集合里放入一个数组元素，此时打印的是地址值，
            List list = Arrays.asList(new boolean[]{true,false});
             System.out.println(list);//[[Z@330bedb4]
            System.out.println(arr.size());//1，由基本数据类型构成的数组视为为一个元素
            List arr1 = Arrays.asList(new Integer[]{123,456});
            System.out.println(arr);//[123,456]当由引用数据类型构成数组时，视为多个元素的集合
            System.out.println(arr.size());//2
    } 
```

![image-20220320223619329](../picture/image-20220320223619329.png)

![image-20220320223659876](../picture/image-20220320223659876.png)

```java
            //1.集合遍历操作，使用迭代器 Iterator 接口
            //2.内部方法：hasNext() 和 next()
		   //3.集合对象每次调用iterator()方法都得到一个全新的迭代器对象，默认游标都在集合的第一个元素之前
		//4.内部定义了remove(),可以在遍历的时候，删除集合中的元素，此方法不同于集合直接调用remove().这里是iterator的remove()
			
            @Test
            public void test(){
                Collection coll = new ArrayList();
                coll.add(123);
                coll.add(456);
                coll.add(new Person("Jerry",20));
                coll.add(new String("Tom"));
                coll.add(false);
        
        //先改造集合的 Iterator 对象
        Iterator iterator = coll.iterator();
        
        //方式一：打印coll.size()次的println
        System.ou.println(iterator.next());
        System.ou.println(iterator.next());
        System.ou.println(iterator.next());
        System.ou.println(iterator.next());
        System.ou.println(iterator.next());
        System.ou.println(iterator.next());
        //指针超过界限将报NoSuchElementException
        System.ou.println(iterator.next());
        
        //方式二：for循环输出 不推荐
        for(int i = 0;i < coll.size();i ++){
            System.ou.println(iterator.next());
        }
        
        //方式三：使用内置函数遍历
        	while(iterator.hasNext()){//判断游标下一位元素是否存在，指针一开始是在第一个元素的前趋
                System.ou.println(iterator.next());
            }
        	
        	//Iterator.remove()：删除游标所指向的集合元素
                //删除集合的TOM
                Iterator iterator1 = coll.iterator();
                while(iterator1.hasNext()){
                    Object obj = iterator1.next();
                    if(("Tom").equals(obj){
                        iterator1.remove();
                    }
                }
               //当要遍历移除tom后的集合，应该重新构造一个iterator对象，因为上面删除使用的iterator对象游标已经指向了被删除元素的位置，无法重置到第一个元素的开头
                       iterator1 = coll.iterator();
                       while(iterator1.hasNext()){
                           System.ou.println(iterator1.next());
                       }
        }
```

![image-20220320233021027](../picture/image-20220320233021027.png)
