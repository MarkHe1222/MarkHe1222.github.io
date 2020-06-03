---
title: Java枚举小结
date: 2020-06-02 22:23:45
categories: Java Basic
tags: Java

---

### 为什么要用枚举

一般情况下，我们可以用常量来进行一些类型的定义。以开发流程的状态为列，开发流程一般分为：`design`, `develop`,`test`,`release`几个阶段，可以使用几个静态常量来定义：

```java
public class Development {
    public static final int DESIGN = 0;
    public static final int DEVELOP = 1;
    public static final int TEST = 2;
    public static final int RELEASE = 3;
}
```

这种定义其实也是可以的，但是会存在一些隐患。比如：

```java
    public static void checkStatus(int status){
			...
    }
```

这个方法的本意是根据数据的数字来判断`Development`的状态，但是如果输入`0~4`范围以外的`int`编译器也不会抛出任何的警告。

但是枚举可以使用更强更严谨的约束，可以帮我们规避掉这个风险，并且代码也更加简洁，有更好的可读性。

```java
public enum DevelopEnum {
    Plan, Develop, Test, Release;
}
```

我们在编写的时候，编译器此时就可以帮我们检查问题，防止我们疏忽造成问题。

```java
    public static void checkStatus(DevelopEnum status) {
			...
    }
```

### 枚举的基本实现原理

实际上，枚举本身也是一个类，我们可以通过编译上面的`DevelopEnum.java`文件，可以得到一个`DevelopEnum.clsss`文件：

```shell
Mark:enumeration mark$ ls
Check.java       DevelopEnum.java Development.java
Mark:enumeration mark$ javac DevelopEnum.java 
Mark:enumeration mark$ ls
Check.java        DevelopEnum.class DevelopEnum.java  Development.java
```

将`DevelopEnum.class`反编译可得到一下代码：

```java
Mark:enumeration mark$ javap DevelopEnum.class 
Compiled from "DevelopEnum.java"
public final class interview.enumeration.DevelopEnum extends java.lang.Enum<interview.enumeration.DevelopEnum> {
  public static final interview.enumeration.DevelopEnum Plan;
  public static final interview.enumeration.DevelopEnum Develop;
  public static final interview.enumeration.DevelopEnum Test;
  public static final interview.enumeration.DevelopEnum Release;
  public static interview.enumeration.DevelopEnum[] values();
  public static interview.enumeration.DevelopEnum valueOf(java.lang.String);
  static {};
}
```

可知，编译器帮我生成了一个`DevelopEnum`的类，该类继承自`java.lang.Enum` ，并且该类是无法被继承的`final` ;还生成了4个`DevelopEnum`的实例对象，分别对应枚举中定义的4个变量，这也说明了，我使用的枚举变量其实是`DevelopEnum`的对象；同时编译器生成了2个`static`方法，分别是`values()`和`valueOf()`; 最后h还有一个空的静态代码块`static {}`。

其中`values()`和`valueOf()`：

查看了一下`Enum.java`其中只有`valueOf()`并没有`values()`，所以`values()`应该是编译器为我们生成的。作用分别为：

```java
DevelopEnum[] developEnums = DevelopEnum.values();        System.out.println(Arrays.toString(developEnums));// [Plan, Develop, Test, Release]
DevelopEnum value = DevelopEnum.valueOf("Plan");
System.out.println(value); // Plan
```

### 枚举常用方法

```java
        DevelopEnum d1 = DevelopEnum.Plan;
        DevelopEnum d2 = DevelopEnum.Develop;
        DevelopEnum d3 = DevelopEnum.Test;
        DevelopEnum d4 = DevelopEnum.Release;
				
				// ordinal() 返回枚举的序列号，从0开始
        System.out.println(d1.ordinal()); // 0
        System.out.println(d2.ordinal()); // 1

				// compareTo() 枚举常量的比较
        System.out.println(d1.compareTo(d2)); // -1
        System.out.println(d2.compareTo(d1)); // 1 
        System.out.println(d3.compareTo(d3)); // 0

				//name() 获取枚举常量的名称
        System.out.println(d1.name()); // 
        System.out.println(d2.name());
```

### 枚举的自定义扩充

