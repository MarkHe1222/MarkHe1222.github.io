---
title: 理解J2EE和EJB
date: 2019-05-12 13:04:23
categories: 
- Java
tags: 
- Java 
---

在介绍这些概念之前我们先理解一下另外两个概念POJO和JavaBean。

### **POJO**

POJO(Plain Oridinary Java Object/ Plain Old Java Object) 称为简单Java对象，具体定义是：有一些private参数作为对象的属性，然后针对每个参数定义get和set方法供外部访问，没有任何类即成，也没有实现任何借口，更没有引用任何气态框架的java对象；

例子：

```java
public class User {  
    private String name;  
    private int age;  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
}
```

### **JavaBean**

JavaBean是一种用Java语言写成的可重用组件。JavaBean符合一定规范编写的Java类。所以JavaBean不是一种技术，而是一种规范。大家针对这种规范，总结了很多开发技巧，做出很多组件或工具。符合这种规范的类，可以被其它的程序员或者框架使用。

总结出来的规范为：

- 所有属性都为private；
- 这个类必须有一个公共的缺省的构造函数(即无参数的构造器)；
- 这个类的属性只能使用get和set来访问，其它的方法遵从[Java标准命名规范](https://blog.csdn.net/u012116457/article/details/22582393);
- 这个类是可[序列化的](http://www.blogjava.net/jiangshachina/archive/2012/02/13/369898.html)(实现serializable接口)

例子：

```java
public class UserInfo implements java.io.Serializable{ 
 
    //实现serializable接口。  
    private static final long serialVersionUID = 1L;  
 
    private String name;  
    private int age;  
      
    //无参构造器  
    public UserInfo() {  
	
    }  
	
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
  
    //javabean当中可以有其它的逻辑方法  
    public void userInfoPrint(){  
        System.out.println("");  
    }  
```

### **J2EE**

介绍完前面的POJO和JavaBean现在开始介绍J2EE。

首先要区分的是J2EE和Java的不同，其实Java不仅仅是代表了编程语言，应该是代表了一种编程体系(软件系统系统的一种流派)，比如，和其相对应地另外一大体系是出自微软的.NET.

J2EE(Java 2 Platform, Enterprise Edition)可以理解为:

> **J2EE = Java2 + 开发企业级软件的标准**

		*注： 从java 1.2 以后的版本都称为Java2*

所以可解释为J2EE是基于Java2的基础上，为了合理利用软件开发公用复用的原则，而订制的一系列的标准，而通常这些标准又会以一系列的软件库的形式存在(同一个标准可以有多个实现)。所以进一步的通俗理解：J2EE就是分别为java领域的企业软件开发提供的一系列的软件库，供大家使用。这里的软件库，有框架的，也有驱动库等等。

### **EJB**

EJB(Enterprise JavaBean)其实就是J2EE这个标准中的一项关键技术，是普通JavaBeans的一种提升和规范，因为企业信息系统开发中需要一个可伸缩的性能和事务、安全机制，这样能保证企业系统平滑发展，而不是发展到一种规模重新更换一套软件系统。

**官方解释**：商务软件的核心部分是它的业务逻辑。业务逻辑抽象了整个商务过程的流程，并使用计算机语言将他们实现。

一般的应用场景是比较重量级的企业级应用当中，这种业务逻辑会很繁重和复杂，EJB其实就是将属于业务逻辑当中的那些类都从客户端抽离出来，放到一个组件中，并将这个组件放到服务器上运行。

#### **- 	EJB的实现技术**

EJB 是运行在独立服务器上的组件，客户端是通过网络对EJB 对象进行调用的。在Java中，能够实现远程对象调用的技术是RMI(Remote Method Invocation)，而EJB 技术基础正是RMI。通过RMI 技术，J2EE将EJB 组件创建为远程对象，客户端就可以通过网络调用EJB 对象了。

##### **-	[RMI](https://blog.csdn.net/peterkang202/article/details/52397147) **

中文名称是"远程方法调用"，它就是利用Java 对象序列化的机制实现分布式计算，实现远程类对象的实例化以及调用的方法。说的更清楚些，就是利用对象序列化来实现远程调用，也就是上面两个概念的结合体，利用这个方法来调用远程的类的时候，就不需要编写Socket 程序了，也不需要把对象进行序列化操作，直接调用就行了非常方便。远程方法调用是一种计算机之间对象互相调用对方函数，启动对方进程的一种机制，使用这种机制，某一台计算机上的对象在调用另外一台计算机上的方法时，使用的程序语法规则和在本地机上对象间的方法调用的语法规则一样。

**优点：** 

这种机制给分布计算的系统设计、编程都带来了极大的方便。只要按照RMI 规则设计程序，可以不必再过问在RMI 之下的网络细节了，如：TCP 和Socket 等等。任意两台计算机之间的通讯完全由RMI 负责。调用远程计算机上的对象就像本地对象一样方便。RMI 可将完整的对象作为参数和返回值进行传递，而不仅仅是预定义的数据类型。也就是说，可以将类似Java 哈西表这样的复杂类型作为一个参数进行传递。

[缺点](https://www.cnblogs.com/ggjucheng/archive/2012/01/06/2314067.html)：

如果是较为简单的方法调用，其执行效率也许会比本地执行慢很多，即使和远程Socket机制的简单数据返回的应用相比，也会慢一些，原因是，其在网络间需要传递的信息不仅仅包含该函数的返回值信息，还会包含该对象序列化后的字节内容。
