# 包装类

如果把基本类型包装成类，那么就可以将变量放入Object里被接受了，此时变量成为一个对象，但仍代表一个变量

<img src="D:\公式教程1\Typora\picture\image-20211111205311379.png" alt="image-20211111205311379" style="zoom:200%;" />

ctrl+t 查看类的继承结构

 ![image-20211111202828757](D:\公式教程1\Typora\picture\image-20211111202828757.png)   

```Java
public class WrapperTest{
    @Test
    int num1 = 10;
    Integer in1 = new Integer(num1);
    System.out.println(in1.toString());//10
    Integer in2 = new Integer("123");
    System.out.println(in2.toString());//123
    Integer in2 = new Integer("123abc");
    System.out.println(in3.toString());//报异常，类型转换失败
    
    Float f1 = new Float(12.3f);
    System.out.println(f1);//12.3
    Float f2 = new Float("12.3");
    System.out.println(f2);//12.3
    
    Boolean b1 = new Boolean(true);
    System.out.println(b1);//true
    Boolean b2 = new Boolean("TrUe");
    System.out.println(b2);//true 这里Boolean包装类对toString有优化，忽略大小写，只要只有4个顺序字母是true即判断为true，否则全部判断为false
    Boolean b3 = new Boolean("true123");
    System.out.println(b2);//false
	
    Order order = new Order();
    System.out.println(Order.isMeal);//false 调用类的属性，属性名是isMeal，没有设值，基本数据类型 boolean d的默认值是 false
    System.out.println(Order.isFemale);//null 调用Order类的对象的包装类，包装类属于类，是引用数据类型，默认值是null
    //引用数据类型：类，接口，数组
}   
   class Order{
    boolean isMeal; 
    Boolean isFemale;   
   }
    
```

## 包装类转换为基本数据类型

```Java
public void test2{
    //包装类-->基本数据类型：调用包装类Xxx的xxxValue()
    @Test
    Integer in1 = new Integer(12);
    int i1 = in1.intValue();
    System.out.println(i1);//12
    
    Float f1 = new Float(12.3);
    float f2 = f1.floatValue();
    System.out.println(f2);//12.3
}
```

## jdk 5.0 新特性 【自动装箱与自动拆箱】

```Java
public void test3{
    //省去新建对象操作，直接将包装类和基本数据类型互相赋值
    //自动装箱
    int num1 = 10;
    Integer num2 = num1;
    
    boolean b1 = true;
    Boolean b2 = b1;
    
    //自动拆箱
    System.out.println(num2.toString());//10
    int num3 = num2;
}
```

## 包装类和 String 的相互转换

![image-20211112001557647](D:\公式教程1\Typora\picture\image-20211112001557647.png)

### 基本数据类型、包装类 ---> String 类型，调用ValueOf(Xxx xxx)

```java
public void test1{
    @Test
    //方式一:连接运算(基本数据类型可用)
    int i = 123;
    String str1 = i + "";
    System.out.println(str1);//字符串：123
    float j = 12.3;
    String str2 = j + "";
    System.out.println(str2);//字符串：12.3
    //方式二:调用包装类 String 的 valueOf(Xxx xxx),适用基本数据类型和其它包装类(除String本身)
    float f1 = 12.3f;
    String str3 = String.valueOf(f1);
    System.out.println(str3);//字符串：12.3
    Double d = new Double(12.4); 
    String str3 = String.valueOf(d);
    System.out.println(str3);//字符串：12.4
}
```

### String 类型--->基本数据类型、包装类，调用包装类的 parsXxx()

```java
public void test2{
    @Test
    	String str1 = "123";
    /*	错误的情况：
    *	int num1 = (int)str1;
    *	Integer in1 = (Integer)str1;  
    *	强转的前提需要两边的类有继承关系
    */
    	//当String变量带有非数字符时，会报 NumberFormatException
    	Integer num1 = Integer.parseInt(str1);//转化为包装类 Integer
    	System.out.println(num1);//int类型：123 包装类对象num1，println方法会自动调用toString(Object obj)方法，println方法系统已重写过toString();
    	int num2 = Integer.parseInt(str1);//转化为int
    	System.out.println(num2);//int类型：123
    	Float num3 = Float.parseFloat(str1);//转化为包装类 Float
    	System.out.println(num3);//float类型：123.0 包装类对象num1，println方法会自动调用toString(Object obj)方法，println方法系统已重写过toString();
    	
    	String str2 = "true1";
    	Boolean b1 = Boolean.parseBoolean(str2);//转化为包装类 Boolean
    	System.out.println(b1);//flase 只要字符串不是true【忽略大小写】全部返回false 
}
```

# String 常用方法

![image-20220228233400975](D:\公式教程1\Typora\picture\image-20220228233400975.png)

