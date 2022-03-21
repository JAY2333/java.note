# 单元测试

可以把要测试的代码放进来运行测试

## 步骤：

1. 选中当前工程 —— 右键选择：build path - add libraries - JUnit 4 —— 下一步

2. 创建 Java 类，进行单元测试

   此时的 Java 类要求：① 此类提供公共的无参的构造器

3. 此类中声明单元测试方法

   此时的单元测试方法：方法的权限是 public ，没有返回值，没有形参

4. 此单元测试方法上需要声明注释：@Test，并在单元测试类导入：import org.junit.Test；

5. 声明好单元测试方法以后，就可以在方法体内测试相应的代码

6. 写完代码后，左键双击单元测试方法名，右键：run as - JUnit Test

<img src="D:\公式教程1\Typora\picture\image-20211111200835345.png" alt="image-20211111200835345" style="zoom:33%;" />

<img src="D:\公式教程1\Typora\picture\image-20211111200924897.png" alt="image-20211111200924897" style="zoom:33%;" />

<img src="D:\公式教程1\Typora\picture\image-20211111200956649.png" alt="image-20211111200956649" style="zoom:33%;" />

![image-20211111201232290](D:\公式教程1\Typora\picture\image-20211111201232290.png)

<img src="D:\公式教程1\Typora\picture\image-20211111201331177.png" alt="image-20211111201331177" style="zoom:33%;" />

![image-20211111201418343](D:\公式教程1\Typora\picture\image-20211111201418343.png)

### 说明：

1. 如果执行结果没有任何异常：绿条
2. 如果执行结果出现异常：红条