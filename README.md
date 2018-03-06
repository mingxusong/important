#### 1. JAVA 中的几种基本数据类型是什么,各自占用多少字节
* short   2字节 16位
* int     4字节 32位
* lang    8字节 64位
* byte    1字节  8位
* char    2字节 16位
* boolean 1字节  8位
* float   4字节 32位
* double  8字节 64位

#### 2. String 类能被继承吗,为什么
* 不能
* String类声明 public final class
* final修饰类表示不可被继承


#### 3. String,StringBuffer,StringBuilder的区别
* String 数据类型 使用char数组实现 拼接操作等会返回新的对象
* StringBuffer,StringBuilder 类String数据类型 使用char数组实现 拼接操作等不会返回新的对象
* StringBuffer中函数加有synchronized关键字 多线程安全
* StringBuilder中函数没有synchronized关键字 多线程不安全
* synchronized关键字表示程序中最多只有一个synchronized关键字程序运行,其他带有synchronized关键字程序需要等到前一个synchronized关键字程序运行完成才能运行

#### 4. ArrayList 和 LinkedList 有什么区别
1. ArrayList 
    * 线性结构
        * 一个有序数据元素的集合
2. LinkedList 
    * 链表 
        * 元素之间通过前驱后继关联

#### 5. 讲讲类的实例化顺序,比如父类静态数据,构造函数,字段,子类静态数据,构造函数,字段,当 new 的时候,他们的执行顺序.
1. 父类静态块
2. 父类静态属性
3. 子类静态块
4. 子类静态属性
5. 父类属性
5. 父类构造函数
6. 子类属性
7. 子类构造函数


#### 6. 用过哪些 Map 类,都有什么区别,HashMap是线程安全的吗,并发下使用的 Map 是什么,他们内部原理分别是什么,比如存储方式,hashcode,扩容,默认容量等.
* TreeMap
	* 红黑树
* HashMap
	* 散列表
		* 通过hash方法计算关键值保存到一个数组中
		* 相同hash冲突采用拉链法解决冲突
		* 当哈希表中的条目数超出了加载因子与当前容量的乘积时进行扩容操作
	    * 默认容量 20	
		* 默认加载因子 7.5
* HashTable
	* 散列表
	* 除了同步运行和key&value不能为空之外与hashMap一致
* ConcurrentHashMap
	* 类似于hashTable,通过CAS(Compare and swap)控制线程安全
* LinkedHashMap 
	* HashMap子类
		* 保存前一个节点和后一个节点
		* 通过重写父类插入移除Entry(Entry&Node)后修改本地节点链表

#### 7.JAVA8 的 ConcurrentHashMap 为什么放弃了分段锁,有什么问题吗,如果你来设计,你如何设计
* 分段锁:一部分数据使用一把锁
* 1.8之后使用CAS(Compare and swap),基于CPU指令实现多线程锁


#### 8.有没有有顺序的 Map 实现类,如果有,他们是怎么保证有序的.
* LinkedHashMap
	* 继承于HashMap,通过重写HashMap的afterNodeAccess方法和afterNodeInsertion从而实现将数据加入链表

#### 9.象类和接口的区别,类可以继承多个类么,接口可以继承多个接口么,类可以实现多个接口么.
* 类:


        不可以继承多个类
        可以实现多个接口
        关键字 class
        属性和方法可以是所有访问修饰符


* 接口:


	    不可以继承多个接口
	    关键字 interface
	    方法修饰符只能是public
	    属性修饰符为只能为 public static final
	    不可以实现方法

#### 10.继承和聚合的区别在哪
* 继承:
    * 使用或实现重写父类或者超类提供的方法实现业务
* 聚合:
	* 组合多个类的方法实现业务

