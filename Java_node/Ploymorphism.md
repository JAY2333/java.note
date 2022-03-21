# 多态性

### <font color='#FFFF00'>重载</font>  和  <font color='#FFFF00'>重写</font> 是实现多态的两种主要方式

## 实现多态：

1. #### 接口多态性

2. #### 继承多态性

3. #### 通过抽象类实现的多态性

## <img src="D:\公式教程1\Typora\picture\HOQ_6H%R1O{QVU3F7`SI2F8.png" alt="img" style="zoom: 200%;" />

## 多态的应用： 模板的方法设计模式（ Template Method ） 

抽象类体现的就是一种模板模式的设计，抽象类作为多个子类的通用模板，子类在抽象类的基础上进行扩展、改造，但子类总体上会保留抽象类的行为方式。

### 解决的的问题：

* 当功能内部一部分实现是确定的，一部分是不确定的。这时可以把不确定的部分暴露出去，让子类去实现。
* 换句话说，<font color='FFA500'>在软件开发中实现一个算法时，整体步骤已经在父类中写好了。但某些部分易变，易变部分可以抽象出来，供不同的子类实现，这就是一种模板模式</font>。

```java
               //模板方法示例一
				public class TemplateTest{
                    public static void main(String[] args){
                        SubTemplate t = new SubTemplate();
                        t.spendTime();
                    }
                }
                //父类的模板方法
                 abstract class Template{
                     public void spendTime(){
                     	long start = System.currentTimeMillis();
                    	this.code();//不确定的、易变的部分
                    	long end = System.currentTimeMillis();      
                		System.out.println("spend times: "+(end - start));
                         }
                	public abstract void code();//抽象方法
                 }
                 //子类的实例(重写code的抽象方法——求质数)
                class Subtemplate extends Template{
                    @Override
                    public void code() {
                        for(int i = 2;i <= 1000;i++){
                            boolean isFlag = true;
                            for(int j = 2;j <= Math.sqrt(i);j++){
                                if(i % j == 0){
                                    isFlag = false;
                                    break;
                                }
                            }
                            if(isFlag){
                                System.out.println(i);
                            }
                        }
                    }
                }
```

```java
			//模板方法示例二
			public class TemplateMethodeTest{
                public static void main(String[] args){
                    BankTemplateMethod btm = new DrawMoney();
                    btm.process();
                    
                    BankTemplateMethod btm2 = new ManageMoney();
                    btm2.process();
                }
            }
		abstract class BankTemplateMethod{
            //具体方法
            public void takeNumber(){
                System.out.println("取号排队");
            }
            public abstract void transact();//办理具体的业务【钩子方法】
            public void evaluate(){
                System.out.println("反馈评分");
            }
            //模板方法，把基本操作组合在一起，子类一般不重写
            public final void process(){
                this.takeNumber();
                this.transact();//钩子方法的实现，具体执行时，挂到哪个重写了该抽象方法的子类就执行这个子类的实现代码
                this.evaluate();
            }
        }
		//子类一
		class DrawMoney extends BankTemplateMethod{
            public void transact(){
                System.out.println("我要取款！");
            }
        }
		//子类二
		class ManageMoney extends BankTemplateMethod{
            public void transact(){
                System.out.println("我要理财!我这里有钱！！");
            }
        }
```

