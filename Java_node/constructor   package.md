#  构造器（constructor）

## 一、构造器的作用：

1. 创建对象
2. 初始化对象的信息

## 二、说明：

1. 如果没有显示的定义类的构造器的话，则系统默认一个空参的构造器
2. 定义构造器的格式：权限修饰符 类名（形参列表）{}
3. **一个类中定义的多个构造器，彼此构成重载**
4. 一旦我们显式的定义了类的构造器之后，系统就不再提供默认的空参构造器
5. 一个类中，至少会有<font color='yellow'>**<font color='cornflowerblue'>一个</font>**</font>构造器

## 示例：

```java
  		public class PersonTest{
      		public static void main(String[] args){
        	  Person p = new Person();//对应空参构造器
          	  Person pp = new Person("Tom");//对应一个参数构造器
          	  Person ppp = new Person("Curry",7);//对应双参构造器
       //对象方法调用：
                p.show();
                pp.show();
                ppp.show();
     		 }
  			} 					
         class Person{
         	int age;//默认初始化，若 int age =1,则为显式初始化
        	String name;
       	 public Person(){}//无参构造器
       	 public Person(String n){
           this.name = n;
       }//单参构造器，对name属性初始化
         public Person(String n,int i){
               this.name = n;
               this.age = i;
           }//双参构造器，初始化属性name,age
      	/*
         *方法
         */
          public void show(){
    	  System.out.println(this.age+" "+this.name);
          }
   }
    
```

# psckage(包)

## package关键字的使用

1. 为了更好的实现项目中的类管理，提供包的概念
2. 使用package声明类或接口所属的包，声明在源文件的首行
3. 包属于标识符，遵循标识符的命名规范
4. 每“.”一次代表一层文件目录
5.  
   - 同一个包下，<font color='cornflowerblue'>**不能**</font>命名同一个名字的接口，类
   - **不同**的包下，<font color='orange'>**可以**</font>命名同一个名字的接口，类

![image-20210504025408617](D:\公式教程1\Typora\picture\image-20210504025408617.png)

# MVC模式

![img](D:\公式教程1\Typora\picture\$}RIN5TNUOCVUP40%WZSXTL.png)

# import（导入）关键字

1. 在源文件中显式的使用import结构导入指定包下的类、接口

2. 声明在包的声明和类的声明之间

3. 如果需要导入多个结构，则并列写出即可

4. 可以使用 " <font color='red'> XXX . * </font>" 的方式，表示都如XXX包下所以的结构

5. 如果使用的类或接口是java.lang包下定义的，则可以省略import结构

6. 如果使用的类或接口是本包下定义的，则可以省略import结构

7. 如果在源文件中，使用了不同包下的同名的类，则必须至少有一个类需要以全名的方式显示  

   -   

     ```java
          date = new Account(1000);//属于java.util下的包
          java.sql.Date date1 = new java.sql.Date(1000L)//属于java.sql下的包
              /*
              *由于同名，故而有一个要全名显示
              */ 
     ```

8. 使用“XXX.*”方式表明可以调用XXX包下的所有结构，但是如果使用的是XXX子包下的结构，则仍需要显式导入（java.lang.reflect.Field  是lang的子包，所以要全名导入）

9. import static  ：导入的指定的类或接口中的静态结构:属性或方法