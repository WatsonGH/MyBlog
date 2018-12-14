## 泛型(Generic) ##
>泛型是Java SE 1.5的新特性，泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。这种参数类型可以用在类、接口和方法的创建中，分别称为泛型类、泛型接口、泛型方法。<br/><br/>
>用于类:<br/>
><pre>public class Generic&lt;T&gt;{}</pre>
>限定泛型的父类:<br/>
><pre>public class Generic&lt;T extends Activity&gt;{}</pre>
>用于接口:<br/>
><pre>public interface IGeneric&lt;T&gt;{}
>public interface IGeneric&lt;T extends Activity&gt;{}</pre>
>用于方法:<br/>
><pre>public &lt;T&gt; Integer genericMethod(T t);
>public &lt;T extends String&gt; Integer genericMethod(T t);</pre>    
>**总结**：
>
>1. 泛型只能在一个类，接口，方法里面声明；声明格式 &lt;T&gt;<br/>
>2. 方法上声明的泛型和类上声明的泛型可以是同一个&lt;T&gt;，互不影响，一般最好用不同的字母区别开<br/><br/>
>
>**泛型擦除：**对于运行的虚拟机来说，其实并不存在泛型。java源文件在编译成字节码文件的过程中会把声明的泛型擦除并且把泛型的引用替换成Object，并进行引用上的强转。所以class里面不会存在泛型的任何信息<br/><br/>
>
>**创建泛型类以及泛型擦除之后的一些问题：**https://www.cnblogs.com/drizzlewithwind/p/6101081.html


## 反射 ##
>**定义：**Java反射就是在程序运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；并且能改变它的属性。说白了。就是javaAPI里面提供了接口能让我们拿到对应的java虚拟机运行的字节码文件，这个文件信息就封装在Class对象中，拿到这个Class对象之后进行的一些api调用拿到字段和方法，这种技术就是反射。<br/><br/>
>**Class对象获得的几种方法**：<br/>
>1.Class clazz = Class.forName("java.lang.Object");<br/>
>2.Class clazz = Object.class;<br/>
>3.Class clazz = 实体对象.getClass();<br/>
>**切记：Class<Person> personClass = Person.class;  //Person.class拿到的其实是带有泛型的Class&lt;Person&gt;，是由JVM虚拟机来加载的并封装到Class对象的。**

>得到Class对象之后再反射得到构造函数、字段、方法、注解信息<br/><br/>
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

>注解：待考证：是不是运行时期的注解才能拿到？
><pre>
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



>1.如果用getDeclaredXx去获取public修饰的方法、字段、构造方法也是可行的，反过来如果用getXx去获取私有的方法、字段、构造方法将会返回
NoSuchMethodException(构造和方法)、NoSuchFieldException(字段)<br/><br/>
>2.反射到的构造方法可用于创建对象、成员可以取值、方法可以调用


## 注解 ##
>注解(Annotation)是一种应用于类、方法、参数、变量、构造器及包声明中的特殊修饰符。<br/>Java SE5内置了三种标准注解：<br/>
><pre>@Override:只能用于方法上，表示当前的方法定义将覆盖超类中的方法。
@Deprecated，使用了注解为它的元素编译器将发出警告，因为注解@Deprecated是不赞成使用的代码，被弃用的代码。
@SuppressWarnings，关闭不当编译器警告信息。
</pre>

>创建注解用@interface符号，其前面也可以加上修饰符public/private等，java还提供了元注解来进行修饰自定义的注解
![4种元注解的作用](https://i.imgur.com/SR6NXli.png)






## Java八种基本数据类型（Primitive Type） ##
**byte：**占用1个字节，8位，取值范围：<br/>
**short：**占用2个字节，16位<br/>
**int：**占用4个字节，32位<br/>
**long：**占用8个字节，64位<br/>
**float：**<br/>
**double：**<br/>
**boolean：**<br/>
**char：**<br/>



<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
同步机制的方式，原理，缺点
ThreadLocal
常用的集合又那些？各个集合的区别?
java常用的关键字
注解
dragger

