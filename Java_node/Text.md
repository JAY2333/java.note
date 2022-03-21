# **第一个代码text**

```java
public class Text(){
    System.out.printf("Hallo Wlord!");
} 
 class    Test(){
 }
   
```

圆的面积

```java
public class PassOject{
    public static void main(String[] args){
        PassOject text =new PassOject();
        Circle c = new Circle();
        text.printAreas(c,5);
    }
    public void printAreas(Circle c,int time){
        c.radius = i;
        doblic area = c.findArea();
        Ssystem.out.println(c.radius + "\t\t"+area);
    }
}
class Circle{
    double radius;  
    public double findArea(){
        return Math.PI^radius*radius;
    }
} 
```

#  随机数(random)   随机[0,1)

## 获取一个随机数（a,b之间）

### <font color='cyan'>**int**</font>  value = ( <font color='cyan'>**int**</font> ) ( <font color='red'>Math</font>.random()*( <font color='red'>b</font> - <font color='red'>a </font> + <font color='orange'>**1**</font> ) ) +  <font color='red'>a</font>

## 获取一个随机数（0, m-1 之间）

###  value =  ( <font color='red'>Math</font>.random()*m )

