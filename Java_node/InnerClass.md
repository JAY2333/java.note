# 内部类

1. ### Java 中允许将一个类A声明在另一个类B中，则类A就是内部类，类B称为外部类

2. ### 内部类的分类：成员内部类 VS 局部内部类（方法内、代码块内、构造器内）

3. #### 成员内部类：

   1. ​	一方面，作为一个类：
      1. 类内可以定义属性、方法、构造器等
      2. 可以被 final 修饰，表示此类不能被继承。不使用 final，则可以被继承
      3. 可以被 abstract 修饰
   2. ​	另一方面：作为外部类的成员：
      1. 调用外部类的结构
      2. 可以用 static 修饰
      3. 可以被4种不同的权限修饰

```java
		public class  InnerClass{
            Person.Hands hands = new  Person.Hands();//创建Hands实例（静态的成员内部类实例化）
            hands.move();//静态内部类成员对象的方法调用
            
            //非静态的成员内部类实例化
            //Person.Leg leg = new Person.Leg();错误的写法
            Person p = new Person();
            Person.Leg leg = p.new Person.Leg();//创建Leg实例（非静态的成员内部类实例化）
            leg.run();//非静态内部类成员对象的方法调用
        }
	class Person{
        //属性
        String name;
        //方法
        public void sport(){
     System.out.println("sport");
        }
        //静态成员内部类
        static class Hands{
            public void move(){
              System.out.println("移动");
            }
        }
        //非静态成员内部类
        class Leg{
            //内部类的属性
            String name;
            //内部类的方法
            public void run(){
            Person.this.sport();//可以调用外部类结构
            }
            public void display(String name){
              System.out.println( name );//输出传参的值
              System.out.println( this.name );//输出本内部类的属性值
              System.out.println( Person.this.name );//输出外部类的属性值
            }//如果与外部类不同名则可直接返回外部类属性值
        }
        
        public void method(){
            //局部内部类
            class A{
            }
            class B{
            }
        }
        //构造器
        public Person(){
            //局部内部类
         class C{  
         }   
        }
    }
```

### 关注如下3个问题：

1. 如何实例化成员内部类的对象（如代码所示↑）
2. 如何在成员内部类种区分调用外部类的结构↑
3. 开发中局部内部类的使用↓↓↓

```java
		//返回了一个实现了Comparable接口的类
		public Comparable getComparable(){
           
            //创建一个实现了Comparable接口的类:局部内部类 
            //方式一：
            class MyComplarable implements Comparable{
                @Override
                public int compareTo(Object o){
                    //TODO Auto-generated method stub
                    return 0;
                }
                return new MyComparable();
            }
            
            //方式二：
            return new Comparable(){
                @Override
                public int compareTo(Object o){
                    return 0;
                }
            };
        }
```

