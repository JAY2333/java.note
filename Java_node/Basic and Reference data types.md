# Java中有俩种数据类型

其中主要有8种基本数据类型和引用数据类型，除了8种基本数据类型以外都是引用数据类型。

## 8种基本数据类型分别是<font color='#FF0000'>byte</font> ，<font color='FFA500'>short</font>,<font color='#FFFF00'>int</font>,<font color='#00FF7F'>long</font>,<font color='#00BFFF'>char</font>,<font color='#00CED1'>boolean</font>,<font color='#9400D3'>float</font>,<font color='#00FA9A'>double</font>

### 具体如下：

 1、**boolean**：数据值只有true或false，适用于逻辑计算。
	    2、**char**：char型（字符型）数据在内存中占用2个字节。char型数据用来表示通常意义上的字符，每个字符占2个字节，Java字符采用Unicode编码，它的前128字节编码与ASCII兼容字符的存储范围在\u0000~\uFFFF，在定义字符型的数据时候要注意加 ' '，比如 '1'表示字符'1'而不是数值1， 
	    3、**byte**：byte型（字节型）数据在内存中占用1个字节，表示的存储数据范围为：-128~127。
		4、**short**：short型（短整型）数据在内存中占用2个字节。
		5、**int**：int型（整型）数据在内存中占用4个字节。
		6、**long**：long型（长整型）数据在内存中占用8个字节。
		7、**float**：float型（单精度浮点型）数据在内存中占用4个字节。（ float 精度为7-8位）
		8、**double**：double型（双精度浮点型）数据在内存中占用8个字节。

## 下面说说java中引用数据类型：

### 引用数据类型分3种：类，接口，数组；

#### 一、类Class引用 

可以是我们创建的，这里我不多讲，主要是讲解几个java库中的类 
**<font color='#FF0000'>Object</font>** ：Object是一个很重要的类，Object是类层次结构的根类，每个类都使用Object作为超类，所有对象（包括数组）都实现这个类的方法。用Object可以定义所有的类 
              如： 
              Object object= new Integer(1); 来定义一个Interger类 
               Integer i=(Integer) object;     在来把这个Object 强制转换成 Interger 类 
**<font color='#FF0000'>String</font>** ：String类代表字符串，Java 程序中的所有字符串字面值（如"abc"）都作为此类的实例来实现。检查序列的单个字符、比较字符串、搜索字符串、提取子字符串、创建字符串副本、在该副本中、所有的字符都被转换为大写或小写形式。 
<font color='#FF0000'>**Date**</font> ：Date表示特定的瞬间，精确到毫秒。Date的类一般现在都被Calendar 和GregorianCalendar所有代替 
Void ：Void 类是一个不可实例化的占位符类，它保持一个对代表 Java 关键字 void 的 Class 对象的引用。 
同时也有对应的Class如：Integer  Long  Boolean  Byte  Character  Double  Float   Short 

### 二、接口interface引用 

可以是我们创建的，这里我不多讲，主要是讲解几个java库中的接口 interface

**<font color='#00FA9A'>List</font><font color='#00FA9A'><E></font>**：

列表 ，此接口的用户可以对列表中每个元素的插入位置进行精确地控制。用户可以根据元素的整数索引 （在列表中的位置）访问元素，并搜索列表中的元素。List 接口提供了两种搜索指定对象的方法。从性能的观点来看，应该小心使用这些方法。在很多实现中，它们将执行高开销的线性搜索。 List 接口提供了两   种在列表的任意位置高效插入和移除多个元素的方法。 

<font color='FFA500'>add()</font> : 在列表的插入指定元素。 
<font color='FFA500'>remove()</font>：移除列表中指定位置的元素。 
<font color='FFA500'>get(int index)</font>：返回列表中指定位置的元素。
		**<font color='#00FA9A'>Map<K,V></font>**

K - 此映射所维护的键的类型 
       V - 映射值的类型 将键映射到值的对象。一个映射不能包含重复的键；每个键最多只能映射到一个值。 
	<font color='#00BFFF'>put(K key,V value)</font>：将指定的值与此映射中的指定键关联（可选操作）。如果此映射以前包含一个该键的映射关系，则用指定值替换旧值（当且仅当，返回 true 时，才能说映射 m 包含键 k 的映射关系）。

<font color='#00BFFF'> remove(Object key)</font>：如果存在一个键的映射关系，则将其从此映射中移除（可选操作）。更确切地讲，如果此 映射包含从满足(key==null ? k==null :key.equals(k))的键 k 到值 v 的映射关系，则移除该映射关系。（该映射最多只能包含一个这样的映射关系.） 

<font color='#00BFFF'>get(Object key)</font>：返回指定键所映射的值；如果此映射不包含该键的映射关系，则返回 **null**。

这里我们主要是用String List Map Object 是最常用Number ArrayList<E> Arrays等 

## 三、数组引用

数组：存储在一个连续的内存块中的相同数据类型（引用数据类型）的元素集合。

数组中的每一个数据称之为数组元素，数组中的元素以索引来表示其存放的位置，索引（下标）从0开始。

### 数组的定义

 第一种方式：类型[] 数组名; 如 int[] nums; 
		第二种方式：类型数组名[]; 如 int nums[];
大多数Java程序员喜欢使用第一种风格,因为它把数据类型int[],和变量名num分开了.
数组的初始化
Java中数组必先初始化后才能使用.
初始化就是给数组元素分配内存，并为每个元素赋初始值。
初始化数组的两种方式：

- 静态初始化:
语法格式:类型[] 数组名 = new 数组类型[]{元素1,元素2,元素3,...元素n};
简化语法：类型[] 数组名 = {元素1,元素2,元素3...元素n};
- 动态初始化:
如果我们事先不知道数组里存储哪些数据，只知道需要存储数据的个数，此时可以使用动态初始化方式。
动态初始化：初始化时由我们指定数组的长度，系统自动为数组元素分配初始值。
格式：类型[] 数组名 = new 数组类型[数组长度];
注意:无论，以哪种方式初始化数组，一旦初始化完成，数组的长度就固定了，不能改变，除非重新初始化。也就是说数组是定长的。

### 为什么Java里有基本数据类型和引用数据类型？

<font color='#00CED1'>引用类型</font>在<font color='#00CED1'>堆</font>里，<font color='#00FF7F'>基本类型</font>在<font color='#00FF7F'>栈</font>里。

栈空间小且连续，往往会被放在缓存。引用类型cache miss率高且要多一次解引用。

对象还要再多储存一个对象头，对基本数据类型来说空间浪费率太高