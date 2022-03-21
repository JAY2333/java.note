# 多线程

 ![image-20210530214121569](D:\公式教程1\Typora\picture\image-20210530214121569.png)

![image-20210530224722481](D:\公式教程1\Typora\picture\image-20210530224722481.png)

![image-20210530225116452](D:\公式教程1\Typora\picture\image-20210530225116452.png)

![image-20210530225140903](D:\公式教程1\Typora\picture\image-20210530225140903.png)

# 线程的分类

![image-20211030232046581](D:\公式教程1\Typora\picture\image-20211030232046581.png)

# 线程的生命周期

<img src="D:\公式教程1\Typora\picture\image-20211030232246182.png" alt="image-20211030232246182" style="zoom:150%;" />

##  线程的创建和使用

#### 方式一

1. 创建一个继承于 Thread 类的子类
2. 重写 Thread 类的 run() → 将此线程执行的操作声明在run()中
3. 创建一个 Thread 类的子类的对象
4. 通过此对象调用 start()

```Java
		//创建一个继承于 Thread 类的子类
		class MyThread extends Thread {
            private static int ticket = 100;//必须为static才能实现多线程
          //重写 Thread 类的 run()
            @Override
      public void run() {
          while(true){
            if(ticket > 0){
                System.out.println(Thread.currentThread().getName()+":"+ticket);
                ticket--;
          			}else{
                			break;
            		}
        		}
      		}
        }       
		public class ThreadTest{
            public static void main(String[] args){
                //创建一个 Thread 类的子类的对象
                MyThread t1 = new MyThread();
                MyThread t2 = new MyThread();
          //t1.run();我们不能通过直接调用run()方法启动线程，否则会被视为在主线程执行，达不到分线程执行的效果
                //通过此对象调用 start()
                t1.start();//作用：①启动当前线程 ②调用当前线程的run()
                t2.start();
          //t1.start();同一对象不能再调用启动一个线程。会报IllegalThreadStateException();只能新建对象解决
                //下面的for循环在main线程中执行的
                for( int i = 0; i < 100; i++){
                    if(i % 2 == 1){
                 	   System.out.println(Thread.currentThread().getName()+":"+i+" 主线程");
                    }
                }
            }
        } 
```

#### 方法二（优先使用）【数据可共享】

1. 创建一个实现 Runnable 接口的类
2. 实现类去实现 Runnable 中的抽象方法：run()
3. 创建实现类的对象
4. 将此对象作为参数传递到 Thread 类的构造器中，创建 Thread 类的对象
5. 通过 Thread 类的对象调用 start()

```java
	//创建一个实现 Runnable 接口的类
class MyThread implements Runnable{
    private int ticket = 100;//此数据可共享(注意得是在 MyThread 类的同一个对象)
    //实现类去实现 Runnable 中的抽象方法：run()
    @Override
    public void run(){
        while(true){
            if(ticket > 0){
                System.out.println(Thread.currentThread().getName()+":"+ticket);
                ticket--;
            }else{
                break;
            }
        }
    }
}
public class ThreadTest{
            public static void main(String[] args){
                //创建实现类的对象
            	MyThread m = new MyThread();
                //将此对象作为参数传递到 Thread 类的构造器中，创建 Thread 类的对象
                Thread t1 = new Thread(m);//如果使用匿名对象则不能则要求上面的属性使用 static,否则无法共享数据，线程会互不干扰，理解为变成了两个进程
                Thread t2 = new Thread(m);
                //通过 Thread 类的对象调用 start()
                t1.start();
                t2.start();            
            }
}
```

# Thread 中的常用方法

1. start()：启动当前线程；调用当前线程的 run()
2. run()：通常需要重写 Thread 类的此方法，将创建的线程要执行的操作声明在此方法中
3. currentThread()：静态方法，返回执行当前代码的线程
4. getName()：获取当前线程的名字
5. setName()：设置当前线程的名字
6. yield()：释放当前 cpu 的执行权
7. join()：在线程 a 中调用线程 b 的 join() ，此时线程 a 就进入阻塞状态，直到线程 b 完全执行完以后，线程 a 才结束阻塞状态
8. stop() : 已过时。当执行此方法时，强制结束当前线程
9. sleep( long millistime ):让当前线程“睡眠”指定的 millistime 毫秒，在指定的 millistime 毫秒的时间内，当前线程是阻塞状态
10. isAlive()：判断当前线程是否存活

