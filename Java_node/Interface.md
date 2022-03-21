# 接口

## 接口的使用

1. 接口使用 interface 来定义

2. java中，接口和类是并列的两个结构

3. 如何定义接口：定义接口中的成员

   * ​		3.1 JDK7及以前：只能定义全局常量和抽象方法
   * 全局常量：public  static  final （书写时可省略）
   * 抽象方法：public abstract
   * ​         3.2  JDK8：除了定义全局常量和抽象方法之外，还可以定义静态方法、默认方法

4. 接口是<font color='FFA500'>不能定义</font>构造器的，意味着接口<font color='#FF0000'>不可以实例化</font>

5. JAVA开发中，通过让类去实现( <font color='#CD5C5C'>implements</font> )的方式来实现

   * ​	如果实现覆盖了接口中的所有抽象方法，则实现类就可以实例化  //<font color='#00BFFF'>如果子类继承了父类的抽象（abstract）方法，并用 @override 重写了该方法，则称为**实现**！【接口类同理方法覆盖该方法也称为实现】</font>
   * ​     如果实现类没有覆盖接口中所有的抽象方法，则此实现类仍为一个抽象类

6. Java类可以实现多个接口 → 弥补了Java单继承的局限性

   ​	格式：<font color='FFA500'>class</font> A <font color='#00FF7F'>extends</font> B <font color='#FF0000'>implements</font> C ，D ， E……

7. 接口与接口之间可以<font color='#9400D3'>**多继承**</font>

8. 接口具体的体现<font color='#9400D3'>多态性</font>

9. 接口，实际上可以看作是一种规范

```java
		public class InterfaceTest {
           public static void main(String[] args){
               System.out.println(Flyable.MAX_SPEED);
               System.out.println(Flyable.MIN_SPEED);
            Computer com = new Computer();//创建一个实现接口类的对象
               Iphone ip = new Iphone();//接口子类的对象
               com.transferDate(ip);//传参接口子类对象
           }   
        }
		//调用实现接口子类的类
		class Computer {
            public void transferDate(Flyable fyable){//传参的是抽象类的实现类【子类】
                 fyable.fly();
            	 fyable.stop();//调用俩个重写的方法
           }
        }     
		//接口定义
		interface Flyable{
            //全局变量
            public static final int MAX_SPEED = 7900;
             int MIN_SPEED = 1;//系统会自动补全 public static final 
            //抽象方法
            public abstract void fly();
            void stop();//系统自动补全public abstract 
        }
	
	class Iphone implements Flyable{
        @Override
        public void fly(){
            	System.out.println("通过引擎起飞");
        	}
         @Override
         public void stop(){
               System.out.println("驾驶员减速停止");
            }
        }
		
   	abstract class Kite implements Flyable{
        @override
        public void fly(){
            
        }//如果不想实例化而想覆盖其中一个抽象方法，必须加上 abstract 表明仍为一个抽象类
    }
```

```java
	//接口多继承
	class A extends Object implements CC{
        @override
        public void method1(){
            // TODO Auto-generated method stub
        }
         @override
        public void method2(){
            // TODO Auto-generated method stub
        }
    }
	interface AA{
        void method1();
    }
	interface BB{
        void method2();
    }
	interface CC extends AA,BB{
    }
```

# 接口与抽象类的异同：

1. 抽象类只能继承一次，但是可以实现多个接口
2. 接口不能声明构造，抽象类可以有
3. 接口和抽象类必须实现其中所有的方法，抽象类中如果有未实现的抽象方法，那么子类也需要定义为抽象类。抽象类中可以有非抽象的方法
4. 接口中的变量必须用 public static final 修饰，并且需要给出初始值。所以实现类不能重新定义，也不能改变其值。
5. 接口中的方法默认是 public abstract，也只能是这个类型。不能是 static，接口中的方法也不允许子类覆写，抽象类中允许有static 的方法

相同点：

**<font color='#00BFFF'>都可以被继承，都可以写抽象方法</font>**，规定了子类必须要重写的方法（所以不能有抽象构造方法和抽象静态方法）；

　　　　　　为什么不能有抽象构造方法：构造方法是类实例化时的构造过程，而抽象类不能被实例化，两者矛盾，所以不存在抽象构造方法。

　　　　　　为什么不能有抽象静态方法：抽象方法是专用于继承来实现的，而静态方法可以被类及其对象调用，不能被继承，两者矛盾，所以不存在抽象静态方法。

　　**<font color='#00BFFF'>都不能被实例化</font>**，所以不能创建实例对象（由于没有对应的具体概念）；【可以用new 接口(){}的方法来当做匿名类，把方法作为参数来进行传递，注：这不是实例化】

# java中接口和继承的区别

## 实际概念区别：

1. 
   不同的修饰符修饰(interface),(extends)
2. 在面向对象编程中可以有多继承!但是只支持接口的多继承,不支持'继承'的多继承哦
   而继承在java中具有单根性,子类只能继承一个父类
3. 
   在接口中只能定义全局常量,和抽象方法
   而在继承中可以定义属性方法,变量,常量等...
4. 某个接口被类实现时,在类中一定要实现接口中的抽象方法
   而继承想调用那个方法就调用那个方法,毫无压力

 

接口是：对功能的描述      继承是：什么是一种什么【西瓜 (子类) 是一种水果（父类）】

始终记住：你可以有多个干爹（接口），但只能有一个亲爹（ 继承）

举例：

　　如果狗的主人只是希望狗能爬比较低的树，但是不希望它继承尾巴可以倒挂在树上，像猴子那样可以飞檐走壁，以免主人管不住它。

那么狗的主人肯定不会要一只继承猴子的狗。

　　设计模式更多的强调面向接口。猴子有两个接口，一个是爬树，一个是尾巴倒挂。我现在只需要我的狗爬树，但是不要它尾巴倒挂，那么我只要我的狗实现爬树的接口就行了。同时不会带来像继承猴子来带来的尾巴倒挂的副作用。这就是接口的好处。

### 面试题：抽象类与接口类的异同

不同：

（1）**抽象类可以有构造方法**，接口中不能有构造方法。

（2）抽象类中可以有普通成员变量，接口中没有普通成员变量. 

（3）抽象类中可以包含静态方法，接口中不能包含静态方法. 

（4） 一个类可以实现多个接口，但只能继承一个抽象类。

（5）接口可以被多重实现，抽象类只能被单一继承. 

（6）如果抽象类实现接口，则可以把接口中方法映射到抽象类中作为抽象方法而不必实现，而在抽象类的子类中实现接口中方法.

 接口和抽象类的相同点: **都可以被继承**.