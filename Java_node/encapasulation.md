# 封装性

## 面向对象的特征一：封装与隐藏

### 封装性的体现

1. 将类的属性 x x x 私有化（private），同时提供公共的（public）方法获取（getXxx)【有返回值】和设置（setXxx)【无返回值void+需求限制】此属性的值
2. 不对外暴露的私有方法
3. 单例

```java
  public class AnimalTest{
      public static void main(string[] args){
        Animal a = new Animal();
          a.name = "旺财";
          a.age = 5;
          a.setLeg(4);
          a.getLegs();
    }
  }    
   class Animal(){
 		    String name;
        	int age;
       private int legs;
       public void setLegs(int l){
           if(l>0 && l%2==0){
               legs = l;
           }else
              legs = 0;
       }
       public int getLegs(){
           return legs;
       }
       public void show(){
  System.out.printf("name:"+a.name+"age:"+a.age+"leg:"+a.legs);
       }
    }


```

### 封装性的体现需要权限修饰符来配合

1. Java规定的4种权限（从大到小排列）：private 、 缺省 、protected 、public  

2. 4种权限都可以用来修饰类及类的结构：属性、方法、构造器、内部类

3. 具体的，4种权限都可以用来类的内部结构：属性、方法、构造器、内部类

4. 修饰类的话，只能使用：缺省、public

5. ![](D:\公式教程1\Typora\picture\GEB0$%ON`AFN2%{6B7`3O.png)

   #### **总结**

   **java提供了4种权限修饰符来修饰类及类的内部结构，体现类及类的内部结构在被调用时的可见性的大小**

# this（尚硅谷P232）

## 说明

1. this可以修饰：属性、方法、构造器
2. this修饰属性、方法时：this理解为：当前对象或正在创建的对象
3. 通常情况下，选择省略this.（如果方法形参和类的属性同名时，必须显式地使用“this.变量”的方式，表明此变量是属性，而非形参）

## 应用

### this调用构造器（减少代码冗余）

1. 我们在类的构造器中，可以显式地使用“this（形参列表)”方式，调用本类中指定地其它的其他构造器
2. 构造器中不能通过“this(形参列表)”方式调用自己
3. 如果一个类中有n个构造器，则最多有n-1个构造器中使用了“this(形式列表)”
4. 规定：“this（形参列表）必须声明在当前构造器的首行
5. 构造器内部最多只能声明一个”this（形参列表）”，用来调用其它的构造器

[【尚硅谷】Java基础全套教程,JAVA零基础入门必备,适合初学者的完整视频 (宋红康主讲)_哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/video/BV1Kb411W75N?p=234&spm_id_from=pageDriver)

