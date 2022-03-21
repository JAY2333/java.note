# JAVA常用类

##  String类

1. String 声明为 finaly 的，不可被继承

2. String 实现了 Serializable 接口：表示字符串是支持<font color='#FF0000'>序列化</font>的，实现 Comparable 接口：表示 String 可以比较大小

3. String 内部定义了 finaly char[] value 用于存储字符串数据

4. String：代表了不可变的字符序列 【不可变的特性】

   体现：

   1. ​	当对字符串重新赋值时，需要重新指定内存区域赋值，不能使用原有的 value 进行赋值
   2. ​    当对现有的字符串进行连接操作时，也需要重新指定内存区域赋值，不能使用原有的 value
   3. 当调用 String 的 replace() 方法修改指定字符或字符串时，也需要重新指定内存区域

5. 通过<font color='FFA500'>字面量</font>(区别于new方式)给一个字符串赋值，此时的字符串值声明在字符串产常量池中

6. 字符串常量池是<font color='#00BFFF'>不会存储相同内容</font>的字符串的

```java
	@Test
	public void test1(){
        String s1 = "abc";
        String s2 = "abc";
        System.out.println(s1 == s2);//true 比较地址值
        s1 = "hello";
        System.out.println(s1);//hello 已在常量池重新定义了一个
        s2 += "def";
        System.out.println(s2);//abcdef 在常量池重新定义了一个
        String s3 = "abc";
        s3.replace('a'，'m');
        System.out.println(s3);//mbc 在常量池重新定义了一个
    }
```

![image-20220226222306081](D:\公式教程1\Typora\picture\image-20220226222306081.png)

 <img src="D:\公式教程1\Typora\picture\image-20220227140041056.png" alt="image-20220227140041056" style="zoom: 150%;" />

![image-20220227140434909](D:\公式教程1\Typora\picture\image-20220227140434909.png)

## 面试题：String s = new String("abc");方式创建对象，在内存创建了几个对象？

#### 两个：

1. 一个是堆空间中new结构
2. 另一个是char[]对于常量池中的数据:"abc"

## 字符串拼接

 

```java
	@Test
	String s1 = "hello";
	String s2 = "world";
	String s = "helloworld";
	String s3 = "hello"+"world";
	String s4 = s1 + "world";
	String s5 = s1 + S2;
	String s6 = (s1+s2).intern();//返回值使用常量池中已存在的"helloworld"
	System.out.println(s3 == s4);//false
	System.out.println(s == s4);//true
	System.out.println(s3 == s5);//false
	System.out.println(s4 == s5);//false
	System.out.println(s3 == s6);//true
	
	String t = "javaEEhadoop";
	final String t1 = "javaEE";//此时的t不再是变量，而是常量
	String t2 = t1 + "hadoop";//所以拼接之后t2由于是常量，于是不是存储在堆里，而是在常量池
	System.out.println(t == t2);//true
```

![image-20220227142338859](D:\公式教程1\Typora\picture\image-20220227142338859.png)

```java
    public class StringTest {

            String str = new String("good");
            char[] a ={'t','e','s','t'};
            public StringTest() {
            }

            public void change(String str,char[] a){
                str = "bad";//由于String的不可变性，这里的str相当于重新new了一个对象
                a[0] = 'W';
                System.out.println("本str："+str.toString());//本str:bad
                System.out.println(this.str == str);//false 这里可以证明构造器加载的str与传进来的str虽然地址一样，但由于String引用类型的不可变性，所以重新new了一个对象因此这里的地址比较不同
            }

        public static void main(String[] args) {
            StringTest stringone = new StringTest();
            stringone.change(stringone.str, stringone.a);
            System.out.println(stringone.str);//good 这里的str仍然是构造器加载的str
            System.out.println(stringone.a);//West
        }
    }
```

## String与byte[]之间的转换

String --> byte[] : 调用String 的 getBytes();

编码String --> byte[]：字符串 --> 字节

解码byte[] --> String ： 字节 --> 字符串

![image-20220301210428580](D:\公式教程1\Typora\picture\image-20220301210428580.png)

![image-20220301210318529](D:\公式教程1\Typora\picture\image-20220301210318529.png)

