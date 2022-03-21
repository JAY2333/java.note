# 异常

 Error : Java虚拟机无法解决的严重问题。如：**JVM系统内部错误**、**资源耗尽** 等严重情况。比如：StackOverflowError 和 OOM。一般不编写针对性的代码进行处理。（基本只能修改源代码）

Exception:其它因编程错误或偶然的外在因素导致的一般性问题，可以使用针对性的代码进行处理。例如：

* 空指针访问
* 试图读取不存在的文件
* 网络连接中断
* 数组角标越界

## Error

```java
	//error	
		public class ErrorTest{
            public static void main(String[] aegs){
                //1.栈溢出：java.lang.StackOverflowError
                main(args);//相当于main方法无限调用main方法，会造成栈溢出
            
                //2.堆溢出：java.lang.OutOfMemoryError
                Integer[] arr = new Integer[1024*1024*1024]
            }
        }
```

1.<font color='#FFFF00'>栈溢出</font>

![image-20210528210054464](D:\公式教程1\Typora\picture\image-20210528210054464.png)

2.<font color='#FFFF00'>堆溢出</font>

![image-20210528210211544](D:\公式教程1\Typora\picture\image-20210528210211544.png)

## Exception

1.  编译时异常( checked )（<font color='#CD5C5C'>受检异常</font>）  【在编译 javac.exe时出错】

   1. IOException

   2. FileNotFoundException

   3. ClassNotFoundException

      ```java
      		//IOException
      		File file = new File("hello.txt");
      		FileInputStream fis = new FileInputStream(file);
      		int data = fis.read();
      		while(data != -1){
                  System.out.print((char)data);
                  data = fis.read();
              }
      		fis.close();
      ```

      

2.  运行时异常( unchecked / RuntimeException)（<font color='#00FA9A'>非受检异常</font>）   【在运行java.exe时出错】

   ​	捕获运行时异常是为了反馈到前端页面进行提醒

   1. NullPointerExcetion  (空指针异常)
   
      ```java
      		int[] arr = null;
               System.out.println(arr[3]);
      
      		String str = "abc";
      		str = null;
      		System.out.println(str.charAt(0));
      ```

        

   2. ArryIndexOutOfBoundsException  (数组越界)
   
      ```java
      		int[] arr = new int[10];
      		System.out.println(arr[10]);//ArrayIndexOutOfBoundsException
      
      		String str = "abc";	
      		System.out.println(str.charAt(3));//StringIndexOutOfBoundsException
      ```
      
      
      
   3. ClassCastException (类型转换异常)
   
      ```java
      		Object obj = new Date();
      		String str = (String)obj;
      ```
   
      
   
      1. NumberFormatException(数字格式异常)
   
   
      ```java
      		String str = "123O";//字母o
      		int str1 = str.parseInt(str);
      ```
   
      
   
   4. InputMismatchException (输入异常)
   
      ```java
      		Scanner scanner = new Scanner();
      		int score = scanner.nextInt();
      		System.out.println(score);
      		//在控制台输入非数字
      ```
   
      
   
   5. ArithmeticException (算数异常)
   
      ​	
   
      ```java
      		int a = 10;
      		int b = 0;
      System.out.println(a / b);
      ```
   
      ### 异常的处理：抓抛模型
   
      1. 过程一：“抛”：程序在正常执行中，一旦出现异常，就在异常代码处生成一个对应异常类的对象。并将此对象抛出。
   
         一旦抛出对象以后，其后代码就不再执行。
   
         关于异常对象的产生：
   
         ①系统自动生成的异常对象
   
         ②手动的生成一个异常对象，并抛出（throw）【throw是抛的过程中手动生成的一个异常对象，throws是抓的过程中异常处理的方式】
   
      2. 过程二：“抓”：可以理解为异常的处理方式：①try-catch-finally  ② throw

### 异常处理机制一：try-catch-finally

