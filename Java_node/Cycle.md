# 循环

## 四要素

1. 初始条件
2. 循环条件 →是<font color='#00FF7F'>boolean</font>类型
3. 循环体
4. 迭代条件

  for(语句1;语句2;语句4){

语句3

​	}

执行顺序：语句1 语句2 语句3 语句4 语句2 语句3 语句4 语句2 语句3 语句4~~~

# 位运算符

<img src="D:\公式教程1\Typora\picture\image-20210518221947005.png" alt="image-20210518221947005" style="zoom:200%;" />

## 二元运算符（   <<        >>    ）

1. 一个<font color='#FF0000'>**m**</font>(十进制)每向左移动<font color='#00CED1'>**n**</font>   [ <font color='#FFFF00'>m <<  n</font> ],得到的数值是<font color='#00BFFF'>n ***（2^n）**</font>(十进制)

2. 一个<font color='#FF0000'>**m**</font>(十进制)每向右移动<font color='#00CED1'>**n**</font>   [<font color='#FFFF00'> m  >>  n</font> ],得到的数值是<font color='#00BFFF'>n **/（2^n）**</font>(十进制)

3. 左右移动有限度，有效位不能溢出最高位（位数由计算机存储位数决定）**<font color='#00FA9A'>最高位是符号位</font>**

4. 如何最高效方式计算2*8？<font color='#00BFFF'>2 << 3</font>

5. 右移的时候，最高位（<font color='#FFFF00'>符号位</font>）不能变.(>>>则全部替换成<font color='#9400D3'>**0**</font>)

   ## &和&&的区别

   - 相同点：运算结果相同
   - 当符号左边是<font color='FFA500'>true</font>时，<font color='#00BFFF'>二者</font>都会执行。当符号左边是<font color='FFA500'>false</font>时，<font color='#FF0000'>&</font>是继续执行，而<font color='#FF0000'>&&</font>不会执行右边

   ##  |   与  || 的区别

   - ​	相同点： |   与  || 运算结果相同
   - 相同点：当符号左边是false时，两者都会执行右边的运算
   - 不同点：当符号左边是<font color='#9400D3'>true</font>时，<font color='#00BFFF'>|</font> 继续执行右边的运算，而 <font color='#00BFFF'>|| </font>不再执行符号右边的运算

## 运算

  <img src="D:\公式教程1\Typora\picture\image-20210518233121059.png" alt="image-20210518233121059" style="zoom:200%;" />

## 三元运算符

1. 结构：（条件表达式）？表达式1：表达式2
2. ​               
   1. 条件表达式结果为 <font color='FFA500'>boolean</font> 类型
   2. 根据条件表达式 <font color='#FF0000'>真</font> 或 <font color='#00FF7F'>假</font>，决定执行表达式<font color='#FF0000'>1</font>，还是表达式<font color='#00FF7F'>2</font>

```Java
			class SanYunTest {
              public static void main(String[] args){
                  int m = 12;
                  int n = 5;
                  int max = ( m > n )? m:n;
                  System.out.println(max); //输出为m
                  
                  double num = ( m > n )? 2:1.0;
                  System.out.println(num); //只有表达式同类型才可输出
                  String maxStr = ( m > n )?"m大":((m == n)?"m和n相等"："n大");
                  System.out.println( maxStr );
              }  
            }
```

