## java基础

参考：

- 狂神说B站系统简介：https://space.bilibili.com/95256449/channel/detail?cid=146244
- 网络资料：https://www.sxt.cn/Java_jQuery_in_action/Introduction_of_programming_language.html
- 百度百科

## 一.计算机基础知识

### 1.Dos命令

1. 打开方式：使用win+R打开CMD（常用）

2. 常用的dos命令

   ```xml
   盘符切换： F：+回车
   查看当前目录下的所有文件  dir
   ```

### 2.计算机语言发展史

```xml
第一代语言：机器语言
第二代语言：汇编语言
第三带语言：高级语言：C、c++、java、C#、python等等
```

### 3.摩尔定律

```xml
1、集成电路芯片上所集成的电路的数目，每隔18个月就翻一番；
2、微处理器的性能每隔18个月提高一倍，而价格下降一半；
3、用一美元所能买到的计算机性能，每隔18个月翻两番。
```

## 二.java是什么？

### 1.java的诞生

```xml
Java是一门面向对象编程语言，不仅吸收了C++语言的各种优点，还摒弃了C++里难以理解的多继承、指针等概念，因此Java语言具有功能强大和简单易用两个特征。Java语言作为静态面向对象编程语言的代表，极好地实现了面向对象理论，允许程序员以优雅的思维方式进行复杂的编程。
```

![image-20210109221825682](C:\Users\13444\Desktop\MyNotes\imgs\image-20210109221825682.png)

## 三.为什么要学习java？

### 1.java的优点：高可用、高性能、高并发

- 简单性
- 面向对象
- 可已执行
- 高性能
- 分布式：网络的分布式开发
- 动态性：反射机制
- 多线程
- 安全性
- 健壮性

### 2.编程语言排行：java占据第二位_2020.12

![image-20210109222744188](C:\Users\13444\Desktop\MyNotes\imgs\image-20210109222744188.png)

## 四.java后端学习进阶路程：任重道远

![image-20210109223721937](C:\Users\13444\Desktop\MyNotes\imgs\image-20210109223721937.png)

## 五.java基础知识

### 1.java的三大版本

- **JavaSE：标注版：**
- JavaME：嵌入式开发-->Android
- **JavaEE：企业级开发：web、服务器端开发**

### 2.JDK、JRE、JVM

- JDK：java开发者工具--包含jre+jvm

- JRE：java运行时环境

- JVM：java虚拟机：

  ```xml
  什么是虚拟机？
  		虚拟机是一种抽象化的计算机，通过在实际的计算机上仿真模拟各种计算机功能来实现的。Java虚拟机有自己完善的硬体架构，如处理器、堆栈、寄存器等，还具有相应的指令系统。Java虚拟机屏蔽了与具体操作系统平台相关的信息，使得Java程序只需生成在Java虚拟机上运行的目标代码（字节码），就可以在多种平台上不加修改地运行。
  ```

### 3.JDK安装及卸载

#### 1.安装JDK

```xml
安装及环境变量配置:
https://blog.csdn.net/kangmiao89757/article/details/9993887?ops_request_misc=%25257B%252522request%25255Fid%252522%25253A%252522160851668416780277053420%252522%25252C%252522scm%252522%25253A%25252220140713.130102334..%252522%25257D&request_id=160851668416780277053420&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-9993887.nonecase&utm_term=java%E5%AE%89%E8%A3%85%E5%8F%8A%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B
```

- java官网下载：https://www.java.com/zh-CN/download/

  注：版本为java-8u271，目前企业较多使用java1.8，截止2020.01.09，oracle javaSE已经更新到java 15。

- java安装时需要dos命令验证java安装成功、环境变量配置成功

  ```xml
  java -version:验证java安装是否成功及环境变量配置、查看本机java环境版本
  ```

  注：学习工作仅安装java jdk是远远不够的，查看“开发新机器配置.md”进一步拓展，类如IDEA的插件安装等未涉及到，仅讨论到java、tomcat、maven、数据库及Jetbrains工具安装，其他开发所用的工具暂未涉及，以待更新。

#### 2.卸载JDK

1. 删除java的安装目录
2. 删除java_home/path
3. java -version查看是否卸载成功

### 4.第一个java程序:HelloWorld

```java
public class hello{
  public static void helloWorld(Strings[] args){
    system.out.println("hello,world");
  }
}
```

- 不依靠IDEA等编码工具手写hello.java

1. 选择一个文件夹新建hello.java文件
2. 使用notepad++（一款十分好用的文本编辑器）打开
3. 编辑，如下图

![image-20210109232511934](C:\Users\13444\Desktop\MyNotes\imgs\image-20210109232511934.png)

4. 使用cmd编译hello.java到hello.class

![image-20210109232217645](C:\Users\13444\Desktop\MyNotes\imgs\image-20210109232217645.png)

5. 同级目录下出现hello.class文件

![image-20210109232343464](C:\Users\13444\Desktop\MyNotes\imgs\image-20210109232343464.png)

6. cmd命令：java hello 回车

![image-20210109232604103](C:\Users\13444\Desktop\MyNotes\imgs\image-20210109232604103.png)

7. 恭喜入门，任重道远

### 5.test

