#    Static

## 实现某些特定的数据在内存空间只有一份

### static(静态的)关键字的使用

- #### 用来修饰：属性、方法、代码块、内部类

  1. ​	使用static修饰属性：静态变量
  		 按是否使用static修饰分为：静态属性 VS 非静态属性（实例变量）
  	​	 实例变量：我们创建了类的多个对象，每一个对象都独立地拥有一套类中地非静态属性，当修改其中一个对象的非静态属性时，不会导致其他对象中同样的属性值的修改。
  	​	 静态变量：我们创建了类的多个对象，多个对象共享同一个静态变量，当通过某一个对象修改静态变量时，会导致其他对象调用此静态时，是修改过了的。  
  	
  	```java
      
		  	public class StaticTest{
	        public static void main(String[] args){
		Chinese.nation = "中国";//由于该属性已随着类加载而加载，故可调用 
	      Chinese.show();//静态方法调用      
	            Chinese c1 = new Chinese();
	            c1.name = "姚明";
	            c1.age = 40;
	            Chinese c2 = new Chinese();
	            c2.name = "马龙"；
	            c2.age = 30;
	          c1.nation = "CHN";//此时syso输出,调用C2.nation是CHN
	          c2.nation = "China";  //此时syso输出，调用c1.nation是China
	        }
	    }
		class Chinese{
	        String name;
	        int age;
	       static String nation;   
	       public static void show(){    
	           System.out.printf("我是一个中国人");
	    	   System.out.printf(Chinese.nation);//静态方法可加载调用静态属性
	       }//静态方法
	    }
	
  2. static 修改属性的其它说明：
  
      ​		静态变量随着类的加载而加载。可以通过“类.静态变量”的方式进行调用
  
      ​		静态变量的加载早于对象的创建
  
      ​	    由于类只会加载一次，则静态变量在内存中也只会存在一份：存在方法区的静态域中 
  
  ![image-20210505171436820](D:\公式教程1\Typora\picture\image-20210505171436820.png)
  
- 静态方法

  1. ​	随着类加载而加载，只能调用静态的方法或属性
  2. ​    非静态方法中，既可以调用非静态的方法和属性，也可以调用静态的方法和属性，也可以调用静态的方法或属性  

  static注意点：

  1. ​	在静态的方法内，不能使用**this、super**关键字
  2. ​    关于静态属性和静态方法的使用，要从生命周期的角度去理解

-   如何确定一个属性是否要声明static？

  - ##### 属性是可以被多个对象所共享的，不会随着对象的不同而不同

- 如何确定一个方法是否要声明static？

  1. 操作静态属性的方法，通常声明为static的
  2. 工具类的方法中，习惯上声明为static的。比如：Math 、Arrays 、Collections

外部类不能使用static的原因：

static常用的两个作用，一个是作用域限制，一个是生存期限制。
对函数来说：
作用域限制：被static修饰的函数，只能用于代码本身文件的调用。
生存期限制：对函数来说，这条是用来说类的静态成员函数的。在类对象出生前，类的静态成员函数就活着了。

如果类外定义函数时在函数名前加了static，因为作用域的限制，就只能在当前 cpp 里用，
类本来就是为了给程序里各种地方用的，其他地方使用类是包含类的头文件，而无法包含类的源文件。
这样就导致无法在其他地方调用这个静态的类成员函数。如果要解决这个办法，就是在头文件中加extern。
然而extern和static是一对儿对立的关键字，不能用在一起。

所以在类外实现类成员函数时，函数名前加个static修饰符就报错了。

# 单例（Singleton）设计模式

<img src="D:\公式教程1\Typora\picture\image-20211031003332148.png" alt="image-20211031003332148" style="zoom:150%;" />

