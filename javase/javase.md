#  快速入门
##  一个最简单的Java程序在windows是如何运行的？

1. 首先我们编写一段Java源代码 保存后文件的后缀是.java,例如保存的文件时HelloWorld.java

2. 然后 我们通过命令行 使用javac HelloWorld.java的命令来编译这个Java源文件。这时候会生成HelloWorld.class  文件，这个是Java字节码

   <!--注意：在使用这条命令前，我们要先到该文件所在的目录，不然找不到这个文件。同时这条命令是用来编译Java源文件的，所以我们应该提前下载jdk，jdk中含有Java的编译器-->

3. 然后我们使用命令 java HelloWorld就可以直接运行Java程序了，这一步其实就是JVM执行字节码

## 在这个一个Java程序运行过程中，生成的各种后缀文件的意义
- 编写后保存为 .Java文件 是源代码
- 使用javac编译器 来编译后生成 的.class文件是字节码
- 有了字节码之后，用命令java 类名 就可以直接运行Java程序了
- 但是，当有多个字节码的时候，我们可以用jar命令打包这些字节码，生成的文件后缀是.jar ，相当于压缩包 。想运行.jar 文件，我们用命令 java -jar运行
- jar 是Java archive 的缩写，意思是Java归档文件，是基于zip格式的文件规范


## jdk jre jvm的关系与区别
- jdk java development kit Java开发工具包
- jre Java runtime environment Java运行环境
- jvm Java virtual machine java 虚拟机

简单来说 开发需要jdk 而运行只需要用到jre，或者包含jre的jdk
以前jdk和jre是分开的，现在的jdk都是包含jre的
他们的关系是 jdk最大，包含jre ，jre包含jvm 。jvm是最小的

- 具体的介绍
jdk包含jre和开发工具（编译器，调试器等）
jre 包含jvm 和 Java程序运行所需要的核心类库
jvm Java虚拟机负责运行Java字节码
一个jar文件可能要用到核心类库的东西，所有只有一个jvm是不够的

## 什么是javaSE
JavaSE（Java Platform, Standard Edition）是 Java 技术体系的核心组成部分，也是 Java 生态的基础。它定义了 Java 语言的标准特性和基础类库，为开发桌面应用、命令行工具、网络应用等提供底层支持。
Java 技术体系分为三个主要平台：

- JavaSE（标准版）：提供基础 API（如字符串处理、集合框架、输入输出、多线程、网络编程等），是 JavaEE 和 JavaME 的基础。
- JavaEE（企业版）：基于 JavaSE，扩展了企业级功能（如 Servlet、JSP、EJB、JPA 等），用于开发 Web 应用和分布式系统。
- JavaME（微型版）：针对嵌入式设备（如手机、机顶盒）优化，现已被 Android 平台取代。



JavaSE 包含以下关键组件：