# StringBuffer

String：<font color='FFA500'>不可变</font>的字符序列，底层使用char[]存储

StringBuffer：<font color='#FFFF00'>可变</font>的字符序列，<font color='#00BFFF'>线程安全</font>的，<font color='#00FF7F'>效率低</font>，底层使用char[]存储

StringBuilder：<font color='#00FF7F'>可变</font>的字符序列，jdk5.0新增的，线程不安全的，<font color='#00FF7F'>效率高</font>，底层使用char[]存储

### 源码分析

```java
	String str = new String();//char[] value = new char[0]
	String str1 = new String("abc");//char[] value = new char[]{'a','b','c'};
	StringBuffer sb1 = new StringBuffer();//char[] value = new char[16] 底层创建了一个长度是16的char数组
	System.out.println(sb1.length());
	sb1.append('a');//value[0] = 'a'
	sb1.append('b');//value[1] = 'b'
	StringBuffer sb2 = new StringBuffer("abc");//char[] value = new char["abc".length()+16]
	//问题1 System.out.println(sb2.length());  长度是3，虽然底层是16+3
	//问题2 扩容问题:如果要添加的数据底层超过16.那就需要扩容底层的数组，默认情况下，扩容为原来的2倍+2，同时将原有数组中的元素复制到新的数组中
	//开发过程中，建议使用：StringBuffer(int capacity) 或 StringBuid(int capacity) 事先指定数组长度，避免后期出现扩容导致效率降低
```

## StringBuffer常用方法

```java
	StringBuffer append();//提供了很多的append()方法，用于字符串拼接
     StringBuffer delete(int start,int end);//删除指定位置的内容，左闭右开
	StringBuffer replace(int start,int end,String str);//把[start,end)位置替换为str
	StringBuffer insert(int offset,xxx);//在指定位置插入xxx
	StringBuffer reverse();//把当前字符序列逆转 
	public int indexOf(String str);//查找一个字符串中，第一次出现指定字符串的位置
	public String substring(int satrt,int end);//返回一个从start开始到end索引结束的左闭右开的子字符串
	public int length();//返回字符串长度
	public char charAt(int n);//返回指定索引处的char字符
	public void setCharAt(int n,char ch);//改变指定索引的字符
     增：append()
     删：delete(int start,int end)
     改：setCharAt(int n,char ch) / replace(int start,int end,String str)
     查：charAt(int n)
     插：insert(int offset,xxx)
     长度：length()
     遍历：toString()    /    for() + charAt()   
        
```

# JDK8之前的日期时间api

## Date

```JAVA
	@Test
	long time = System.currentTimeMillis();
	System.out.println(time);//返回当前时间与1970年1月1日0时0分0秒之间的毫秒单位的时间差，称为时间戳
	
	java.util.Date类
        @Test
     public void test(){
        //构造器一：空参
        Date date1 = new Date();
        System.out.println(date1.toString());//Sat Feb 16 16:35:31 GMT+08:00 2019 显示年月日时分秒
    	System.out.println(date1.getTime());//15503062004104 获取当前Date对象对应的毫秒数
    	//构造器二：创建指定毫秒数的Date对象
		Date date2 = new Date(15503620410L);
        System.out.println(date2.toString);
	
        java.sql.Date :数据库使用的时间api
        java.sql.Date date3 = new java.sql.Date(35235325345L);
        System.out.println(date3);//1971-02-13
        //如何将java.util.Date(父类)对象转换为java.sql.Date对象(子类)
        //情况一：
            Date date4 = new java.sql.Date(2343243242323L);
        java.sql.Date date5 = (java.sql.Date)date4;
        //情况二：
        Date date6 = new Date();
        java.sql.Date date7 = new java.sql.Date(date6.getTime()) ;
        //先将父类Date转换成毫秒数，将此毫秒数放入sql时间类的获得格式年份的方法getTime(),再赋值给sql时间类  
```

## SimpleDateFormat

