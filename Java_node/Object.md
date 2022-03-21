# Object类的使用

1. java.lang.object类
2. 如果在类中声明未使用 extends 关键字指明其父类，则默认父类为 java.lang.object

**Object类方法**

Object是所有类的父类，任何类都默认继承Object。Object类到底实现了哪些方法？

**（1）clone方法**

保护方法，实现对象的浅复制，只有实现了Cloneable接口才可以调用该方法，否则抛出CloneNotSupportedException异常。

**（2）getClass方法**

final方法，获得运行时类型。

**（3）toString方法**

该方法用得比较多，一般子类都有覆盖。

**（4）finalize方法**

该方法用于释放资源。因为无法确定该方法什么时候被调用，很少使用。

**（5）equals方法**

该方法是非常重要的一个方法。一般equals和==是不一样的，但是在Object中两者是一样的。子类一般都要重写这个方法。

**（6）hashCode方法**

该方法用于哈希查找，重写了equals方法一般都要重写hashCode方法。这个方法在一些具有哈希功能的Collection中用到。

一般必须满足obj1.equals(obj2)==true。可以推出obj1.hash- Code()==obj2.hashCode()，但是hashCode相等不一定就满足equals。不过为了提高效率，应该尽量使上面两个条件接近等价。

**（7）wait方法**

wait方法就是使当前线程等待该对象的锁，当前线程必须是该对象的拥有者，也就是具有该对象的锁。wait()方法一直等待，直到获得锁或者被中断。wait(long timeout)设定一个超时间隔，如果在规定时间内没有获得锁就返回。

调用该方法后当前线程进入睡眠状态，直到以下事件发生。

（1）其他线程调用了该对象的notify方法。

（2）其他线程调用了该对象的notifyAll方法。

（3）其他线程调用了interrupt中断该线程。

（4）时间间隔到了。

此时该线程就可以被调度了，如果是被中断的话就抛出一个InterruptedException异常。

**（8）notify方法**

该方法唤醒在该对象上等待的某个线程。

**（9）notifyAll方法**

该方法唤醒在该对象上等待的所有线程。

#  Equals()

1. 是一个方法，而非运算符

2. 只适用于引用数据类型

3. 像 <font color='#FF0000'>String</font>、<font color='#FF0000'>Data</font>、<font color='#FF0000'>File</font>、<font color='#FF0000'>包装类</font>都重写了 Object 类中的 equals() 方法，重写以后，比较的不再是两个引用数据类型的地址值是否相同，<font color='FFA500'>而是比较两个对象的"实体内容"是否相同</font>

4. 通常情况下，<font color='#FFFF00'>自定义的类</font>，如果使用 equals() 的话，也通常是比较两个实体“内容”是否相同，那么我们就<font color='#00CED1'>必须</font>对 equals() 进行<font color='#00FF7F'>***重写***</font>，重写以后比较的<font color='#9400D3'>不再是地址值</font>，而是实体内容。快捷键如下图

5. ![image-20211108220801592](D:\公式教程1\Typora\picture\image-20211108220801592.png)

6. Object 类中的 equals() 的定义：

   ```Java
   public boolean equals(Object obj){
       return (this == obj)
   }//说明:object类中定义的 equals() 和 == 的作用是相同的，比较两个对象的地址值是否相同,即两个引用是否指向同一个对象实体
   Costomer cust1 = new Costomer("Tom",21);
   Costomer cust2 = new Costomer("Tom",21);
   System.out.println( cust1 == cust2 );//false
   String str1 = new String("wang");
   String str2 = new String("wang");
   System.out.println( str1 == str2 );//true
   ```

   ![image-20211108213653046](D:\公式教程1\Typora\picture\image-20211108213653046.png)

## ![image-20210505013839534](D:\公式教程1\Typora\picture\image-20210505013839534.png)

## == :

1. 可以使用在基本数据类型变量和引用数据类型变量中

2. 如果比较的是基本数据类型变量：比较两个变量保存的数据是否相等（不一定类型要相同）【但是比较的时候两边必须都是相同的变量类型，要么都是引用数据类型，要么都是基本数据类型】

   ```java
   char i = 'A';//ASCII码对应65
   int j = 65;
   System.out.println( i == j );//true
   ```

3. 如果比较的是引用数据类型变量：比较两个对象的<font color='FFA500'>地址值</font>是否相同,即两个引用是否指向同一个对象实体

   ```Java
   Costomer cust1 = new Costomer("Tom",21);
   Costomer cust2 = new Costomer("Tom",21);
   System.out.println( cust1 == cust2 );//false
   ```

   #  toString()

   1. 当我们输出一个对象的引用时，实际上就是调用当前对象的 toString() 方法，返回地址。
   2. <font color='#FF0000'>String</font>、<font color='#FF0000'>Data</font>、<font color='#FF0000'>File</font>、<font color='#FF0000'>包装类</font>等都<font color='#FFFF00'>重写</font>了Object 类中的 toString()方法，使得在调用对象的时 toString() 时，返回“实体内容”信息
   3. 自定义类也可以重写 toString() 方法 ，当调用此方法时，返回对象的“实体内容”，使用右键的 source 可以使用系统已重写过的封装好的toString方法
   
   ```Java
   public static void mian(String[] args){
       Customer cust1 = new customer("Tom",21);//自定义的一个类，未重写
       System.out.println(cust1.toString());//com.atguigu.Java1.Customer@15db9742  
       System.out.println(cust1);//com.atguigu.Java1.Customer@15db9742,地址值与上面相同，说明prinln当检测到参数是object时，会自动调用toString()方法【未重写】
       String str = new String("MM");
       System.out.println(str);//MM
       Date date = new Date(4534534534543L);
       System.out.println(date.toString());//Mon Sep 11 08:55:34 GMT+08:00
       //String、Date系统已重写过
   }
   //toString源码
     public String toString() {
           return getClass().getName() + "@" + Integer.toHexString(hashCode());
       }
   ```
   
   