```java
class HelloThread extends Thread{
    @Override
    public void run(){
        for(int i = 0;i < 100; i++){
            if(i % 2 == 0){
                try{
                    Thread.sleep(10);//此方法要try-catch捕获可能的异常(容易出现InterruptedException异常)
                }catch(InterruptedException e){
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName() + ":" + i);
            }
        }
    }
}
public class ThreadTest{
            public static void main(String[] args){
            	MyThread t = new MyThread();
            }
}
```

# 线程的安全问题

当多个线程在抢占式执行时，若有的线程因为各种原因进入了<font color='#FF0000'>阻塞</font>状态，并且尚未操作完成时，而 CPU 此时将资源分配给其它线程运行，<font color='#FFFF00'>很可能对共享的数据造成</font>例如跳过判断条件等问题的<font color='#FFFF00'>威胁</font>，所以要通过<font color='#00BFFF'>同步机制</font>来解决线程的安全问题。

## 方式一：同步代码块

```java
    synchronized(同步监视器){
	//需要被同步的代码
}
```

说明：

1. 操作共享数据的代码，即为需要被同步的代码
2. 共享数据：多个线程共同操作的变量
3. 同步监视器，俗称：锁。任何一个类的对象都可以当锁（要求：<font color='#00CED1'>多个线程必须公用一个锁</font>）

* 在<font color='#00BFFF'>继承</font> Thread 类创建的多线程方式中，慎用 <font color='#00CED1'>this</font> 充当同步监视器
* 在<font color='#00BFFF'>实现</font> Runnable 接口创建的多线程方式中，可以考虑使用<font color='#00CED1'> this</font> 充当同步监视器
* 操作同步代码时，只能有一个线程参与，其它线程等待，相当于一个单线程过程，效率低，安全性高

```Java
class MyThread implements Runnable{
    private int ticket = 100;
    Object obj = new Object();
    @Override
    public void run(){
        while(true){
            synchronized(obj){
                //使用继承(implements)的方式实现多线程时，可以使用synchronized(this)，此处的this表示【MyThread m = new MyThread()】 m 这个唯一的对象，若使用匿名对象则可以视为多进程，没有多线程效果
                //使用继承(extends)的方式实现多线程则不能使用synchronized(this)，此处的this将代表【MyThread t1 = new MyThread();MyThread t2 = new MyThread();】t1 和 t2 两个对象
                //无论使用继承(implements)还是继承(extends)，都可以使用synchronized(MyThread.class)Class class1 = MyThread.class,因为类都只加载一次，故可充当为唯一对象。【反射原理】
             if(ticket > 0){
                try{
                    Thread.sleep(100);
                }catch(InterruptedException e){
                    e.printStackTrace();
                }
                    System.out.println(Thread.currentThread().getName()+":卖的票号是"+ticket);
                    ticket--;
                }else{
                    break;
                }
            } 
        }
    }
}
public class ThreadTest{
            public static void main(String[] args){
            	MyThread m = new MyThread();
                Thread t1 = new Thread(m);
                Thread t2 = new Thread(m);
                t1.start();
                t2.start();              
            }
}
```

## 方式二：同步方法

如果操作共享数据的代码完整的声明在一个方法中，我们不妨将此方法声明为同步的

* <font color='#00BFFF'>实现</font> Runnable 接口

```Java
class MyThread implements Runnable{
    private int ticket = 100;
    @Override
    public void run(){
        while(true){
			show();
        }
    }
    private synchronized void show(){//把方法声明为 synchronized，此时同步监视器的对象是this，【MyThread m = new MyThread();里的m】
        while(true){
             if(ticket > 0){
                try{
                    Thread.sleep(100);
                }catch (InterruptedException e){
                    e.printStackTrace();
                }
                    System.out.println(Thread.currentThread().getName()+":卖的票号是"+ticket);
                    ticket--;
                }else{
                    break;
                }
        }   
    }
}
public class ThreadTest{
            public static void main(String[] args){
            	MyThread m = new MyThread();
                Thread t1 = new Thread(m);
                Thread t2 = new Thread(m);
                t1.setName("窗口1");
                t2.setName("窗口2");
                t1.start();
                t2.start();              
            }
}
```

* <font color='#00BFFF'>继承</font> Thread 类