```java
	//jdk8之前的api
	 @Test
	public void testSimpleDtaeFormat(){
        //创造对象
        SimpleDate sdf = new SimpleDateFormat();
        //格式化：日期 --> 字符串
        Date date = new Date();
        System.out.println(date);
        String format = sdf.format(date);
        System.out.println(format);//19-2-18 上午11:43
        
        //解析：格式化的逆过程 字符串--->日期
        String str = "19-12-18 上午11:43";
        Date date1 = sdf.parse(str);
        System.out.println(date1);//Wed Dec 18 11:43:00 GMT+08:00 2019
    }

	//比较灵活的写法
	SimpleDateFormat sdf1 = new SimpleFormat("yyyy-MM-dd hh:mm:ss");
	//格式化
	String format1 = sdf1.format(date);
	System.out.println(format1);//2022-03-03 20:46:23
	//解析
	Date date2 = sdf1.parse(2019-02-18 11:43:21);//要注意与创建的对象所声明的格式一致,如果识别失败就会抛异常ParseException
	System.out.println(date2);//Wed Dec 18 11:43:00 GMT+08:00 2019
```

算法题

```java
	//获取两个字符串中最大的相同子串
	public class FindMax {
    public String findMax(String str1,String str2){
       if(str1 != null &str2 != null){
           String maxstr = (str1.length() >= str2.length()?str1:str2);
           String minstr = (str1.length() < str2.length()?str1:str2);
           int length = minstr.length();
           for (int i = 0; i < length; i++) {
               for (int x = 0 , y = length - i;y <=length;x++,y++){
                   String str = minstr.substring(x,y);
                   if(str1.contains(str)){
                       return str;
                   }
               }
           }
        }
            return null;
    }

    public static void main(String[] args) {
        FindMax findMax = new FindMax();
        System.out.println(findMax.findMax("aabbccddbcbhellohello", "hello"));
    }
}	
```

## Calender类(抽象类)

```java
	//要注意获取的1月是输出0，以此类推，周日是1...
	@Test
	public void testCalendar(){
        //一,实例化
        //方式1：创建其子类(GregorianCalendar)的对象,不常用
        GregorianCalendar gregorianCalendar = new GregorianCalendar();
        //方式2：调用其静态方法getInstance()
        Calendar calendar = Calendar.getInstance();
        //二:常用方法
        //get()
        System.out.println(calendar.get(Calendar.DAY_OF_MONTH)); 7//获取当天属于该月的第几天
        //getTime():日历类-->Date
            System.out.println(new Calendar.getTime());//获取当天的毫秒数
        //setTime()
         SimpleDateFormat date1 = new SimpleDateFormat("xxxx-mm-dd");
         Date date2 = new date1.prase("2020-01-01");
         System.out.println(new Calendar.setTime(date2.getTime()));//利用simpleDateFormat()对象获取指定天数的日历格式时间     
    }
```

## JDK8中的新日期API

```java
	localDate localDate  = LocalDate.now();//获取年月日
	LocalTime localTime = LocalTime.now();//获取时分秒
	LocalDateTime localDateTime = LocalDateTime.now();//获取年月日时分秒
	System.out.println(localDate);//2022-01-01
	System.out.println(localTime);//15:15:15
	System.out.println(localDateTime);//2022-01-01T15:15:15.435
	
	//of():设置指定的年月日时分秒，不会有时分秒
	LocalDtaeTime localDateTime localDateTime1 = LocalDateTime.of(2020,10,6,13,23,43);
	System.out.println(locatDateTime);//2020-10-06T13:23:43

	//getXxx()
	System.out.println(locatDateTime.getDayOfMouth());//18,获取当前时间属于当月的第几天
	System.out.println(localDateTime.getDayOfWeek());//MONDAY,获取当天属于星期几
	System.out.println(locatDateTime().getMouth);//FEBRUARY，获取当天属于第几月，英语
	System.out.println(locatDateTime.getMouthValue());//2，获取当天属于第几月，阿拉伯数字
	System.out.println(locatDateTime.getMiunte);//18，获取当前时间的分钟
	
	//体现不可变性
	//withXxx():设置相关的属性
	LocalDate localDate1 = localDate.withDayOfMouth(22);//改变月的号数
	System.out.println(localDate);2022-05-18//当前是18号
	System.out.println(localDate1);//改成了22号，当localDate的值仍然不变，而是赋值给localDate1
	LocalDateTime localDateTime1 = localDate.withDayOfHour(4);//改变时针
	System.out.println(localDateTime);2022-05-18T15:22:00.114//当前是15:22
	System.out.println(localDate1);2022-05-18T04:22:00.114//改成了04:22，当localDateTime的值仍然不变，而是赋值给localDateTime2
        LocalDateTime localDateTime3 = localDateTime.plusMouths(3);//将当前时间加了3个月
		System.out.println(localDateTime);2022-02-18T15:22:00.114//当前是2022-02-18
		System.out.println(localDateTime3);2022-05-18T15:22:00.114//将当前时间改为了2022-05-18
	LocalDateTime localDateTime4 = localDateTime.minusDays(6);
	  System.out.println(localDateTime);2022-02-18T15:22:00.114//当前是2022-02-18
        System.out.println(localDateTime4);2022-02-12T15:22:00.114//当前是2022-02-12
```

