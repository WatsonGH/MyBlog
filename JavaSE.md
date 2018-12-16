## 泛型(Generic) ##
>泛型是Java SE 1.5的新特性，**泛型的本质是参数化类型**，也就是说所操作的数据类型被指定为一个参数。这种参数类型可以用在类、接口和方法的创建中，分别称为泛型类、泛型接口、泛型方法。
>
>**泛型的声明(定义)，可同时定义多个：<泛型类型的变量符>，例如：&lt;T&gt;、&lt;T,E&gt;**
>
>用于类
><pre>public class Generic&lt;T&gt;{}</pre>限定泛型的父类
><pre>public class Generic&lt;T extends Activity&gt;{}</pre>用于接口
><pre>public interface IGeneric&lt;T&gt;{}
>public interface IGeneric&lt;T extends Activity&gt;{}</pre>用于方法
><pre>public &lt;T&gt; Integer genericMethod(T t);
>public &lt;T extends String&gt; Integer genericMethod(T t);</pre>    
>**总结**：
>1. 泛型只能在一个类，接口，方法里面声明；声明格式 &lt;T&gt;
>2. 方法上声明的泛型和类上声明的泛型可以是同一个&lt;T&gt;，互不影响，一般最好用不同的变量字符区别开
>
>**泛型擦除**：对于运行的虚拟机来说，其实并不存在泛型。java源文件在编译成字节码文件的过程中会把声明的泛型擦除并且把泛型的引用替换成Object，并进行引用上的强转。所以class里面不会存在泛型的任何信息
>
>**创建泛型类以及泛型擦除之后的一些问题**：https://www.cnblogs.com/drizzlewithwind/p/6101081.html


## 反射 ##
>**定义**：
>Java反射就是在程序运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；并且能改变它的属性。说白了。就是javaAPI里面提供了接口能让我们拿到对应的java虚拟机运行的字节码文件，这个文件信息就封装在Class对象中，拿到这个Class对象之后进行的一些api调用拿到字段和方法，这种技术就是反射。
>
>**Class对象获得的几种方法**：
>
1. Class clazz = Class.forName("java.lang.Object");
2. 2.Class clazz = Object.class;
3. Class clazz = 实体对象.getClass();

>**切记：上面三种获取方式拿到的Class对象都默认带有泛型的，即Class&lt;Object&gt;;比如Person.class拿到的其实是带有泛型的Class&lt;Person&gt;，是由JVM虚拟机来加载的并封装到Class<T>对象的。**
>
>得到Class对象之后再反射得到构造函数、字段、方法、注解信息
>构造方法：
><pre>
>//获取private私有的构造方法(构造方法即使是私有的也能创建对象)，int.class是一个引用，JVM运行时，int类型Class对象已经建立，通过int.class来引用
>Person.class.getDeclaredConstructor(String.class,int.class)
>//获取public公开的构造方法
>Person.class.getConstructor(String.class,int.class)
></pre>
>字段：
><pre>
>//获取private私有成员变量
>Person.class.getDeclaredField("name")
>//获取public公开的成员变量
>Person.class.getField("name")
></pre>
>方法：
><pre>
>//获取private私有的方法
>personClass.getDeclaredMethod("getName",String.class)
>//获取public公开的方法
>Person.class.getMethod("getName",String.class)
></pre>
>注解：
><pre>
>//只能是运行时期的注解才能通过反射获取到
>//类上的注解
>Person.class.getAnnotation(Deprecated.class)
>//方法上的注解
>Person.class.getMethod("getName").getAnnotation(Deprecated.class)
>//方法或者构造方法上的参数注解
>Person.class.getMethod("getName").getParameterAnnotations()[0][0]
>//字段上的注解
>Person.class.getField("name").getAnnotation(Deprecated.class)
>//构造方法上的注解
>Person.class.getConstructor("Person").getAnnotation(Deprecated.class)
>//包名上的注解
>Person.class.getPackage("Person").getAnnotation(Deprecated.class)
></pre>
>
>**注意**：
>**1. 如果用getDeclaredXx去获取public修饰的方法、字段、构造方法也是可行的，反过来如果用getXx去获取私有的方法、字段、构造方法将会返回NoSuchMethodException(构造和方法)、NoSuchFieldException(字段)**
>
>**2. 反射到的构造方法可用于创建对象、成员可以取值、方法可以调用**