```Java
		class MyThread extends Thread {
            private static int ticket = 100;
            @Override
      public void run() {
          while(true){
              show();
        		}
      		}
            private static synchronized void show(){//此时的同步监视器有两个 t1 和 t2，若强制使用必须将此方法声明为静态，方法声明为静态后，同步监视器对象不再是this，而是class
                if(ticket > 0){
                    try{
                    Thread.sleep(100);
                }catch (InterruptedException e){
                    e.printStackTrace();
                }
             System.out.println(Thread.currentThread().getName()+":"+ticket);
              ticket--;
          			}else{
                			break;
            		}
            }
        }       
		public class ThreadTest{
            public static void main(String[] args){
                MyThread t1 = new MyThread();
                MyThread t2 = new MyThread();
                t1.start();
                t2.start();
            }
        }
```

## 方法三：Lock锁

```Java
	class Window implements Runable{
    private int ticket = 100;
    private ReentrantLock lock = new ReentrantLock();//创建Lock对象
    @Override 
    public void run(){
        while(true){
            try{
                lock.lock();//启动锁
                if(ticket > 0){
                    try{
                        Thread.sleep(100);
                    }catch(InterruptedException e){
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread()getName()+":售票，票号为："+ticket);
                    ticket--;
                }else{
                    break;
                }
            }finally{
                lock.unlock();//释放锁
            }
        }
    }
}
	public class LockTest{
     public static void main(String[] args){
        Window w = new Window();
        Thread t1 = new Thread(w);
        Thread t2 = new Thread(w);
        Thread t3 = new Thread(w);
        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");
        t1.start();
        t2.start();
        t3.start();
    }
}
```

### synchronized  和 Lock 的异同？

相同：都用于解决线程问题

<font color='#00BFFF'>不同</font>：syschronized机制在执行完同步代码后，<font color='#00CED1'>自动释放</font>同步监视器

Lock需要手动启动 [ lock() ] 和手动解锁 [ unlock() ]

### 同步方法总结

1. 同步方法仍然涉及同步监视器，只是不需要我们显式地声明
2. <font color='FFA500'>非静态</font>的同步方法，同步监视器是：<font color='#FFFF00'>this</font>
3.  <font color='#FF0000'>静态</font>的同步方法，同步监视器是：<font color='#FFFF00'>class</font> (当前类本身)

### 线程安全的单例模式之懒汉式

```java
public class BankTest{
    }
    class Bank(){}
    private static Bank instance = null;
    public static Bank getInstance(){
        //方式一：效率慢，其它线程只能在此方法处等待
        synchronized (Bank.class){
        	if(instance == null){
            	instance = new 	Bank();
        	}
        }
        return instance;
        
        //方式二:外加判断，后入的线程通过此处判断即可完成
        if(instance == null){
            synchronized (Bank.class){
				if(instance == null){
                		instance = new Bank();
                  }
            }
        }
    }

```

# 线程的死锁问题

## 概念：

1. 不同的线程分别占用对方需要的同步资源不放弃，都在等对方放弃自己需要的同步资源，就形成了线程的死锁
2. 出现死锁后，不会异常，不会出现提示，只有所有的线程都处于阻塞状态，无法继续

## 解决办法

1. 专门的算法、原则
2. 尽量减少同步资源的定义
3. 尽量避免嵌套同步

### 可能死锁的情况

```Java
public class ThreadTest {
    public static void main(String[] args){
        StringBuffer s1 = new StringBuffer();
        StringBuffer s2 = new StringBuffer();
        new Thread(){
            @Override
            public void run(){
                synchronized (s1){
                    s1.append("a");
                    s2.append("1");
                    try{
                    	Thread.sleep(100);
                    }catch(InterruptedException e){
                        e.printStackTrace();
                    }//当第一个线程醒来时，此时第二个线程刚好执行到sleep苏醒，此时s1是充当线程锁，出不来，而这第一个线程需要s2的资源才往下执行    
                    synchronized (s2){
                    	s1.append("b");
                    	s2.append("2");
                        System.out.println(s1);
                        System.out.println(s2);
                    }
                }
            }
        }.start();
        
        new Thread(new Runnable(){
            @Override
            public void run(){
            	synchronized (s2){
                    s1.append("c");
                    s2.append("3");
                    try{
                    	Thread.sleep(100);
                    }catch(InterruptedException e){
                        e.printStackTrace();
                    }//当第二个线程醒来时，等待s1，而上面的s1被第一个线程锁住了，第二个线程的s2又卡死在这里不给释放，于是死锁形成  
                    synchronized (s1){
                    	s1.append("d");
                    	s2.append("4");
                        System.out.println(s1);
                        System.out.println(s2);
                    }
                }
            }
        }).start();
    }
}
```