## 瞬时 Instant

   

```java
	@Test
	public void test(){
        //now():获取本初子午线对应的标准时间
        Instant instant = Instan.now();
        System.out.println(instant);//2019-02-18T07:29:41.7192
        //添加数时间的偏移量,中国的东八区，故加8
        OffsetDtaeTime offsetDateTime = instant.atOffset(ZoneOffset.ofHours(8));
        System.out.println(offsetDateTime);//2019-02-18T15:32:50.611+08:00
        //toEpochMilli():获取自1970年1月1日0时0分0秒(UTC)开始的毫秒数 ---> Date类的getTime()
        long milli = instant.toEpochMilli();
        System.out.println(milli);//1550475314878L
        //ofEpochMilli():通过给定的毫秒数，获取Instant实例 -->Date(long millis)
        Instant instant1 = Instant.ofEpochMilli(1550475314878L);
        Ssytem.out.println(instant1);//2019-02-18T07:35:14.8782
    }
```

## DateTImeFormatter类

```java
	@Test
	public void test{
    	//自定义格式，如：ofPattern("yyyy-mm-dd hh:mm:ss")
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-mm-dd hh:mm:ss");//定义格式
        //格式化
        String str = formatter.format(LocalDateTime.now());
        System.out.println(str);//2019-02-18 03:53:10
        //解析
        TemporalAccessor accessor = formatter.parse("201902-18 03:52:09");
        System.out.println(accessor);//{NanoOfSecond=0,MicroOfSecond=0,HourOfAmp=3,MinuteOfHour=52,MilliofSecond=0,SecondOfMinute=9},ISO resolved to 2019-02-18
	}
```

## JAVA比较器

 说明：Java中的对象，正常的情况下，只能进行比较 :== 或 != 。<font color='#FF0000'>不能</font>使用 > 或 < 的，但在开发场景中，我们需要对多个对象进行排序，言外之意，就需要比较对象的大小。如何实现?使用两个接口中的任何一个：Comparable 或 Comparator

### Comparable 接口的使用

1. 像String、包装类等实现了Comparable接口，重写了compareTo()方法，给出了两个比较对象大小的方式
2. 像 String 、包装类重写 compareTo( )方法以后，进行了从小到大的排序
3. 重写 compareTo(obj) 的规则
   1. 如果当前对象 this <font color='#FF0000'>大于</font>形参obj，则返回<font color='#FF0000'>正整数</font>
   2. 如果当前对象 this <font color='#FFFF00'>小于</font>形参对象 obj ，则返回<font color='#FFFF00'>负整数</font>
   3. 如果当前对象 this <font color='#00BFFF'>等于</font>形参对象 obj ，则返回 <font color='#00BFFF'>0</font>

```java
	public class CompareTest{
		@Test
        public void test1(){
            String[] arr = new Sring[]{"AA","CC","KK","MM","GG","JJ","DD"};
            Arrays.sort(arr);
            System.out.println(Arrays.toString(arr));//AA CC DD GG JJ KK MM
        }
	}
```

### 对于自定义类来说，如果如果需要排序，我们可以让自定义类<font color='#FFFF00'>实现</font>  <font color='#00CED1'>comparable</font>  <font color='#FFFF00'>接口</font>，在comparseTo(obj) 方法中指明排序方法