## 注解 ##
>注解(Annotation)是一种应用于类、方法、方法参数、变量、构造器及包声明中的特殊修饰符。是java 5的新特性之一。Java SE5内置了三种标准注解
><pre>
>@Override: 只能用于方法上，表示当前的方法定义将覆盖超类中的方法。
>@Deprecated: 使用了注解为它的元素编译器将发出警告，因为注解@Deprecated是不赞成使用的代码，被弃用的代码。
>@SuppressWarnings: 关闭不当编译器警告信息。
></pre>

>**1.创建注解**
>创建注解用@interface符号，其前面也可以加上修饰符public/private等，java还提供了元注解来进行修饰自定义的注解
>![4种元注解的作用](https://i.imgur.com/SR6NXli.png)
>
>**2.声明注解的属性**
>注解里面只存在属性，用于记录固定的数据值
><pre>
>@Target({ElementType.METHOD,ElementType.PARAMETER})
>@Retention(RetentionPolicy.CLASS)
>public @interface MyAnnoation {
    int id() default 1;
    String[] name() default {"zhangsan","lisi"};
    RetentionPolicy enum;
>}
></pre>
>
>可以发现在定义属性方面和在接口上定义方法很相似(定义注解属性可以加上default)，上面定义了一个MyAnnoation注解，并且为其定义了三个属性并赋予了默认的值
>
>**①注解属性的类型必须是：八种基本数据类型和枚举类型**
>**②如果注解的属性在定义时没有赋值默认值，则在使用注解时，必须指定该属性的值，如果有默认值，可不赋值**


## 枚举（enumeration） ##
>枚举其实就是一个类，用关键字enum来定义而不是class，父类默认是继承Enum抽象类(实现了Serializable可用于序列化)，而Enum又继承了Object，所以枚举实质上就是一个类。不同于类的特点是其构造方法默认是私有的(编译器默认私有化)，所以这个类只能在内部创建好固定数量的对象提供给外面使用。特点：
>
>**1.构造方法私有，不能在外部创建**
>**2.只能在类内部创建自身对象提供外部访问**
>**3.能实现其他接口，不能再继承其他类，因为已经继承了java.lang.Enum**
>**4.枚举不能被继承，因其构造方法是私有的，创建子类枚举时无法调用父类枚举的构造方法，导致无法继承，实在要继承只能通过内部类的方式**

## Java数据类型（Primitive Type） ##

>**Java是强类型语言，强类型语言也称为强类型定义语言。是一种总是强制类型定义的语言，要求变量的使用要严格符合定义，所有变量都必须先定义后使用。Java中的数据类型分为基本数据类型和引用数据类型。jvm会根据不同的数据类型来开辟不同的内存空间**
>**八种数据类型：**
>**byte**：Java中最小的数据类型，在内存中占8位(bit)，即1个字节，取值范围-128~127，默认值0
>**short**：短整型，在内存中占16位，即2个字节，取值范围-32768~32717，默认值0
>**int**：整型，用于存储整数，在内在中占32位，即4个字节，取值范围-2147483648~2147483647，默认值0
>**long**：长整型，在内存中占64位，即8个字节-2^63~2^63-1，默认值0L
>**float**：浮点型，在内存中占32位，即4个字节，用于存储带小数点的数字（与double的区别在于float类型有效小数点只有6~7位），默认值0
>**double**：双精度浮点型，用于存储带有小数点的数字，在内存中占64位，即8个字节，默认值0
>**char**：字符型，用于存储单个字符，占16位，即2个字节，取值范围0~65535，默认值为空
>**boolean**：布尔类型，占1个字节，用于判断真或假（仅有两个值，即true、false），默认值false
>
>**引用数据类型：**
>引用数据类型分3种：类，接口，数组
>
>**变量：**
>变量分为两个部分，变量类型（数据类型）和变量名，String s；String即为变量类型，s则为变量名，这样就定义好了一个名为s的变量，从变量字面意思就可以理解到他的值是不固定的，在不同的时间变量可能指向不同的值，由开发者来指定。

## JVM内存分配机制 ##

同步机制的方式，原理，缺点
ThreadLocal
常用的集合又那些？各个集合的区别?
java常用的关键字
注解
dragger

