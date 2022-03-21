# main()方法使用说明

1. main()方法作为*<font color='#00FF7F'>程序入口</font>*
2. main()方法也是一个普通的静态方法
3. main()方法作为与控制台的交互( 另一种常用方法是：Scanner )

```java
public class MainTest{
		public static void mian(String[] args){
				Main.main(new String[100]);//执行的时候会提示让您选择程序入口，MainTest 和 Main 二选一
		}
class Main{
    public static void mian(String[] args){
				for(int i = 0;i < args.lenght;i++){
                    args[i] = "args_" + i;
                    System.out.println(args[i]);
                }
		}
	} 
}
```

## （String[] args）

这个形参可以实现和控制台交互

1点击下图之后等待一下，让其编译一个class文件

![image-20211108113600101](D:\公式教程1\Typora\picture\image-20211108113600101.png)

2![image-20211108114043895](D:\公式教程1\Typora\picture\image-20211108114043895.png)

3 左边选中当前类名，在右图的框中输入参数，引号可加可不加![image-20211108114130858](D:\公式教程1\Typora\picture\image-20211108114130858.png)

4效果![image-20211108114158209](D:\公式教程1\Typora\picture\image-20211108114158209.png)

#  代码块

## 作用：

初始化类、对象

### 只能使用 static 修饰

```java
static String desc = "我是一个人";
int id;
//静态代码块 (如果一个类中定义了多个静态代码块，随着声明顺序先后执行)
static{
    desc = "我是一个爱学习的人";//可以重新覆盖 static 所声明的值
    System.out.println("hello,static block-1");//会随着类的加载而执行，只执行一次
}
static{
    System.out.println("hello,static block-2");//顺序在后，后执行
}
//非静态代码块(多个非静态代码块一样按先后声明顺序执行，若只赋值属性一般直接写在一个代码块中)
{
    id = 1;//可以在创建对象时给对象属性赋值赋值
    System.out.println("hello,block");//随着对象的创建而执行，每造一个对象就自动调用一次，代码块优先于构造器执行
}
```

```Java
//加载顺序
class Father{
    static{
       System.out.println("第一个执行");
    }
    {
       System.out.println("第三个执行");
    }
}    
class Son extends Father{
    	static{
           System.out.println("第二个执行");
        }
    	{
           System.out.println("第四个执行");
    	}
    	public son(){
            super();
            System.out.println("第五个执行");
        }
	}   
    public void SonText{
        public void main(String[] args){
            System.out.println("第一个执行");
        }
    }

```



# 对属性可以赋值的位置

1. 默认初始化
2. 显式初始化
3. 构造器初始化
4. 有了对象后，通过 “对象**<font color='#FF0000'>.</font>**属性” 或 “ 对象**<font color='#FF0000'>.</font>**方法” 的方式，进行赋值
5. 代码块赋值