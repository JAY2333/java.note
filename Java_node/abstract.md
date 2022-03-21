# 抽象类与抽象方法

##  定义：

随着继承层次中一个个新子类的定义，类变得越来越具体，而父类则更一般，通用。类的设计应保证父类和子类能共享特征。而有时将一个父类设计得非常抽象，以至于它没有具体的实列，这样的类叫做<font color='#9400D3'>抽象类</font>

abstract关键字的使用		

1. ​	abstract  ：抽象的

2. ​     abstract 可以用来修饰的结构：类、方法

3. abstract修饰类：抽象类
   * <font color='#FF0000'>此类不能实例化</font> 
   * 抽象类中一定有构造器，便于<font color='#9400D3'>***子类实例化时调用***</font>(涉及子类对象实例化的全过程)
   * 开发中，都有提供抽象类的子类，让子类对象实例化，完成
   
4. abstract 修饰方法 ：抽象方法
   * 抽象方法只有方法的声明 ，没有方法体
   * 包含抽象方法的类，一定是一个抽象类，反之，抽象类中可以没有抽象方法
   * 若子类重写了父类中的所有的抽象方法后，此子类方可实例化
   * 若子类<font color='#00BFFF'>没有</font>重写了父类中的所有的抽象方法，则此子类也是一个抽象类，也需要abstract去修饰
   
   #### 注意点
   
   1. abstract 不能用来修饰：属性、构造器等结构
   2. abstract 不能用来修饰私有方法、静态方法、final方法、final的类

### 规范示例

```java
	public class AbstractTest{
        public static void main(String[] args){
            Student s = new Student("王贵炳"，21);
            s.walk();
            s.eat();
        }
    }
	abstract class Person{
        String name;
        int age;
        public Person(){
        }
        public Person(String name,int age){
            this.name = name;
            this.age = age;
        }
        public abstract void eat();//抽象方法
        public void walk(){
            System.out.println("散步");
        }
    }
		//处理带有抽象方法的子类的实现方法一
		class Student extends Person{
            public Student(String name,int age){
                super(name,age);//调用父类的构造器
            }
            @Override
            public void eat(){
               System.out.println("学生吃饭");
           } 
        }
		//处理带有抽象方法的子类实现方法二
		abstract class Student2 extends Person{ 
            public Student(String name,int age){
                super(name,age);//调用父类的构造器
            }
            //由于子类没有重写抽象方法，因此该子类要加 abstract 修饰
        }
```

### 抽象类的匿名使用

```Java
		public class PersonTest{
            public static void main(String[] args){
          method1(new Student());//1.匿名对象(省略了对student的实例化)  
          method2(new Worker());//2.非匿名类的匿名对象（worker类的匿名对象，相当于Worker w = new Worker();                                            method2(w);[标准写法：非匿名的类且非匿名的对象]）
           
            Person p = new Person(){//3.匿名子类非匿名对象p。创建了一匿名子类p，省略了创建一个类去继承抽象类的过程，当任                                       // 只需一次使用时，用这个方法能提高效率
               @Override               
               public void sleep(){        
                   System.out.println("好好睡觉");//匿名子类要重写其父类的抽象方法
               }
            };
                   method2(p);
                   //这个是对Person抽象类实例化子类的匿名写法
                    
                   method2 ( Person(){   //4.匿名子类匿名对象。对上述匿名子类的更简便写法，把简便创建子类p的步骤也省略了
                        @Override
                        public void sleep(){
                            System.out.println("好好睡觉")；
                          }      
                   } );   
           }     
            } 
            //注意此时的Student是实例化后的类【子类】
            public static void method1(Student s){
                //方法体略
            }
            //注意此时的Person是抽象类【父类】,由于数据类型是抽象类，故传递的仍应为实例化的子类或该抽象类的匿名子类
            public static void method2(Person p){
          	    p.sport();
                p.sleep();//父类的抽象方法
            }
        }
		//抽象类创建
		abstract class Person{
            public void  sport(){
      System.out.println("运动");
            }
           public abstract void  sleep();
        }
		//Worker子类
		class Worker extends Person{
            @Override
            public void  sleep(){
                //TODO Auto-generated method stub
            }
        }
		//student子类
		class Student extends Person{
        public Student(){
            super();
        }
            @Override
            public void sleep(){
        System.out.println("学生睡觉");
           } 
        }
```



