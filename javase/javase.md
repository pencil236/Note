#  第一个Java程序
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



# 基础语法









# 面向对象编程（OOP）





## 封装



## 继承



## 多态







# 重要API



## 集合

- 什么是集合

  如果一个Java对象的内部持有若干其他的Java对象，并对外提供访问的接口，这个Java对象就被称为集合。比如Java的数据可以看成一种集合

- 为什么要引入集合的概念？

  为了便于处理一组类似的数据



# 进阶概念