#### 11.讲讲你理解的 NIO
* java IO 模型之一
    * 面向缓冲区,同步非阻塞IO模型
    * Selector监听通道事件
    * 核心组件:通道,缓冲区,选择器
    * 数据从通道进入缓冲区
    
    
          NIO API 的集中抽象为缓冲区,它们是数据容器字符集及其相关解码器和编码器,它们在字节和 Unicode 字符之间进行转换
          各种类型的通道,它们表示到能够执行 IO 操作的实体的连接;
	      以及选择器和选择键它们与可选择信道 一起定义了多路的 无阻塞的 I/O 设施

		

#### 12.反射的原理,反射创建类实例的三种方式是什么.
* 反射原理
    * 每当编写并且编译了一个新类就会产生一个Class对象(被保存在一个同名.class文件中)
    * 在运行时打开和检查.class文件
    * 通过Class对象找到某一个类中的方法以及属性等

* 反射创建类实例


        Class.forName().newInstance();
        ClassLoader.loadClass().newInstance();
        类名.class.newInstance();
    
 #### 13.反射中,Class.forName 和 ClassLoader 区别
* 当使用.class来创建对Class对象的引用时,不会自动初始化该Class对象.为了使用类而做的准备工作包括三个步骤
    * Class.forName得到的class是已经初始化完成的
    * Classloader.loaderClass得到的class是还没有链接的
 
 
 
          1.加载:由类加载器执行,查找字节码并从这些字节码中创建一个class对象
    	  2.链接:验证类中的字节码,为静态域分配空间,解析这个类创建的对其他类的所有引用
    	  3.初始化:如果该类具有超类,则对其初始化,执行静态初始化器和静态初始化块.
	      初始化被元迟到了对静态方法(构造器隐式地是静态的)或者非常数静态域进行首次引用时才执行

#### 14.描述动态代理的几种实现方式,分别说出相应的优缺点

    以二进制形式修改已有类或者动态生成类,在类被加载入 Java 虚拟机之前动态改变类行为

* JDK
    * java原生动态代理
    * 运行速度慢
* Javassist
    * 没有类型检查
    * 没有泛型支持
    * 没有自动封包差包
    * 运行速度较快
* CGLIB
    * 会导致PermGen内存泄露
    * 运行速度块
    
#### 15.动态代理与CGLIB实现的区别
* JDK
  * 定义一个功能接口，然后让代理和来实现这个接口  
* CGLIB
  * 通过继承.代理继承自被代理类中的方法,这样代理则拥有了被代理类中的的功能,代理还可以通过重写被代理类中的方法,来实现多态.
  
#### 16.为什么CGlib方式可以对接口实现代理.

    通过继承.代理继承自被代理类中的方法,这样代理则拥有了被代理类中的的功能,代理还可以通过重写被代理类中的方法,来实现多态.

#### 17.final 的用途
* 修饰属性表示常量
* 修饰类表示不可被继承
* 修饰方法表示不可被重载

#### 18.写出三种单例模式实现
* 懒汉模式
    
    
    	public class Singleton {  
        	private static Singleton instance = null;  
        	private Singleton(){}  
        	public static Singleton getInstance() {  
            	if (instance == null) {  
                	synchronized (Singleton.class) {  
                    		if (instance == null) {
                        		instance = new Singleton();  
                    		}  
                	}  
            	}  
        	return instance;  
        	}  
    	}
        
* 饿汉模式


    	public class Singleton{  
        	private static Singleton instance = new Singleton();  
        	private Singleton(){}  
        	public static Singleton newInstance(){  
            		return instance;  
        	}  
    	}
    
* 枚举模式


    	public enum Singleton{  
        	instance;  
        	public void doSomething(){}      
    	}  

#### 19.如何在父类中为子类自动完成所有的 hashcode 和 equals 实现?这么做有何优劣
* 子类不实现hashcode和equals默认调用父类方法
* 父类设置公共参数,为公共参数实现hashcode和equals
    * 优点
        * 子类无需实现hashcode和equals
    * 缺点
        * 无法根据子类特定属性实现hashcode和equals
        