```java
	实体类
        package gk;
    import org.junit.Test;
    import java.util.Arrays;

    public class Goods implements Comparable {
        private double price;
        private String name;

        public Goods() {
        }

        public Goods(String name, double price) {
            this.price = price;
            this.name = name;
        }

        public double getPrice() {
            return price;
        }

        public void setPrice(double price) {
            this.price = price;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        @Override
        public String toString() {
            return "Goods{" +
                    "price=" + price +
                    ", name='" + name + '\'' +
                    '}';
        }
		//自然排序，从小到大
        @Override
        public int compareTo(Object o) {
            if (o instanceof Goods) {
                Goods goods = (Goods) o;
    //            方式一：指明商品价格从高到低排序，返回正交换，返回负数不变
                if (this.price > goods.price) {
                    return 1;
                } else if (this.price < goods.price) {
                    return -1;
                } else
                    //当价格一样时，按名称排序
                    return this.name.compareTo(goods.name);
    //            方式二：
    //            return Double.compare(this.price,goods.price);
            }
            throw new RuntimeException("传入的数据类型不一致");
        }
    }
```

```java
        package gk;
    import org.junit.Test;
    import java.util.Arrays;

    public class test {
        @Test
        public void test1(){
            Goods[] arr = new Goods[4];
            arr[0] = new Goods("lenovo",2019);
            arr[1] = new Goods("huawei",2022);
            arr[2] = new Goods("xiaomi",2015);
            arr[3] = new Goods("apple",2022);
            Arrays.sort(arr);
            System.out.println(Arrays.toString(arr));//[Goods{price=2015.0, name='xiaomi'}, Goods{price=2019.0, name='lenovo'}, Goods{price=2022.0, name='apple'}, Goods{price=2022.0, name='huawei'}]
        }
    }

```

### compare() 自定义排序

1. 建立一个 <font color='#FF0000'>comparator </font>的子类对象(可匿名)
2. 重写该子类的 <font color='FFA500'>compare()</font> 方法

```java
	 @Test
    public void test2(){
       String[] arr = new String[]{"NN","WW","TT","EE","AA","SS"};
       Arrays.sort(arr, new Comparator() {
           @Override
           public int compare(Object o1, Object o2) {
               //从高到低排序
               if(o1 instanceof String && o2 instanceof String){
                   String s1 = (String) o1;
                   String s2 = (String) o2;
                   return -s1.compareTo(s2);//加了负数，按从高到低排序
               }
               throw new RuntimeException("数据类型不一致");
           }
       });
        System.out.println(Arrays.toString(arr));
    }//[WW, TT, SS, NN, EE, AA]
```

```java
	 @Test
    public void test3(){
        Goods[] arr = new Goods[5];
        arr[0] = new Goods("lenovo",2019);
        arr[1] = new Goods("huawei",2022);
        arr[2] = new Goods("xiaomi",2015);
        arr[3] = new Goods("apple",2022);
        arr[4] = new Goods("lenovo",2000);
        Arrays.sort(arr, new Comparator(){
            @Override
            public int compare(Object o1, Object o2) {
                //先从名称大到小排，再从价格小到大排
                if(o1 instanceof Goods && o2 instanceof Goods){
                        Goods g1 = (Goods) o1;
                        Goods g2 = (Goods) o2;
                    if(g1.getName().equals(g2.getName())){
                        return Double.compare(g1.getPrice(),g2.getPrice());
                    }else {
                        return -g1.getName().compareTo(g2.getName());
                    }
                }
                throw new RuntimeException("数据类型不一致");
            }
        });
        System.out.println(Arrays.toString(arr));
    }//[Goods{price=2015.0, name='xiaomi'}, 
	 //Goods{price=2000.0, name='lenovo'}, 
	 //Goods{price=2019.0, name='lenovo'}, 
	//Goods{price=2022.0, name='huawei'}, 
	//Goods{price=2022.0, name='apple'}]
```

Comparable 接口与 Comparator 的使用对比：

1. Comparable 接口的方式一旦确定，保证 Comparable 接口实现类的对象在任何位置都可以比较大小。
2. Comparator 接口属于临时性的比较。
