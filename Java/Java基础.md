# 面向对象和面向过程的区别
面向对象易维护、易复用、易拓展，因为面向对象有封装、继承、多态的特点，但是性能比面向过程低。

# Java和C++的区别
都是面向对象的语言，支持封装、继承、多态。  
Java没有指针用来直接访问内存。  
Java类只能单继承，C++可以多继承。  
Java有自动内存管理机制，不用手动释放无用内存。  

# 基本数据类型
boolean/~  Boolean  
byte/8  Byte  
short/16  Short  
int/32  Integer  
long/64  Long  
char/16  Character  
float/32  Float  
double/64  Double  

# 重载和重写
重载即方法名相同，参数列表不同（类型，个数）。  
重写即子类对父类可允许访问的方法进行重新编写，方法名和参数必须相同，返回值范围小于父类，抛出异常范围小于父类，访问修饰符范围大于或等于父类。  
如果父类的方法被private修饰，则子类不能重写。  

# 封装、继承、多态
封装即把一个对象的私有化，只提供给外界访问的方法。  
继承即子类继承父类，子类拥有父类的所有属性和方法，但是私有类无法访问。子类可以拓展出自己的属性和方法。子类可以重写父类的方法。  
多态即引用变量所指向的对象或调用的方法，在编程时不确定，而是在运行时才确定。实现多态一般通过继承和接口，如用父类引用指向子类对象并调用重写父类的方法，那只有在运行时才知道时调用的是哪个重写的方法。  

# String、StringBuffer、StringBuilder
String是不可变的，因为使用了final修饰字符数组。  
StringBuffer、StringBuilder都继承AbstractStringBuilder类，都可变，因为它们的字符数组没有用final修饰。  
String不可变，即常量，线程安全。  
StringBuffer有同步锁，线程安全。  
StringBuilder没有锁，线程不安全。  

# 装箱与拆箱
装箱：将基本数据类型包装成引用类型。  
拆箱：包装器类型转换为基本数据类型。  
基本数据类型不是面向对象，包装类即将其转化为对象，方便操作。  

# equals()和==，以及hashcode()
==：判断两个对象是否是同一对象，即比较地址。如果是基本数据类型则比较值。  
equals：如果类没有重写，则与==相等。    
        如果重写了，一般是比较两个对象的值是否相等。  
hashcode：如果两个对象相等，则hashcode也相等，反之不一定。  
即hashcode也和equals一样，没重写也是通过地址来得到哈希码，重写了才通过值。  
所以，在散列表中加入两个拥有相同值的不同对象时，不仅要重写equals，还要重写hashcode，才能避免重复元素的加入。  

# final
final修饰的变量初始化后不能修改，修饰的类不能被继承，修饰的方法不能重写。  

# static
静态方法或静态内部类只能访问所属类的静态变量和方法，方法中不能有this和super关键字。  
静态语句块只在类初始化时执行一次。  
非静态内部类依赖于外部类，即需要先实例化外部类后，才能用该实例去创建内部类。静态内部类则不用，能直接创建。  

初始化顺序：  
静态代码（静态变量，静态代码块）优先于非静态代码，最后才是构造方法。  
有继承的情况下：父类静态代码>子类静态代码>父类非静态>父类构造方法>子类非静态>子类构造方法。  

# 异常类
Java的异常主要有两类，Exception和Error，都继承自Throwable类。  
Error：程序无法处理的错误。如虚拟机运行错误（Virtual MachineError）和内存溢出（OutOfMemoryError）等。  
Exception：程序能处理的异常。如RuntimeException，NullPointerException，ArrayIndexOutOfBoundsException。  

异常处理：  
try块：捕获异常，后面跟0个或多个catch块，没有carch则必须跟finally块。  
carch块：处理捕获的异常。  
finally块：最后肯定执行的块，如其他块有return语句，则会在return前被执行。如都有return，依旧会在return前执行，并且finally里的返回值会覆盖原始返回值。  

# transient
不想序列化的变量，用transient修饰。只能修饰变量，不能修饰方法和类。  

# 浅拷贝与深拷贝
浅拷贝：只拷贝引用对象，即两个引用指向同一对象。  
深拷贝：创建新对象，并复制其内容。即两个相同内容的不同对象。  

# 访问权限修饰符
private、protected、public，不加访问修饰符即包级可见。  

# 抽象类和接口
抽象类用abstract声明，如果一个类包含抽象方法，则该类必须为抽象类。不能被实例化，只能被继承。  
接口的字段和方法默认为public，且默认为static和final，不能为private和protected。  

# 反射
在运行时获取程序中类的信息，即jvm在运行时才动态加载类或调用和访问方法。  
通过反射获取某个方法后，可以用invoke（）来调用方法。  

# 代理类Proxy  
loader: 代理对象的类加载器  
interfaces: 代理对象实现的接口列表  
h: 调用处理器  
Proxy.newProxyInstance(ClassLoader loader, Class<?>[] interfaces, InvocationHandler h);