#### 20.请结合 OO 设计理念,谈谈访问修饰符 public private protected default 在应用设计中的作用
* public
    * 所有类可用
    * 有被所有对象知情的重要性
* private
    * 只有自身类可用
    * 只有自身对象依赖对其他对象没有使用用处或者其他对象不需要知情
* protected
    * 子类可用
    * 不想被其他类直接引用但是可被子类复写或者被子类使用,对其它对象用处不大
* default
    * 子类和同一个包下的类可用
    * 相同包下对象和子类需要使用或者需要感知到
    
#### 21.深拷贝和浅拷贝区别


        同为拷贝内容,但浅拷贝被拷贝对象的内容与拷贝对象内容同为一个引用,深拷贝拷贝对象会创建新的引用存放被拷贝对象内容
        
#### 22.数组和链表数据结构描述,各自的时间复杂度
* 数组
    * 线性结构实现
    * 逻辑存储顺序与物理存储顺序一致
    * 长度固定
* 链表
    * 链式存储结构
    * 逻辑存储顺序与物理存储顺序不一致,需要记录元素前驱后继记录元素逻辑位置
    * 长度可变

#### 23.error和exception的区别,CheckedException,RuntimeException的区别
* error
    * 程序无法处理的错误,发生于虚拟机自身或虚拟机试图执行应用,可能会导致中断线程
* exception
    * 操作或操作可能会引发的错误,可以被程序处理
    * CheckedException
        * 检查型异常,强制要求必须做异常处理
    * RuntimeException
        * 运行时异常,因操作引发的异常,不要求强制做异常处理

#### 24.请列出5个运行时异常
* NullPointException 
    * 空指针异常
    * 调用对象为null的时候发生
* IndexOutOfBoundsException
    * 数组下标越界一场
    * 获取对象下标超出数组长度时
* ClassCastException
    * 类转换异常
    * 类型转换时类型不属于父子类或同一个类型时
* IllegalArgumentException
    * 非法参数异常
    * 函数需要参数与传递参数不符时 
* UnsupportedOperationException
    * 不支持操作异常
    * 调用函数不存在时

#### 25.在自己的代码中,如果创建一个java.lang.String对象,这个对象是否可以被类加载器加载?为什么
* 不可以
* jdk类加载器 启动类加载器(bootstrap)会将Java_Home/lib下面的类库加载到内存中,所以自己创建的java.lang.String对象无法被加载

#### 26.说一说你对java.lang.Object对象中hashCode和equals方法的理解.在什么场景下需要重新实现这两个方法.
* equals
    * 进行非引用判断对象是否一致
    * 当使用属性或特殊方法判断对象是否一致时重新实现
* hashcode
    * 计算hashcode
    * 当需要在使用hash存储时为了让元素更分散或更密集时重新实现

#### 27.在jdk1.5中,引入了泛型,泛型的存在是用来解决什么问题


        泛型实现了参数化类型的概念,使代码可以应用于多种类型.
        最初的目的是希望类或方法能够具备最广泛的表达能力.

#### 28.这样的a.hashcode()有什么用,与a.equals(b)有什么关系
* a.hashcode()
    * 获取当前hashcode值
* a.equals(b)
    * 如果equals返回true按hashcode常规协定两个对象将会返回同一个hashcode值


        hashcode常规协定
        在 Java 应用程序执行期间,在对同一对象多次调用 hashCode 方法时，必须一致地返回相同的整数,前提是将对象进行 equals 比较时所用的信息没有被修改.从某一应用程序的一次执行到同一应用程序的另一次执行,该整数无需保持一致.
        如果根据 equals(Object) 方法,两个对象是相等的,那么对这两个对象中的每个对象调用 hashCode 方法都必须生成相同的整数结果.
        如果根据 equals(java.lang.Object) 方法,两个对象不相等,那么对这两个对象中的任一对象上调用 hashCode 方法不 要求一定生成不同的整数结果.但是，程序员应该意识到,为不相等的对象生成不同整数结果可以提高哈希表的性能.