- **Java 语言规范**：定义语法（如类、接口、继承、泛型、Lambda 表达式等）。
- **Java 虚拟机（JVM）**：执行字节码的运行环境。
- 核心类库（Java API）
  - **java.lang**：基础类（如`Object`、`String`、`Thread`）。
  - **java.util**：集合框架（如`List`、`Map`）、日期时间 API。
  - **java.io** 和 **java.nio**：输入输出和文件操作。
  - **[java.net](https://java.net/)**：网络编程（如`Socket`、`HTTP`客户端）。
  - **java.math**：高精度计算（如`BigDecimal`）。
  - **java.concurrent**：多线程和并发工具。



**什么是API？**api（application programming interface）应用程序接口 ，是一组定义了软件组件之间如何交互的规则、协议和工具。简单来说，API 是软件与软件之间的 “桥梁”，让不同的程序能够互相调用功能、交换数据。



# 面向对象编程（OOP）

## 面向对象基础



### 封装



### 继承



### 多态

- 子类如果定义了一个与父类方法签名完全相同的方法，被成为覆写，也叫重写(Override)

- 加上@Override可以让编译器帮助检查是否进行了正确的覆写。希望进行覆写，但是不小心写错了方法签名，编译器会报错。

- 但是@Override不是必需的

  ``` java 
  // override
    public class Main {
      public static void main(String[] args) {
          Person p = new Student();
          p.run(); // 应该打印Person.run还是Student.run?
      }
    }
  
  class Person {
      public void run() {
          System.out.println("Person.run");
      }
  }
  
  class Student extends Person {
      @Override
      public void run() {
          System.out.println("Student.run");
      }
  }
  ```


  上面的代码，最后p.run()打印的是Student.run
  说明Java的实例方法调用是基于运行时的实际类型的动态调用，而不是变量的声明类型
  这个非常重要的特性在面向对象编程中称之为多态(Polymorphic)
  多态是指，针对某个类型的方法调用，其真正执行的方法取决于运行时期实际类型的方法

### 抽象类
如果父类的一个方法本身没有实现任何功能，只是用来被子类继承，那么这个方法就是一个抽象方法
抽象方法只能放在抽象类中，他们都要用abstract修饰。这种抽象方法和抽象类的作用就是为子类的继承作一种规范。
从抽象类继承的子类必须实现抽象方法
如果不实现抽象方法，则该子类仍是一个抽象类；
例子如下

``` java
// abstract class
public class Main {
    public static void main(String[] args) {
        Person p = new Student();
        p.run();
    }
}

abstract class Person {
    public abstract void run();
}

class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}
```


### 接口
接口是比抽象类更抽象的一种存在
因为如果一个抽象类全是抽象方法，连字段都没有，那么这样的抽象类就可以写成接口
在Java中一个类只能继承一个父类，但是一个类可以实现多个接口。
接口的声明使用关键字interface 接口的使用要用关键字implements。
例子如下：
class Student implements Person {
    private String name;

```java
public Student(String name) {
    this.name = name;
}

@Override
public void run() {
    System.out.println(this.name + " run");
}

@Override
public String getName() {
    return this.name;
}
```
}

### 静态字段和静态方法
在类中定义的字段成为实例字段，每个字段有独立的字段。与之相对，如果一个字段被static修饰，就是静态字段。静态字段在一个类中只有一个共享的空间。
同理，用static修饰的方法就是静态方法。可以通过类名而不通过实例变量调用，类似于其他语言中的函数。
例子如下：
// static method
public class Main {
    public static void main(String[] args) {
        Person.setNumber(99);
        System.out.println(Person.number);
    }
}

class Person {
    public static int number;

```java
public static void setNumber(int value) {
    number = value;
}
```
}


### 包
  为了解决类名冲突的问题，我们使用package来进行区分，package实际上是一种类名空间。真正完整的类名实际上是包名.类名
例如：
小明的Person类存放在包ming下面，因此，完整类名是ming.Person；
小红的Person类存放在包hong下面，因此，完整类名是hong.Person；
小军的Arrays类存放在包mr.jun下面，因此，完整类名是mr.jun.Arrays；
JDK的Arrays类存放在包java.util下面，因此，完整类名是java.util.Arrays。

在定义class的时候，我们需要在第一行声明这个class属于哪个包。
没有定义包名的class，它使用的是默认包
按照包结构把上面的Java文件组织起来。假设以package_sample作为根目录，src作为源码目录，那么所有文件结构就是：

package_sample
└─ src
    ├─ hong
    │  └─ Person.java
    │  ming
    │  └─ Person.java
    └─ mr
       └─ jun
          └─ Arrays.java
即所有Java文件对应的目录层次要和包的层次一致。

bin目录存放编译生成的class文件，文件结构和src目录结构相同
为了避免名字冲突，我们需要确定唯一的包名。推荐的做法是使用倒置的域名来确保唯一性。子包就可以根据功能自行命名。
下面是一个实例的结构
oop-package
└── src
    └── com
        └── itranswarp
            ├── sample
            │   └── Main.java
            └── world
                └── Person.java
Main这个类所在的包名就是com.itranswarp.sample,Main的完整类名就是com.itranswarp.sample.Main。这个sample 就是我们根据功能自行命的名。
### 包的作用域
位于同一个包的类，可以访问包作用域的字段和方法。不用public、protected、private修饰的字段和方法就是包作用域。

#### import
在一个class中，我们总会引用其他的class。例如，小明的ming.Person类，如果要引用小军的mr.jun.Arrays类，他有三种写法：
- 第一种，直接写出完整类名	 mr.jun.Arrays arrays = new mr.jun.Arrays();
- 第二种写法是用import语句，导入小军的Arrays，然后写简单类名。这样就不用老是写完整类名那么麻烦了
  在写import的时候，可以使用*，表示把这个包下面的所有class都导入进来（但不包括子包的class）。因为包没有父子关系。java.util和java.util.zip是不同的包，两者没有任何继承关系。
- 还有一种import static的语法，它可以导入一个类的静态字段和静态方法




### 作用域
在Java中，我们经常看到public、protected、private这些修饰符。在Java中，这些修饰符可以用来限定访问作用域。

### 内部类
在Java程序中，通常情况下，我们把不同的类组织在不同的包下面，对于一个包下面的类来说，它们是在同一层次，没有父子关系：

java.lang
├── Math
├── Runnable
├── String
└── ...
还有一种类，它被定义在另一个类的内部，所以称为内部类（Nested Class）

### classpath和jar
#### classpath
classpath是JVM用到的一个环境变量，它用来指示JVM如何搜索class。
因为Java是编译型语言，源码文件是.java，而编译后的.class文件才是真正可以被JVM执行的字节码。因此，JVM需要知道，如果要加载一个abc.xyz.Hello的类，应该去哪搜索对应的Hello.class文件。
所以，classpath就是一组目录的集合，它设置的搜索路径与操作系统相关。
#### jar包
如果有很多.class文件，散落在各层目录中，肯定不便于管理。如果能把目录打一个包，变成一个文件，就方便多了。

jar包就是用来干这个事的，它可以把package组织的目录层级，以及各个目录下的所有文件（包括.class文件和其他文件）都打成一个jar文件，这样一来，无论是备份，还是发给客户，就简单多了。

jar包实际上就是一个zip格式的压缩文件，而jar包相当于目录。如果我们要执行一个jar包的class，就可以把jar包放到classpath中：

java -cp ./hello.jar abc.xyz.Hello
这样JVM会自动在hello.jar文件里去搜索某个类。
jar包就是zip包，所以，直接在资源管理器中，找到正确的目录，点击右键，在弹出的快捷菜单中选择“发送到”，“压缩(zipped)文件夹”，就制作了一个zip文件。然后，把后缀从.zip改为.jar，一个jar包就创建成功。

假设编译输出的目录结构是这样：

package_sample
└─ bin
   ├─ hong
   │  └─ Person.class
   │  ming
   │  └─ Person.class
   └─ mr
      └─ jun
         └─ Arrays.class
这里需要特别注意的是，jar包里的第一层目录，不能是bin，而应该是hong、ming、mr





## Java核心类

- 学什么？

学习这些核心类，其实就是理解他们各种接口的**概念**，明白这些接口是在**哪种情景**下使用的，为什么被编写出来的。然后再知道他们各自的**实现类**，以及**CRUD**的具体代码实现是怎么写的。

CRUD     create read update delete 增查改删

进阶的学习就是去学习这些操作有哪些效率更高的方法，会有对应的封装，我们要学会如何使用，还要明白为什么效率更高。





# 异常处理

一个健壮的程序必须处理各种各样的错误。

所谓错误，就是程序调用某个函数的时候，如果失败了，就表示出错。

调用方如何获知调用失败的信息？有两种方法：

- 方法一：约定返回错误码。

例如，处理一个文件，如果返回`0`，表示成功，返回其他整数，表示约定的错误码

因为使用`int`类型的错误码，想要处理就非常麻烦。这种方式常见于底层C函数。

- 方法二：在语言层面上提供一个异常处理机制。

Java内置了一套异常处理机制，总是使用异常来表示错误。

异常是一种`class`，因此它本身带有类型信息。异常可以在任何地方抛出，但只需要在上层捕获，这样就和方法调用分离了



因为Java的异常是`class`，它的继承关系如下：

```
                     ┌───────────┐
                     │  Object   │
                     └───────────┘
                           ▲
                           │
                     ┌───────────┐
                     │ Throwable │
                     └───────────┘
                           ▲
                 ┌─────────┴─────────┐
                 │                   │
           ┌───────────┐       ┌───────────┐
           │   Error   │       │ Exception │
           └───────────┘       └───────────┘
                 ▲                   ▲
         ┌───────┘              ┌────┴──────────┐
         │                      │               │
┌─────────────────┐    ┌─────────────────┐┌───────────┐
│OutOfMemoryError │... │RuntimeException ││IOException│...
└─────────────────┘    └─────────────────┘└───────────┘
                                ▲
                    ┌───────────┴─────────────┐
                    │                         │
         ┌─────────────────────┐ ┌─────────────────────────┐
         │NullPointerException │ │IllegalArgumentException │...
         └─────────────────────┘ └─────────────────────────┘
```

从继承关系可知：`Throwable`是异常体系的根，它继承自`Object`。`Throwable`有两个体系：`Error`和`Exception`，`Error`表示严重的错误，程序对此一般无能为力，例如：

- `OutOfMemoryError`：内存耗尽
- `NoClassDefFoundError`：无法加载某个Class
- `StackOverflowError`：栈溢出

而`Exception`则是运行时的错误，它可以被捕获并处理。

某些异常是应用程序逻辑处理的一部分，应该捕获并处理。例如：

- `NumberFormatException`：数值类型的格式错误
- `FileNotFoundException`：未找到文件
- `SocketException`：读取网络失败

还有一些异常是程序逻辑编写不对造成的，应该修复程序本身。例如：

- `NullPointerException`：对某个`null`的对象调用方法或字段
- `IndexOutOfBoundsException`：数组索引越界

`Exception`又分为两大类：

1. `RuntimeException`以及它的子类；
2. 非`RuntimeException`（包括`IOException`、`ReflectiveOperationException`等等）

Java规定：

- 必须捕获的异常，包括`Exception`及其子类，但不包括`RuntimeException`及其子类，这种类型的异常称为Checked Exception。

- 不需要捕获的异常，包括`Error`及其子类，`RuntimeException`及其子类。

  

  注意

  编译器对RuntimeException及其子类不做强制捕获要求，不是指应用程序本身不应该捕获并处理RuntimeException。是否需要捕获，具体问题具体分析

  

# 反射





# 注解



# 泛型

泛型是一种“代码模板”，可以用一套代码套用各种类型。

## 什么是泛型

在讲解什么是泛型之前，我们先观察Java标准库提供的`ArrayList`，它可以看作“可变长度”的数组，因为用起来比数组更方便。

实际上`ArrayList`内部就是一个`Object[]`数组，配合存储一个当前分配的长度，就可以充当“可变数组”：

```java
public class ArrayList {
    private Object[] array;
    private int size;
    public void add(Object e) {...}
    public void remove(int index) {...}
    public Object get(int index) {...}
}
```



如果用上述`ArrayList`存储`String`类型，会有这么几个缺点：

- 需要强制转型；
- 不方便，易出错。

例如，代码必须这么写：

```java
ArrayList list = new ArrayList();
list.add("Hello");
// 获取到Object，必须强制转型为String:
String first = (String) list.get(0);
```



很容易出现ClassCastException，因为容易“误转型”：

```java
list.add(new Integer(123));
// ERROR: ClassCastException:
String second = (String) list.get(1);
```



要解决上述问题，我们可以为`String`单独编写一种`ArrayList`：

```java
public class StringArrayList {
    private String[] array;
    private int size;
    public void add(String e) {...}
    public void remove(int index) {...}
    public String get(int index) {...}
}
```



这样一来，存入的必须是`String`，取出的也一定是`String`，不需要强制转型，因为编译器会强制检查放入的类型：

```java
StringArrayList list = new StringArrayList();
list.add("Hello");
String first = list.get(0);
// 编译错误: 不允许放入非String类型:
list.add(new Integer(123));
```



问题暂时解决。

然而，新的问题是，如果要存储`Integer`，还需要为`Integer`单独编写一种`ArrayList`：

```java
public class IntegerArrayList {
    private Integer[] array;
    private int size;
    public void add(Integer e) {...}
    public void remove(int index) {...}
    public Integer get(int index) {...}
}
```



实际上，还需要为其他所有class单独编写一种`ArrayList`：

- LongArrayList
- DoubleArrayList
- PersonArrayList
- ...

这是不可能的，JDK的class就有上千个，而且它还不知道其他人编写的class。

为了解决新的问题，我们必须把`ArrayList`变成一种模板：`ArrayList<T>`，代码如下：

```java
public class ArrayList<T> {
    private T[] array;
    private int size;
    public void add(T e) {...}
    public void remove(int index) {...}
    public T get(int index) {...}
}
```



`T`可以是任何class。这样一来，我们就实现了：编写一次模版，可以创建任意类型的`ArrayList`：

```java
// 创建可以存储String的ArrayList:
ArrayList<String> strList = new ArrayList<String>();
// 创建可以存储Float的ArrayList:
ArrayList<Float> floatList = new ArrayList<Float>();
// 创建可以存储Person的ArrayList:
ArrayList<Person> personList = new ArrayList<Person>();
```



因此，泛型就是定义一种模板，例如`ArrayList<T>`，然后在代码中为用到的类创建对应的`ArrayList<类型>`：

```java
ArrayList<String> strList = new ArrayList<String>();
```



由编译器针对类型作检查：

```java
strList.add("hello"); // OK
String s = strList.get(0); // OK
strList.add(new Integer(123)); // compile error!
Integer n = strList.get(0); // compile error!
```



这样一来，既实现了编写一次，万能匹配，又通过编译器保证了类型安全：这就是泛型。

**泛型就是编写模板代码来适应任意类型；**

**泛型的好处是使用时不必对类型进行强制转换，它通过编译器对类型进行检查；**

## 使用泛型

编译器如果能自动推断出泛型类型，就可以省略后面的泛型类型。例如，对于下面的代码：

```java
List<Number> list = new ArrayList<Number>();
```



编译器看到泛型类型`List<Number>`就可以自动推断出后面的`ArrayList<T>`的泛型类型必须是`ArrayList<Number>`，因此，可以把代码简写为：

```java
// 可以省略后面的Number，编译器可以自动推断泛型类型：
List<Number> list = new ArrayList<>();
```

### 泛型接口

可以在接口中定义泛型类型，实现此接口的类必须实现正确的泛型类型。

## 编写泛型

编写泛型类比普通类要复杂。通常来说，泛型类一般用在集合类中，例如`ArrayList<T>`，我们很少需要编写泛型类。

如果我们确实需要编写一个泛型类，那么，应该如何编写它？

可以按照以下步骤来编写一个泛型类。

首先，按照某种类型，例如：`String`，来编写类：

```java
public class Pair {
    private String first;
    private String last;
    public Pair(String first, String last) {
        this.first = first;
        this.last = last;
    }
    public String getFirst() {
        return first;
    }
    public String getLast() {
        return last;
    }
}
```



然后，标记所有的特定类型，这里是`String`，把特定类型`String`替换为`T`，并申明`<T>`：

```java
public class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() {
        return first;
    }
    public T getLast() {
        return last;
    }
}
```



熟练后即可直接从`T`开始编写。



# 集合

集合是一种数据结构。<!--一种组织和存储数据的方式 -->

Java 中的 “集合（Collection）” 是用于存储和操作多个对象的容器框架，它提供了统一的接口和实现类，方便开发者处理数据集合。Java 集合框架（Collection Framework）主要位于 `java.util` 包下，核心目标是简化数据存储、检索和操作的过程。

## 集合简介

集合类(collection)分为三种

- set(集合) 特点是元素是唯一的。对应着数学中的集合(set)

- List(列表) 特点是元素是可重复的，有序的

- Map(映射) 存在键值对，键值是唯一的。

  

集合的常见实现方式有：

- 哈希表(Hash set)

- 树结构(Tree set)

- 链表或数组(简单实现)

## Java中的集合

Java 集合框架主要分为两大体系：

  1. **Collection 接口**：存储**单个元素**的集合，是所有**单列集合**的根接口。
  2. **Map 接口**：存储**键值对**（Key-Value）的集合，不属于 `Collection` 体系，但常被归类为集合框架的一部分。key唯一，而value可以重复





  其中，`Collection` 接口有三个主要子接口：

  - `List`：有序、可重复的集合（允许元素重复，元素有索引）。
  - `Set`：无序、不可重复的集合（元素唯一，无索引）。
  - `Queue`：队列，按特定规则（如 FIFO）操作元素的集合。

  

### 集合与数组的区别

- **长度灵活性**：集合长度动态可变，数组长度固定。
- **存储类型**：集合只能存对象（基本类型需装箱为包装类），数组可存基本类型和对象。
- **功能丰富度**：集合提供了大量操作方法（如 `add`、`remove`），数组仅支持简单的索引访问。



### Collection

存储单个元素的集合，所有单列集合的根接口

#### List

是按索引顺序访问的长度可变的有序表。也是一个接口，具体的实现类有两种ArrayList,LinkedList；

![image-20250812153008922](C:\Users\23623\AppData\Roaming\Typora\typora-user-images\image-20250812153008922.png)



#### Set
Set用于存储不重复的元素集合，
Set实际上相当于只存储key、不存储value的Map。我们经常用Set用于去除重复元素。
因为放入Set的元素和Map的key类似，都要正确实现equals()和hashCode()方法，否则该元素无法正确地放入Set。





ArrayList的内部是通过数组来实现的，LinkedList是通过链表来实现的。这些实现类里面封装了一些数组/链表的操作，让我们使用起来更方便。

### Map

`Map`是一种映射表，可以通过`key`快速查找`value`；

最常用的一种`Map`实现是`HashMap`。

`Map`和`List`不同的是，`Map`存储的是`key-value`的映射关系，并且，它*不保证顺序*。在遍历的时候，遍历的顺序既不一定是`put()`时放入的`key`的顺序，也不一定是`key`的排序顺序。使用`Map`时，任何依赖顺序的逻辑都是不可靠的。以`HashMap`为例，假设我们放入`"A"`，`"B"`，`"C"`这3个`key`，遍历的时候，每个`key`会保证被遍历一次且仅遍历一次，但顺序完全没有保证，甚至对于不同的JDK版本，相同的代码遍历的输出顺序都是不同的！



Map的实现方式有HashMap 和 SortedMap。HashMap是用数组实现的，是用空间换时间的映射表，是无序的。

​	而SortedMap会对key进行内部排序。SortedMap也是一种接口，他的具体实现类是TreeMap。`SortedMap`保证遍历时以Key的顺序来进行排序。例如，放入的Key是`"apple"`、`"pear"`、`"orange"`，遍历的顺序一定是`"apple"`、`"orange"`、`"pear"`，因为`String`默认按字母排序。

​	使用`TreeMap`时，放入的Key必须实现`Comparable`接口。`String`、`Integer`这些类已经实现了`Comparable`接口，因此可以直接作为Key使用。作为Value的对象则没有任何要求。使用TreeMap时，对Key的比较需要正确实现相等、大于和小于逻辑！






# IO