1. #### try-catch-finally的使用

   ```Java
   		try{
   		//可能出现异常的代码
   		}catch(异常类型1 变量名1){
   			//处理异常的方式1
            }catch(异常类型2 变量名2){
   			//处理异常的方式1
            }catch(异常类型3 变量名3){
   			//处理异常的方式1
           }
   		...
            finally{
                //一定会执行的代码
            }   
   ```

   ```Java
   		public class ExceptionTest1{
               @Test
               public void test(){
                   String str = "123";
                   str = "abc";
                   try{
                       int num = Integer.parseInt(str);
                       System.out.println("hello-------1");
                     	}catch(NullPointerException e){
                        System.out.println("出现空指针异常了，不要着急！"); 
                       }catch(NumberFormatException e){
                       //粗暴提示
                        System.out.println("出现数值转换异常了，不要着急！"); 
                       //正规处理提示方式一：使用 String getMessage();
                          System.out.println(e.getMessage); 
                       //正规处理提示方式二：使用 printStackTrace;
                           e.printStackTrace();
                   	}
                   System.out.println("hello------2");
               }
           }
   ```

   ![image-20210529004448114](D:\公式教程1\Typora\picture\image-20210529004448114.png)

2. #### 说明：

   1. finally 是可选的

   2. 使用 try 将可能出现异常代码包装起来，子执行过程中，一旦出现异常，就会生成一个对应异常类的对象，根据此对象的类型，去catch中进行匹配

   3. 一旦 try 中的异常对象匹配到某个catch时，就进入 catch 中进行异常的处理，一旦处理完成，就跳出当前的 try-catch 结构（在没有写 fianly 的情况），继续执行其后的代码 

   4. 

      * catch中的异常类型如果没有子父类关系，则谁声明在上，谁声明在下无所谓
      * catch中的异常类如果满足子父类关系，则要求子类一定要声明在父类的上面，否则报错
      * ![image-20210529011951952](D:\公式教程1\Typora\picture\image-20210529011951952.png)

   5. 常用的异常对象处理方式：

      ①String getMessage() (打印了出错的信息)

      ② printStackTrace() (常用)

   6. <font color='#00BFFF'>在 try 结构中声明的变量，在出了 try 结构以后就不能再被调用</font>
   
   体会：
   
   * 使用 try-catch-finally 处理编译时异常，使得程序在编译时不再报错，但运行时仍可能报错，相当于我们使用体会：使用 try-catch-finally 将一个编译可能出现的异常，延迟到运行时出现。
   * 开发中，由于运行时异常比较常见，我们通常就不针对运行时异常编写 try-catch-finally 了。针对编译时异常，我们一定要考虑异常
   
3. try-catch-finally 中的 finally 的使用

   1. finally 是可选的

   2.  finally 中声明的是一旦会被执行的代码，即使 catch 中又出现异常了，try 中有 retuen 语句，catch 中有return语句情况等

      ```Java
      			public int method(){
                      try{
                          int[] arr = new int[10];
                          System.out.println(arr[10]);
                          return 1;
                      }catch(ArrayIndexOutOfBoundsException e){
                          e.printStackTrace();
                          return 2;//如果下边的finally没有return 3 ,将继续执行这个catch,执行return 2
                      }finally{
                          System.out.println("我一定被执行");
                          return 3;//由于finally必须被执行，故而ArrayIndexOutOfBoundsException异常的return 2将不会b执行，而是在return 3 结束程序
                      }
                  }	
      ```

   3. try-catch-finally可以嵌套使用

   4. 使用环境：如 输入输出流 / 数据库连接 / 网络编程 Scoket 等资源，JVM不能自动回收的，我们仍需要手动进行资源的释放。此时的资源释放，就必须放在 finally 中。

      ```Java
      		public void test2(){
                  FileInputStream fis = null;
                  try{
                      File file = new File("Hello.txt");
                      fis = new FileInputStream(file);
                      int data = fis.read();
                      while(data != -1){
                          System.out.print((char)data);
                          data = fis.read();
                      }
                  }catch(FileNotFoundException e){
                      e.printStackTrace();
                  }catch(IOException e){
                      e.printStackTrace();
                  }finally{
                      try{				//try-catch-finally嵌套使用
                          if(fis != null)
                     			fis.close();
                      }catch(IOException e){
                          e.printStackTrace();
                      }
                  }
              }	
      ```

