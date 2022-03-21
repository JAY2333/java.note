# 数组概述

## 	1 数组的理解

数组（Array），是多个相同类型数据按一定顺序排列的集合，并使用一个名字命名，且通过编号的方式对这些数据进行统一的管理。

## 	2 数组相关概念

数组名

元素

角标、小标、索引

* 数组本身是<font color='#D2691E'>**引用数据类型**</font>（包括接口、类、数组、枚举、注解、字符串型），而其中的元素可以是任何数据类型
* 创建数组对象会在内存开辟一整块连续的空间
* 数组的长度一旦确定，就不能修改
* 数组是有序排列的
* 数组分类：
  1. ​		按照维数：一维数组、二维数组……
  2. ​        按照数组元素的类型：基本数据类型元素的数组、引用数据类型元素的数组

# 数组的使用

## 1 初始化

```java
public static void main(String[] args){
    //int类型的声明和初始化
    int num;//声明
    num = 10;始化
    int id = 1001;//声明+初始化
    
    //一维数组的声明和初始化
    int[] ids;//声明
    //静态初始化:数组的初始化和元素的赋值操作一起进行
   ids = new int[]{1001,1002,1003,1004};
    //动态初始化：数组的初始化和数组元素赋值操作分开
    String[] names = new String[5];
    
    //调用方式：数组角标(索引)，从0开始，到(数组长度-1)结束
    names[0] = "王贵炳";
    
    //获取数组长度(使用 length 获取)
    System.oout.println(names.length);
    
    //遍历数组
    for(int i = 0;i < names.length;i++){
         System.oout.println(names[i]);
    }
    
    //数组元素的默认初始化值
    1 数组元素是整形：0
    2 数组元素是浮点型：0.0
    3 数组元素是 char 型：0 或 '\u0000'(空字符)，而非'0'
    4 数组元素是 boolean 型：false
    5 数组元素是引用数据类型：null   
}
```

#   多维数组的使用

```java
public static void main(String[] args){
    //二维数组的声明和初始化
    //静态初始化
    int[][] arr1 = new int[][]{{1,2,3},{4,5},{6,7,8}};
    //动态初始化1
    String[][] arr2 = new String[3][2];
    //动态初始化2
    String[][] arr3 = new String[3][];
    //调用
    System.oout.println(arr1);//本数组地址值
    System.oout.println(arr1[0]);//本数组第一维数组的地址值
    System.oout.println(arr1[0][1]);//2
    System.oout.println(arr1[1][2]);//报错，数组溢出，只有两个元素
    System.oout.println(arr2[1][1]);//null
    //获取数组长度
    System.oout.println(arr1.lenght);//3
    System.oout.println(arr1[0].lenght);//3
    System.oout.println(arr1[1].lenght);//2
    //遍历数组 注意第二层for循环 要指定第一维数组的长度的
    		for (int i = 0; i < arr1.length; i++) {
			for (int j = 0; j < arr1[i].length; j++) {
				System.out.println(a[i][j]);				
			}
		}
    //数组是引用类型
    double[][] arr4 = new double[4][];
    System.oout.println(arr4);//地址值
    System.out.println(arr4[0]);//null  多维数组的外层元素初始化为 null
    System.oout.println(arr4[1][0]);//空指针异常 内层元素未定义故报空指针
} 
```

![image-20211028195004393](D:\公式教程1\Typora\picture\image-20211028195004393.png)

##  size() 、length、length()的区别

**length——数组的属性**

**length()——String的方法**

**size()——集合的方法**

```java
	//length不是方法，是属性，数组的属性
	public static void main(String[] args) {
	int[] intArray = {1,2,3};
	System.out.println("这个数组的长度为：" + intArray.length);
}
	//length()是字符串String的一个方法
	public static void main(String[] args) {
	String str = "HelloWorld";
	System.out.println("这个字符串的长度为：" + str.length());
    }
       // 进入length()方法看一下实现
    private final char value[];

    public int length() {
            return value.length;
        }
	//@return     the length of the sequence of characters represented by this object.-----→即由该对象所代表的字符序列的长度，所以归根结底最后要找的还是length这个底层的属性；
	//size()方法，是List集合的一个方法
	public static void main(String[] args) {
	List<String> list = new ArrayList<String>();
	list.add("a");
	list.add("b");
	list.add("c");
	System.out.println("这个list的长度为：" + list.size());
	}
	//在List的方法中，是没有length()方法的；也看一段ArrayList的源码
	
    private final E[] a;

    ArrayList(E[] array) {
           if (array==null)
                 throw new NullPointerException();
           a = array;
    }

    public int size() {
           return a.length;
    }
	//由这段就可以看出list的底层实现其实就是数组，size()方法最后要找的其实还是数组的length属性.另外，除了List，Set和Map也有size()方法，所以准确说size()方法是针对集合而言。
```

