# 枚举

## 枚举类的使用

1. 类的对象是有限个
2. 定义一组常量时，强烈建议使用枚举
3. 如果枚举类只有一个对象，则可以当作单例模式的实现方法

## 如何定义枚举类

**方式一：jdk5.0前，自定义枚举类**

```java
	public class SeasonTest{
        Season spring = Season.SPRING;
        System.out.println(spring);
    }
	class Season{
        //1.声明Season对象的属性，声明为 final 不可变的常量后，可以 显式赋值/代码块赋值/构造器赋值 前两者只能定义一个常量，后者可随构造器对象赋值多个不同常量
        private final String seasonName;
        private final String seasonDesc;
        //2.私有化类的构造器，并给对象赋值
        private Season(String seansonName,String seasonDesc){
            this.seasonName = seasonName;
            this.seasonDesc = seasonDesc;
        }
        //3.对象声明为static,final，这样将能让Season类去指定其中一个构造器
        public static final Season SPRING = new Season("春天","春暖花开");
        public static final Season SUMMER = new Season("夏天","烈日炎炎");
        public static final Season AUTUMN = new Season("秋天","秋高气爽");
        public static final Season WINTER = new Season("冬天","傲雪凌霜");
        //4.其它诉求①提供toString(){
        @Override
        public String toString(){
        return "Season{" + "seasonName = '" + '\'' + ",seasonDesc=" + seasonDesc + '\'' + '}';
        }
        //②提供getXxx()方法以供调用
        public String getSeasonName(){
            return seasonName;
        }
        public String getSeasonDesc(){
            return seasonDesc;
        }
      }
    }
```

​    **方式二：Enum**

```Java
 	@Test	
	public class SeasonTest{
        Season spring = Season.SUMMER;
        System.out.println(spring);//SUMMER,打印的是常量名，可以调用get方法
    }
	enum Season{
                //1.让Season类去指定其中一个构造器，多个对象之间用逗号
         SPRING("春天","春暖花开")，
         SUMMER("夏天","烈日炎炎")，
         AUTUMN("秋天","秋高气爽")，
         WINTER("冬天","傲雪凌霜");
        //2.声明Season对象的属性，private final 修饰
        private final String seasonName;
        private final String seasonDesc;
        //3.私有化类的构造器，并给对象赋值
        private Season(String seansonName,String seasonDesc){
            this.seasonName = seasonName;
            this.seasonDesc = seasonDesc;
        }
        //4.其它诉求①,enum继承于lang类，toString()也可以去重写，一般不需要
      // @Override
       // public String toString(){
       // return "Season{" + "seasonName = '" + '\'' + ",seasonDesc=" + seasonDesc + '\'' + '}';
        }
        //②提供getXxx()方法以供调用
        public String getSeasonName(){
            return seasonName;
        }
        public String getSeasonDesc(){
            return seasonDesc;
        }
      }
    }
```

**Enum的常用方法**

```java
	@Test 		
	public class SeasonTest{
        Season spring = Season.SUMMER;
        System.out.println(spring.toString());//SUMMER,打印的是常量名，可以调用get方法
        //values()：返回所有枚举类组成的数组
        Season[] values = season.values();
        for(int i = 0,i < values.length(),i++){
            System.out.print(values[i]);//SPRING SUMMER AUTUMN WINTER
            }
        //valueof(String objName)  返回枚举类对象名是objName的对象，如果没有objName的枚举类对象，则抛异常：IllegalArgumentException
            Season winter = Season.valueof("WINTER");
            System.out.println(winter);
        //    
    }
```

![image-20220314191401928](../picture/image-20220314191401928.png)

## 使用enum关键字实现接口类

```java
 	@Test	
	public class SeasonTest{
        Season spring = Season.SUMMER;
        //spring.show();当方法在此处重写时，所有对象通用----show重写方法在枚举类里
        spring.show();//SPRING独用此方法----show重写方法在枚举类的对象里面
    }
	interface Info{
        void show();
    }
	enum Season implements Info{
                //1.让Season类去指定其中一个构造器，多个对象之间用逗号
         SPRING("春天","春暖花开"){
         @Override
             public void show(){
                 System.out.println("SPRING独用此方法")
             }
         }，
         SUMMER("夏天","烈日炎炎"){
         @Override
             public void show(){
                 System.out.println("SUMMER独用此方法")
             }
         }，
         AUTUMN("秋天","秋高气爽"){
         @Override
             public void show(){
                 System.out.println("AUTUMN独用此方法")
             }
         }，
         WINTER("冬天","傲雪凌霜"){
         @Override
             public void show(){
                 System.out.println("WINTER独用此方法")
             }
         };
        //2.声明Season对象的属性，private final 修饰
        private final String seasonName;
        private final String seasonDesc;
        //3.私有化类的构造器，并给对象赋值
        private Season(String seansonName,String seasonDesc){
            this.seasonName = seasonName;
            this.seasonDesc = seasonDesc;
        }
        //②提供getXxx()方法以供调用
        public String getSeasonName(){
            return seasonName;
        }
        public String getSeasonDesc(){
            return seasonDesc;
        }
      //若重写不定义在各个枚举类的对象里，则所有枚举类对象都实现同一个show()方法
        //@Override
        //public void show(){
			//System.out.println("当方法在此处重写时，所有对象通用");
        //}
    }
```

  