![image-20220224175044597](D:\公式教程1\Typora\picture\image-20220224175044597.png)

```Java
class Account {
    private int acc;
    private ReentrantLock lock = new ReentrantLock();
    public Account(){}
    public Account(int acc) {
        this.acc = acc;
    }
        public void saveMoney() {
            try {
//                lock.lock();只有打开了才不会有线程安全问题
                acc += 1000;
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName() + "存钱成功，余额为：" + acc);
            } finally {
//                lock.unlock();
            }
        }

    }
    class pTest implements Runnable {
        //这一步可以跨类创建共享对象调用方法
        private Account acc;
        public pTest(Account acc) {
            this.acc = acc;
        }

        @Override
        public void run() {
            for (int times = 0; times <= 2; times++) {
                acc.saveMoney();
            }

        }
    }

public class processOne {
    public static void main(String[] args) {
    Account a = new Account(0);
    pTest p = new pTest(a);
    Thread t1 = new Thread(p);
    Thread t2 = new Thread(p);
    Thread t3 = new Thread(p);
    t1.setName("小明");
    t2.setName("小红");
    t3.setName("小亮");
    t1.start();
    t2.start();
    t3.start();
    }
}
```

#  线程的通信

#### 例子：两个线程打印 1-100 ，线程1 ， 线程2 交替打印

###### 涉及三个方法：

1. wait() : 一旦执行此方法，线程进入阻塞状态，并释放同步监视器
2. notify() : 一旦执行此方法，就会唤醒 wait 的一个线程，如果有多个线程 wait ，就唤醒优先级最高的
3. notifyAll() : 一旦执行此方法，就会唤醒所有被  wait 的线程

###### <font color='#FF0000'>说明</font>：

1. wait() , notify() , notifyAll() 三个方法必须使用在同步代码块或同步方法中
2. wait() , notify() , notifyAll() 三个方法的调用者<font color='FFA500'>必须是同步代码块或同步方法中的同步监视器</font>，<font color='FFA500'>否则，会出现 IllegalMonitorStateException 异常</font>

```java
	class Number implements Runnable{
        private int number = 1;
        private Object obj = new Object();
        @Override 
        public void run(){
            while(true){
             synchronized(obj){
                 obj.notify();//唤醒线程
                if(number <= 100){
                    try{
                        Thread.sleep();
                    }catch(InterruptedException e){
                        e.prinkStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName() + ":" + number);
                    number++; 
                    try{
                        obj.wait();//阻塞线程，会释放锁
                    }catch(InterruptedException e){
                        e.prinkStackTrace();
                    }
                }eles{
                    break;
                }
            } 
            }
        }
    }
public class CommunicationTest{
    public static void main(String[] args){
        Number number = new Number();
        Thread t1 = new Thread(number);
        Thread t2 = new Thread(number);
        
        t1.setName("线程一");
        t2.setName("线程二");
        
        t1.start();
        t2.start();
    }
}
```

### 面试题：sleep() 和 wait() 的异同？

