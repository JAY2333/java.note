#  注解

![image-20220314201827095](../picture/image-20220314201827095.png)

![image-20220314202344634](../picture/image-20220314202344634.png)

![image-20220314204151712](../picture/image-20220314204151712.png)

![image-20220314202622772](../picture/image-20220314202622772.png)

![image-20220314204122813](../picture/image-20220314204122813.png)

## 如何自定义注解

![image-20220314211016060](../picture/image-20220314211016060.png)

```java
/** 仿照SupperWarrings定义
*①注解声明为:@interface
*②内部定义成员，只有单个成员时通常使用value表示
*③可以指定成员默认值，使用 default 定义
*④如果自定义注解没有成员，表明一个标识作用
*如果注解有成员，在使用注解时，需要指名员的量
*自定义注解必须配上注解的信息处理流程（使用反射）才有意义
*自定义注解通过都会指明两个元注解：Rentention、Target
*jdk提供的四种元注解
元注解：对现有的注解进行解释说明的注解
Retention:指定所修饰的 Annotation 的生命周期：SOURCE\CLASS(默认行为)\RUNTIME,只有声明为 RUNTIME 生命周期的注解，才能通过反射获取
Target:用于指定被修饰的 Annotation 能用于修饰哪些程序元素【例如类，构造器，属性等】
Docimented:表示所修饰的注解在被 javadoc 解析时，会被保留下来
Inherited:被它修饰的 Annotation 将具有继承性,父类声明该注解时，其子类自动加上该注解
**/
@Inherited
@Repeatable(MyAnnotations.class)
@Retention(RetentionPolicy.RUNTIME)
@Target({TYPE,FIELD,METHOD,PARMETER,CONSTRUCTOR,LOCAL_VARIABLE,TYPE_PARAMETER})
public @interface MyAnnotation {
	String value() default "hello";
}
```

```java
 @MyAnnotation(value = "hi")
class Person{
}
```

### JDK8新特性

```java
//jdk8之前
MyAnnotations({MyAnnotations(value="hi"),MyAnnotations(value="hello")})
    jdk8之后
//可重复注解：①在MyAnnotation上声明@Repeatable,成员值为MyAnnotations.class
//②MyAnnotation的Target和Retention等元注解与MyAnnotations相同
//类型注解:①ElementType.TYPE_PARAMETER:在MyAnnotation注解类中的Target中添加 TYPE_PARAMETER 的声明即可让注解写在类型变量的声明语句中，如泛型声明
	//ElementType.TYPE_USE 表示注解能写在类型的任何语句中
```

