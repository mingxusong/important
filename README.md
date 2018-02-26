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
    各种类型的通道,它们表示到能够执行 IO 操作的实体的连接;以及选择器 和选择键,它们与可选择信道 一起定义了多路的 无阻塞的 I/O 设施

		

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
 
 
 
        加载:由类加载器执行,查找字节码并从这些字节码中创建一个class对象
    	链接:验证类中的字节码,为静态域分配空间,解析这个类创建的对其他类的所有引用
    	初始化:如果该类具有超类,则对其初始化,执行静态初始化器和静态初始化块.初始化被元迟到了对静态方法(构造器隐式地是静态的)或者非常数静态域进行首次引用时才执行

#### 14.描述动态代理的几种实现方式,分别说出相应的优缺点