上面的例子是比较简单的**单值**用法，很多情况下我们需要**多值**用法， 我们就前面的例子继续拓展。通过前面的学习我们也知道枚举本身是一个类，所以我们也可以在枚举的定义中加入属性、构造函数、方法：

```java
public enum DevelopEnumNew {
    Plan("plan", 000),
    Develop("develop", 111),
    Test("test", 222),
    Release("release", 333);

    private String stage;
    private Integer code;

    DevelopEnumNew(String stage, Integer code) {
        this.stage = stage;
        this.code = code;
    }

    public String getStage() {
        return stage;
    }

    public Integer getCode() {
        return code;
    }

    public static Integer getCodeByStageName(String stage){
        for (DevelopEnumNew enums : DevelopEnumNew.values()) {
            if (enums.stage.equals(stage)) {
                return enums.getCode();
            }
        }
        return null;
    }
}
```

既然是类，那自然也可以和接口(`interface`)结合使用，举个例子：

**a. 当不使用枚举时：**

```java
    public String checkStatus(String status) {
        String result = "";
        if ("Plan".equals(status)) {
            result = "Status: " + "Plan";
        } else if ("Develop".equals(status)) {
            result = "Status: " + "Develop";
        } else if ("Test".equals(status)) {
            result = "Status: " + "Test";
        } else if ("Release".equals(status)) {
            result = "Status: " + "Release";
        }
        return result;
    }
```

**b. 使用枚举时：**

```java
    public String checkStatus(DevelopEnum status) {
        String result = "";
        switch (status) {
            case Plan:
                result = "Status: " + "Plan";
                break;
            case Develop:
                result = "Status: " + "Develop";
                break;
            case Test:
                result = "Status: " + "Test";
                break;
            case Release:
                result = "Status: " + "Release";
                break;
            default:
                break;
        }
        return result;
    }
```

**c. 使用枚举 + 接口时：**

接口：

```java
public interface logging {
    public abstract String log();
}
```

枚举：

```java
public enum  DevelopEnumImpl implements logging {
    Plan {
        @Override
        public String log() {
            return "Plan";
        }
    },

    Develop {
        @Override
        public String log() {
            return "Develop";
        }
    },

    Test {
        @Override
        public String log() {
            return "Test";
        }
    },

    Release {
        @Override
        public String log() {
            return "Release";
        }
    };
}
```

用法：

```java
    public String checkStatusImpl(String status) {
        return DevelopEnumImpl.valueOf(status).log();
    }
```

对比可知，明显枚举 + 接口的方法具有更强的拓展性，并且代码也更加优雅。如果想要对条件继续扩充的话，可以再定义新的借口，再到枚举中添加代码，而不用对主逻辑的代码进行改动。

### 枚举的集合类

#### a. EnumSet

`EnumSet`是枚举类型专用的`Set`集合。`EnumSet`不允许使用`null`元素，如果再`EnumSet`当中插入`null`，则会跑出`NullPointerException`，但是如果判断`EnumSet`当中是否存在`null`元素是否存在，或者删除`null`元素则不会抛异常。`EnumSet`不是线程安全的。

```java
    public Boolean isDev(Dev dev){
        EnumSet<DevelopEnum> enums = EnumSet.of(DevelopEnum.Plan, DevelopEnum.Develop);
        if (enums.contains(dev.getName())) {
            return true;
        }

        return false;
    }
```

#### b. EnumMap

`EnumMap`是枚举的专属集合，其`Key`要求必须为`Enum`类型。注意`EnumMap`的`Key`不能为`null`，因为`EnumMap`继承了`AbstractMap`，所以`EnumMap`也有一般`map`的方法。还有个不同的地方是，在`new EnumMap<>(enum.class); `需要传入类型信息，即`Class`对象。

假设PM要统计所有项目的开发状态：

```java
        EnumMap<DevelopEnum, Integer> enumIntegerEnumMap = new EnumMap<>(DevelopEnum.class);

        for (Project project: projects) {
            Integer num = enumIntegerEnumMap.get(project.getDevStatus);
            if (null != num) {
                enumIntegerEnumMap.put(project.getDevStatus, num+1);
            } else {
                enumIntegerEnumMap.put(project.getDevStatus, 1);
            }
        }
```

### 枚举的设计模式应用

#### a. 单例模式

#### b. 策略模式