```java
	@Test
	String s1 = "HelloWorld";
	System.out.println(s1.length());// 10 返回字符串长度
	System.out.println(s1.charAt(0));// H 返回某索引处的字符
	System.out.println(s1.isEmpty());//false 判断是否为空字符串
	System.out.println(s1.toLowerCase());//helloworld，将String中所有字符转换为小写
	System.out.println(s1.toUpperCase());//HELLOWORLD将String中所有字符转换为小写
	String s3 = String s2 = " H e l l o ";
	System.out.println(s2.trim());// h e l l o 由于不可变性,s2没有变
	System.out.println(s3.trim());//h e l l o忽略前导空白和尾部空白，中间的空白保留
	String a1 = "HelloWorld";
	String a2 = "helloworld";
	System.out.println(a1.equals(a2))//false 比较两字符串是否相同
    System.out.println(s2.equalsIgnoreCase(a2));//true 忽略大小写然后比较两字符串是否相同
	String b1 = "abc";
	String b2 = b1.concat("def");
	System.out.println(b2);//abcdef 将指定字符串拼接到此字符串末尾，相当于+
	String s5 = "abc";
	String s6 = new String("abe");
	System.out.println(s5.compareTo(s6));//-2 涉及字符串排序 从第一个位置开始比较两个字符串的ASCII码的大小并相减,结果为正，说明前者比后者大
	String s7 = "北京尚硅谷教育";
	String s8 = s7.subString(2);//返回一个新字符串，从指定位置的beginIndex开始取值
	System.out.println(s7);//北京尚硅谷教育
	System.out.println(s8);//尚硅谷教育
	String s9 = s7.subString(2，5);//返回一个新字符串，从指定位置的beginIndex开始取值，到endIndex结束，不包括最后一个索引
	System.out.println(s8);//尚硅谷
```

 ![image-20220228233423144](D:\公式教程1\Typora\picture\image-20220228233423144.png)

```java
	 @Test
	String str1 = "helloworld";
	boolean b1 = str1.endsWith("rld");//测试此字符是否以指定的后缀结束
	System.out.println(b1);//true
	boolean b2 = str1.startsWith("He");//测试此字符是否以指定的前缀开始
	System.out.println(b2);//false
	boolean b3 = str1.startsWith("ll"，2);//测试此字符从指定索引开始的字符串是否为指定的前缀开始
	System.out.println(b3);//true
	String str2 = "wor";
	System.out.println(str1.contains(str2));//true d当且仅当此字符包含指定的 char 值序列时，返回true
	System.out.println(str1.indexOf("lo"));//3 返回指定子字符串在此字符中第一次出现处的索引
	System.out.println(str1.indexOf("lol"));//-1 若找不到首次出现指定字符的索引则返回-1
	System.out.println(str1.indexOf("lo",5));//-1从指定的索引开始，返回指定子字符串在此字符中第一次出现处的索引，若找不到返回-1
	String str3 = "lilolilo"
	 System.out.println(str3.lastindexOf("li"));//5，返回此指定字符串中最右边出现处的索引，从右往左看,li第一次出现的索引为5
	System.out.println(str3.lastindexOf("lo",4));//0，从第5索引开始从右往左匹配，li第一次出现的索引为0
```

![image-20220228233442443](D:\公式教程1\Typora\picture\image-20220228233442443.png)

```java
	@Test
	String str1 = "北京尚硅谷教育";
	String str2 = str1.replace('北'，"东");// 返回一个新字符串，它是通过 newChar 替换此字符中出现的所有 oldChar 得到的
	System.out.println(str2);//东京尚硅谷教育
	
	//把前字符串的数字替换成逗号，如果结果中开头和结尾有逗号的话去掉
	String str = "12hello34world5java678mysql9";
	String string = str.replaceAll("\\d+"，",").replaceAll("^&$","");//第一个参数必须为正则匹配
	System.out.println(string);//hello,world,java,masql 
	
	str = "123456"; 
	boolean matches = str.matches("\\d+");//判断字符串是否全部由数字组成
	System.out.println(matches);//true
     System.out.println("123a45".matches("\\+"));//false   
	
	str = "hello|world|java";
	String[] strs = str.split("\\|");
	for(int i = 0; i < strs.length; i++){
        System.out.print(strs[i]+" ");//hello world java
    }
	System.out.println();
	str2 = "hello.world.java";
	String[] strs2 = str2.split("\\.");
	for(int i = 0; i < strs2.length; i++){
		System.out.print(strs2[i] + " ");//hello world java
    }
```

![image-20220228233204236](D:\公式教程1\Typora\picture\image-20220228233204236.png)

![image-20220228233324163](D:\公式教程1\Typora\picture\image-20220228233324163.png)

```java
	 public static void main(String args[]) {
        String str = new String("Welcome-to-Runoob");
 
        System.out.println("- 分隔符返回值 :" );
        for (String retval: str.split("-")){
            System.out.println(retval);
        }
 
        System.out.println("");
        System.out.println("- 分隔符设置分割份数返回值 :" );
        for (String retval: str.split("-", 2)){
            System.out.println(retval);
        }
 
        System.out.println("");
        String str2 = new String("www.runoob.com");
        System.out.println("转义字符返回值 :" );
        for (String retval: str2.split("\\.", 3)){
            System.out.println(retval);
        }
 
        System.out.println("");
        String str3 = new String("acount=? and uu =? or n=?");
        System.out.println("多个分隔符返回值 :" );
        for (String retval: str3.split("and|or")){
            System.out.println(retval);
        }
```