### 异常处理机制二：throws  + 异常类型

1. “ throws  + 异常类型”写在方法的声明处。指明此方法执行时，可能会抛出的异常类型。一旦当方法体执行时，如果出现异常，仍会在异常代码处生成一个异常类的对象。此对象满足 throws 后异常类型时，就会被抛出。异常代码后续的代码，就不再执行！异常代码后续的代码，不再执行！（注意只是跳出本throws的模块  ）

2. 体会：try-catch-finally：真正的将异常给处理掉了

   throws 的方式只是将异常抛给了方法的调用者，并没有真正将异常处理掉

3. 开发中如何选择使用 try-catch-finally 还是 throws ?

   1. 如果父类中被重写的方法没有 throws 方式处理异常，则子类重写的方法也不能使用 throws ，意味着如果子类重写的方法中有异常，必须使用 try-catch-finally 方式处理
   2. 执行的方法中，先后又调用了另外的几个方法，这几个方法是递进关系执行的。我们建议这几个方法使用throws的方式处理，而执行的方法a可以考虑使用 try-catch-finally方式处理

```java
	public class ExceptionTest2 {
        public static void main(String[] args){
         try{
            method2();
         }catch(IOException e){
             e.printStackTrace();
         }
            method3();
        }
        public static void method3(){
            try{
                method2();
            }catch(IOException e){
                e.printStackTreace();  
            }
        }
        public static void method2() throws IOException{
            method1();
        }
		public static void method1() throws FileNotFoundException,IOException{
            Flie file = new FileInputStream(file);
            int data = fis.read();
            while(data != -1){
                System.out.print((char)data);
                data = fis.read();
            }
            fis.close();
            System.out.println("此处可能不执行");//当前面的代码被捕获到异常，本throws模块异常处之后的代码将不再往后执行
        }
	}
```

## 手动抛出异常

```java
		public class StudentTest {
            Stuent s = new Student();
            try{//方式二处理
            s.regist(-1001);
            }catch(Exeption e){//使用try-catch-finally
                //e.printStackTrace 此处可更换为下面手动的输出异常类对象e的自定义内容
                 System.out.println(e.getMessage());
            }
            System.out.println(s);
        }
		class Student{
            private int id;
            public void regist(int id) throws Exception{
                if(id > 0){
                    this.id = id;
                }else{
     			  //粗暴地处理异常              
                   // System.out.println("您输入的数据非法!");
                    
                    
                    //手动抛出异常
                    //方式一，不进行异常处理
                   // throw new RuntimeException("您输入的数据非法");此方法是不用向上throws从而抛给被调函数进行try-catch-finally处理的
                   
                    //方式二，进行异常处理
                    throw new Exception("您输入的数据非法！");
                }
            }
        }
```

## 用户自定义异常

1. 继承于现有的异常结构：RuntimeException、Exception
2. 提供全局常量：serialVersionUID
3. 提供重载构造器

```Java
		public class MyException extends RuntimeException{
            static final long serialVersionUID = -7034897190745766939L;//模仿 RuntimeExceptiond 的继承模板[数字串表示类的唯一标识号]
            public MyException(){           
            }
            public MyException(String msg){
                super(msg);
            }
        }
		class Student{
            private int id;
            public void regist(int id) throws Exception{
                if(id > 0){
                    this.id = id;
                 	}else{
                    	throw new MyException("不能输入负数");//throw 只能抛出属于异常类的子类对象，此时是调用了构造器的
                	}
            	}
		}
			public class StudentTest {
            try{
            	 	Stuent s = new Student();
                 	s.regist(-1001);
                	System.out.println(s);
            	}catch(Exception e){
                		//e.printStackTrace
                		System.out.println(e.getMessage());
            	}
            }
```

## 比较 throw 和 throws 的异同

throw：手动→生成一个异常对象并抛出，在方法内部使用，自动→自动抛出异常对象

throws：处理异常的方式使用在方法处声明处的末尾
