#  **scanner**

## 使用步骤：

1. 导包 import  java.util.Scanner;
2. Scanner 的实例化
   - Scanner scan = new Scanner(System.in);
3. 调用Scanner类的相关方法来获取指定类型的变量
   - <font color='red'>int </font>num = scan.nextInt();
   - <font color='red'>boolean</font>  scan = scan.nextBoolean();//布尔类型
4. 如果输入数据类型与定义的不同会抛出异常：<font color='orange'>***InputMisMatchException***</font>

```java
	public class Text {
	public static void main(String []args) {
		Scanner input = new Scanner(System.in);
		System.out.println("请输入一个字符串(中间能加空格或符号)");
	String a= input.nextLine();
		
        System.out.println("请输入一个字符串(中间不能加空格或符)号));
	   String b = input.next();
		
                           			System.out.println("请输入一个整数");
		int c;
		c = input.nextInt();
		
                           			System.out.println("请输入一个double类型的小数");
		double d = input.nextDouble();
		
                           			System.out.println("请输入一个float类型的小数");
		float f = input.nextFloat();          
                           			System.out.println("按顺序输出abcdf的值：");       				System.out.println(a);
		System.out.println(b);
		System.out.println(c);
		System.out.println(d);
		System.out.println(f);
	}
}
```

```java
            请输入一个字符串(中间能加空格或符号)
            我爱祖国！
            请输入一个字符串(中间不能加空格或符号)
            ILoveChina
            请输入一个整数
            520
            请输入一个double类型的小数
            12.26e3
            请输入一个float类型的
            3.1415926
                
            按顺序输出abcdf的值：
            我爱祖国！
            ILoveChina
            520
            12260.0
            3.1415925
```