1. 相同点：一旦执行方法，都可以使得当前的线程进入阻塞状态
2. 不同点：
   1. <font color='#00BFFF'>两个方法声明的位置不同： Thread 类中声明 sleep()，Object 类中声明 wait()</font>
   2. <font color='#00CED1'>调用的要求不同： sleep() 可以在任何需要的场景下调用。 wait() 必须使用在同步代码块或同步方法中</font>
   3. <font color='#FF0000'>关于是否释放同步监视器，如果两个方法都使用同步代码块或同步方法中，sleep() 不会释放锁， wait(） 会释放锁</font>

![image-20220224194802472](D:\公式教程1\Typora\picture\image-20220224194802472.png)

```Java
    package gk;
    class Clerk{
        private int proudctCount = 0;

        public synchronized void cosumeProduct()  {
            if(proudctCount > 0){
                System.out.println(Thread.currentThread().getName()+"正在消费第"+ proudctCount + "个产品");
                proudctCount --;
                notify();
            }else{
                try {
                    wait();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }

        public synchronized void produceProduct()  {
            if(proudctCount < 20){
                proudctCount ++;
                System.out.println(Thread.currentThread().getName()+"正在生产第"+ proudctCount + "个产品");
              	notify();
            }else{
                try {
                    wait();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    class producer implements Runnable{
        private Clerk clerk;
        public producer(Clerk clerk) {
            this.clerk = clerk;
        }

        @Override
        public  void run() {
            System.out.println(Thread.currentThread().getName()+"开始生产");
            while(true){
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                clerk.produceProduct();
            }
        }
    }
    class Cosumer implements Runnable{
        private Clerk clerk;

        public Cosumer(Clerk clerk) {
            this.clerk = clerk;
        }

        @Override
        public  void run() {
            System.out.println(Thread.currentThread().getName()+"开始消费");
            while(true){
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                clerk.cosumeProduct();
            }
        }
    }

    public class ProductTest {
        public static void main(String[] args) {
            Clerk clerk = new Clerk();
            producer p = new producer(clerk);
            Thread t1 = new Thread(p);
            t1.setName("生产者1");
            Cosumer cosumer = new Cosumer(clerk);
            Thread c1 = new Thread(cosumer);
            c1.setName("消费者1");
            t1.start();
            c1.start();
        }
    }

```

# JDK5.0 ——创建线程的俩个新方法

## 三 ： 实现 Callable 方法 

```java
	//1、创建一个实现Callable的实现类
	class NumThread implments Callable{
        //2、实现call方法，将此线程所需要执行的操作声明在call()中
        @Override 
        public Object call() throws Exception {
            int sum = 0;
            for(int i = 1; i <= 100; i++){
                System.out.println(i);
                sum += i;
            }
        }
        return sum;
    }
	public class ThreadNew {
        public static void main(String[] args){
            //3、创建Callable接口实现类的对象
            NumThread unmThread = new NumThread();
            //4、将此Callable接口实现类的对象作为参数传递到 FutureTask 类的构造器中，创建 FutureTask 的对象
            FutureTask futureTask = new FutureTask(numThread);
            //将 FutureTask 的对象作为参数传递到 Thread 类的构造器中，创建 Thread 类的对象，并调用start()
            new Thread(futureTask).start();
            try{
                //6、获取 Callable 中的call方法的返回值，get()返回值即为 FUtureTask 构造器参数 Callable 实现类重写的 call() 的返回值 
                Object sum = futureTask.get();
                System.out.println("总和为："+ sum);
            }catch (InterruptedException e){
                e.printStackTrace();
            }catch (ExecutionException e){
                e.printStackTrace();
            }
        }
    }
```

### 如何理解实现 Callable 接口的方式创建多线程比实现 Runnable 接口创建的多线程方式强大？

1.  <font color='#FF0000'>call() 可以有返回值</font>
2. call() <font color='FFA500'>可以抛出异常</font>，被外面的操作捕获，获取异常信息
3. <font color='#FF0000'>call() 是支持泛型的</font>

## 四 ：使用线程池

 ![image-20220225221740385](D:\公式教程1\Typora\picture\image-20220225221740385.png)

![image-20220225221822497](D:\公式教程1\Typora\picture\image-20220225221822497.png)

```Java
	class NumberThreadone implements Runnable{
        @Override 
        public void run(){
            for(int i = 0; i <= 100; i++){
                if(i%2 == 0){
                    System.out.println(Thread.currentThread().getName() + ":"+ i);
                }
            }
        }
    }
	class NumberThreadtwo implements Runnable{
        @Override 
        public void run(){
            for(int i = 0; i <= 100; i++){
                if(i%2 != 0){
                    System.out.println(Thread.currentThread().getName() + ":"+ i);
                }
            }
        }
    }
	public class ThreadPool {
		public static void main(String[] args){
            //1、提供固定容量的线程池
            ExecutorService service = Executors.newFixedThreadPool(10);
            //设置线程池的属性(拓展)
            ThreadPoolExecutor service1 = (ThreadPoolExecutor) service;
            service1.setCorePoolSize(15);//设置核心池大小，还有setKeepAliveTime()等属性
            //2、执行，需要提供实现Runnable（或Callable）接口实现类的对象
            service.execute(new NumberThreadone());//适用于Runnable
            service.execute(new NumberThreadtwo());//适用于Runnable
            
            //service.submit();适用于Callable
            
            //3、关闭连接池
            service.shutdown();
        }
    }
```

