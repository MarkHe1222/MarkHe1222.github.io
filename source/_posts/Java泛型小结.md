---
title: Java泛型小结
date: 2020-06-14 23:15:14
categories: Java
tags: Java Basic

---

### 什么是泛型？

泛型，即“参数化类型”。一提到参数，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。那么参数化类型怎么理解呢？顾名思义，就是将类型由原来的具体的类型参数化，类似于方法中的变量参数，此时类型也定义成参数形式（可以称之为类型形参），然后在使用/调用时传入具体的类型（类型实参）。
**泛型的本质是为了参数化类型（在不创建新的类型的情况下，通过泛型指定的不同类型来控制形参具体限制的类型）**。也就是说在泛型使用过程中，操作的数据类型被指定为一个参数，这种参数类型可以用在类、接口和方法中，分别被称为**泛型类、泛型接口、泛型方法**。

### 为什么要用泛型？

创建一个`List`，不指定类型的话，则可以添加任意类型:

```java
public class GenericsDemo1 {
    public static void main(String[] args) {
        List arrayList = new ArrayList();
        arrayList.add("string");
        arrayList.add(1);

        for (int i = 0; i < arrayList.size(); i++) {
            System.out.println(arrayList.get(i));
        }
    }
}

//Output:
string
1
```

但是如果如果需要以`String`的类型来处理`arrayList`内的元素，则编译的时候会遇到错误(编译器不报错)：

```java
public class GenericsDemo1 {
    public static void main(String[] args) {
        List arrayList = new ArrayList();
        arrayList.add("string");
        arrayList.add(1);

        for (int i = 0; i < arrayList.size(); i++) {
//            System.out.println(arrayList.get(i));
            String s = (String) arrayList.get(i);
        }
    }
}
```

`ERROR`:

```java
Exception in thread "main" java.lang.ClassCastException: java.lang.Integer cannot be cast to java.lang.String
```

若是我们在初始化`arraryList`的时候，指定了`String`类型，则编译器能够提前发现问题：

```java
        List<String> arrayList = new ArrayList();
        arrayList.add("string");
        //arrayList.add(1);
```

### 泛型的类型擦除

下面例子中，定义了`List<String>`和`List<Integer>`，本意上是2个类型，但是在编译后都变成`ArrayList`。`Java`的泛型基本上都是在编译器这个层次上实现的，在生成的字节码中是不包含泛型中的类型信息，使用泛型的时候加上类型参数，在编译器编译时会去掉，这个过程称为类型擦除。

```java
        List<String> stringList = new ArrayList<>();
        stringList.add("string");
        List<Integer> integerList = new ArrayList<>();
        integerList.add(1);

        Class classStringList = stringList.getClass();
        Class classIntegerList = integerList.getClass();

        System.out.println(classStringList); // class java.util.ArrayList
        System.out.println(classIntegerList); // class java.util.ArrayList
        System.out.println(classStringList == classIntegerList);  //true
```

后面详细讲解这块。

### 泛型的使用

泛型的使用情形分为三种：泛型类、泛型接口、泛型方法

#### 泛型类

泛型类用于类的定义中，可以通过这个方式来实现对类的”参数化“，顾名思义，在new类的时候可以输入类型参数。典型的用法就是各种容器类，如：`List`、`Set`、`Map`

基本用法：

```java
public class GenericClass<T> {
    public T key;

    public GenericClass(T key){
        this.key = key;
    }

    public T getKey() {
        return key;
    }
}

public class GenericDemo {
    public static void main(String[] args) {
        GenericClass<String> genericClass = new GenericClass<>("String");
        System.out.println(genericClass.getKey());  // String
    }
}
```

`new`泛型类的时候，不一定要传入类型实参。如上的例子所示，使用泛型的时候，若传入泛型类型实参(`String`)，则创建的类会根据类型参数做相应的限制。如果不传入类型参数的话，如下例子所示，使用泛型类的时候，成员变量可以为任意的类型。

```java
public class GenericDemo {
    public static void main(String[] args) {
        GenericClass<String> genericClass = new GenericClass<>("String");
        System.out.println(genericClass.getKey());

        GenericClass genericStr = new GenericClass("str");
        GenericClass genericInt = new GenericClass(1);
        GenericClass genericChar = new GenericClass('c');

        System.out.println(genericStr.getKey()); // str
        System.out.println(genericInt.getKey()); // 1
        System.out.println(genericChar.getKey()); // c
    }
}
```

需要注意的是:

1. 泛型类的类型参数必须为引用类型(类类型)，不能是基础类型(`string`, `int` ...);

2. 不能对泛型类使用`instanceof`

   ```java
           Integer val = 1;
           if (val instanceof GenericClass<Integer>) {
               System.out.println("test");
           }
   ```

   ```java
   GenericDemo.java:17: error: illegal generic type for instanceof
           if (val instanceof GenericClass<Integer>) {
   ```

#### 泛型接口

泛型接口的定义和泛型类基本相同，基本用法：

```java
public interface GenericsInterface<T> {
    public T getKey();
}
```

**未传入类型参数，实现泛型接口类：**

```java
public class GenericsImpl<T> implements GenericsInterface<T> {

    private T key;

    public GenericsImpl(T key) {
        this.key = key;
    }

    @Override
    public T getKey() {
        return key;
    }

    public static void main(String[] args) {
        GenericsImpl<String> generics = new GenericsImpl("str");
        System.out.println(generics.getKey());
    }
}
```

注意，其中实现类的声明中，不能忽略泛型类的声明`<T>`, 即：`public class GenericsImpl<T> implements GenericsInterface<T> {`若是忽略了`<T>`，编译会出现错误：

```java
public class GenericsImpl implements GenericsInterface<T> {
	... ... 
}

=========================================
ERROR:

GenericsImpl.java:3: error: cannot find symbol
public class GenericsImpl implements GenericsInterface<T> {
                                                       ^
  symbol: class T
```

**传入类型参数，实现泛型接口类：**

```java
public class GenericsImplPara implements GenericsInterface<String>{
    private String key;

    public GenericsImplPara(String key) {
        this.key = key;
    }

    @Override
    public String getKey() {
        return key;
    }

    public static void main(String[] args) {
        GenericsImplPara genericsImplPara = new GenericsImplPara("test");
        System.out.println(genericsImplPara.getKey()); // test
    }
}
```

当传入类型参数String时，则泛型类的声明`<T>`可以忽略。即`public class GenericsImplPara<T> implements GenericsInterface<String>`简化为以上的`public class GenericsImplPara implements GenericsInterface<String>`.

#### 泛型方法

与**泛型类**在实例化类的时候指明泛型的具体类型不同的是，**泛型方法**是在调用方法的时候指明泛型的具体类型。

#####泛型方法的基本用法:

```java
    /**
     * 泛型方法的基本介绍
     * @param GenericClass<T> genericClass 传入的泛型实参
     * @return T 返回值为T类型
     * 说明：
     * 		1> public与返回值T中间<T>非常重要,可以理解为声明此方法为泛型方法;
     * 		2> 只有声明了<T>的方法才是泛型方法,泛型类中的使用了泛型的成员方法并不是泛型方法;
     *		3> <T>表明该方法将使用泛型类型T,此时才可以在方法中使用泛型类型T;
     *		4> 与泛型类的定义一样,此处T可以随便写为任意标识,常见的如T、E、K、V等形式的参数常用于表示泛型
     */
    public <T> T genericsMethod(GenericClass<T> genericClass) {
        T instance = genericClass.newInstance();
        return instance;
    }
```

##### 类中使用泛型方法：

```java
public class GenericsFruit {
    static class Fruit {
        @Override
        public String toString() {
            return "Fruit";
        }
    }

    static class Apple extends Fruit {
        @Override
        public String toString() {
            return "Apple";
        }
    }

    static class Person {
        @Override
        public String toString() {
            return "Person";
        }
    }

    static class GenerateTest<T> {
        // 前面提到过，没有<T>修饰的方法不是泛型方法，T为调用方法的参数类型
        public void show1(T t) {
            System.out.println(t.toString());
        }
				
      	// 有<T>修饰，是泛型方法；此时可以在方法中使用泛型类型T;
        public <T> void show2(T t) {
            System.out.println(t.toString());
        }
				
      	// 本质上和show2方法一样，只是通配符的不同，后面会详细讲解一下通配符的使用
        public <E> void show3(E t) {
            System.out.println(t.toString());
        }
      	
      	// 错误的声明，此泛型方法只声明了<T>，并没有声明<E>
//        public <T> void show4(GenericClass<E> e) {
//            System.out.println(e.toString());
//        }
    }

    public static void main(String[] args) {
        Apple apple = new Apple();
        Person person = new Person();

        GenerateTest<Fruit> generateTest = new GenerateTest<>();
				
      	// show1 不是泛型方法，所以T是指类GenerateTest 初始化的时候，限定的Fruit
        generateTest.show1(apple);
//        generateTest.show1(person);

      	// show2方法有 <T> 修饰，所以此方法可以传入任意的类类型
        generateTest.show2(apple);
        generateTest.show2(person);

      	// 同 show2
        generateTest.show3(apple);
        generateTest.show3(person);
    }
  
  // OUTPUT：
  Apple
	Apple
  Person
  Apple
  Person

```

##### 可变参数的泛型方法：

```java
        public <T> void print(T... args) {
            for(T t: args) {
                System.out.println("T is: " + t);
            }
        }

				... ...
          
				generateTest.print("111",222,"aaaa","2323.4",55.55);

  // OUTPUT:
  T is: 111
  T is: 222
  T is: aaaa
  T is: 2323.4
  T is: 55.55
```

##### 静态方法使用泛型参数：

如果想要静态方法中使用泛型，即泛型参数。则这个静态方法必须为泛型方法(`<T>`)：

错误示例：

```java
        public static void testStatic(T t) {
            System.out.println(t);
        }

// 编译ERROR：
non-static type variable T cannot be referenced from a static context
        public static void testStatic(T t) {
```

正确用法：

```java
        public static <T> void testStatic(T t) {
            System.out.println(t);
        }
```

因为如果是类中的变量使用了静态变量，静态变量的调用是可以在类初始化之前就调用的，而泛型类在初始化之前，还不能确定类型，所以不能在类中使用静态的泛型参数。

##### 泛型方法小结：

- 静态方法想要使用泛型参数，则必须使用泛型方法；
- 泛型方法必须要有泛型声明`<T>`;
- 尽量使用泛型方法

### 泛型通配符

常用的泛型通配符为： `T，E，K，V，？` ，本质上这些字符都区别，是我们代码中一种约定俗成的东西。如上文提到的`T`，我们可以使用`A—Z`中的任意字符替换，并不会影响程序本身的运行，但是如果使用其他字母替换的话，代码整体的可读性较弱，没有统一的规范。

通常：

- `？` 表示不确定的`java`类型;
- `T (type)`表示具体的一个`java`类型;
- `K V (key value)`分别代表`java`键值中的`Key Value`;
- `E (element)`代表`Element`

#### 无界通配符 `<?>`

一般用于不确定或者不关心实际要操作的类类型，表示可以传入任意类类型参数；

```java
        public static void testQuestion(GenericClass<?> objs){
            System.out.println(objs);
        }
```

#### 上界通配符`<? extends T>`

用 `extends`关键字声明，表示参数类型可能是所指定`T`的类型，或者是此`T`类型的子类。这样有两个好处：

- 如果传入的类型不是`T`或者`T`的子类，编译不成功
- 泛型中可以使用`T`的方法，要强转成`T`才能使用

```java
        public <K extends Apple, E extends Person> E testUp(K k, E e){
            E res = e;
            res.toString(k);
            // ...
            return res;
        }
```

**注**： 类型参数列表中如果有多个类型参数上限，用逗号分开

#### 下界通配符`<? super T>`

用 `super`关键字声明，表示参数类型可能是所指定的`T`类型，或者是此`T`类型的父类型，直至`Object`类:

```java
public class Animal {
    public void eat() {
        System.out.println("animal eat");
    }
}

public class Dog extends Animal {
    public void run() {
        System.out.println("Dog run");
    }

    @Override
    public void eat() {
        System.out.println("Dog eat");
    }
}

public class GenericLowBound {
    public static void main(String[] args) {
        List<Dog> dogs = new ArrayList<>();
        List<Animal> animals = new ArrayList<>();
        new GenericLowBound().test(animals, dogs);
    }

    private <T> void test(List<? super T> dst, List<T> src) {
        for (T t: src) {
            dst.add(t);
        }
    }
}
```

上述例子中`test`方法中`dst`类型范围是**“大于等于”**`src`类型，所以`dst`的容器也能装下`src`。

#### `<?>`和`>T>`的区别

```java
        // 指定了集合tList中的元素的类型必须为T
        List<T> tList = new ArrayList<>();

        // 这里的？指集合qList中元素类型可以为任意类型，没有任何实际意义，这里是用作例子说明
        List<?> qList = new ArrayList<>();
```

在泛型的使用中，`？`和`T`都是表示某一类型，区别是我们可以对`T`类型的参数进行一些操作（方法调用等），而`？`却不行，很容理解，因为`？`是不确定的类型，如果需要对参数进行某个方法调用，我们无法确定`？`的参数是否有这个方法。

```java
        // 能确定operate()能返回T类型
				T t = operate();
				
				// 无法确定？
        ? q = operate();
```

`T`是一个**确定的**类型，通常用于泛型类和泛型方法的定义，`？`是一个**不确定**的类型，通常用于泛型方法的调用代码和形参，不能用于定义类和泛型方法。

##### `T`可以用来保证泛型参数的一致性

像下面的代码中，约定的`T`是`Number`的子类才可以，但是申明时是用的`Animal`和`Dog`，所以就会报错。

```java
    public static void main(String[] args) {
        List<Dog> dogs = new ArrayList<>();
        List<Animal> animals = new ArrayList<>();

        new GenericLowBound().test2(animals, dogs);
    }

    private <T extends Number> void test2(List<T> src, List<T> dest) {
        System.out.println(src);
        System.out.println(dest);
    }

Error：
========================
error: method test2 in class GenericLowBound cannot be applied to given types;
        new GenericLowBound().test2(animals, dogs);
                             ^
  required: List<T>,List<T>
  found: List<Animal>,List<Dog>
  reason: inference variable T has incompatible bounds
    equality constraints: Dog,Animal
    upper bounds: Number
  where T is a type-variable:
    T extends Number declared in method <T>test2(List<T>,List<T>)
```

##### 类型参数`T`可以多重限定而通配符`?`不行

使用`&`符号设定多重边界（`Multi Bounds`)，指定泛型类型`T`必须是`MultiLimitInterfaceA`和`MultiLimitInterfaceB`的共有子类型，此时变量`t`就具有了所有限定的方法和属性。对于通配符`?`来说，因为它不是一个确定的类型，所以不能进行多重限定。

```JAVA
public interface MultiLimitInterfaceA {
}

public interface MultiLimitInterfaceB {
}

public class MultiLimitClass implements MultiLimitInterfaceA, MultiLimitInterfaceB{
    public <T extends MultiLimitInterfaceA & MultiLimitInterfaceB> void test(T t) {
        System.out.println(t);
    }
}
```

#####通配符`?`可以使用**超类限定**而类型参数`T`不行

类型参数`T`只具有 一种类型限定方式(`extends`):

```java
T extends A
```

但是通配符` ? `可以进行两种限定(`extends  + super`)：

```java
? extends A
? super A
```

#### `List<T>`，`List<Object>`，`List<?>`区别

前面已经说过`<T>`和`<?>`的区别，这里主要说明下`<Object>`，`Object`和`T`不同点在于，`Object`是一个实打实的类,并没有泛指谁，而`T`可以泛指比如`Object` , **`public void printList2(List<T> list){}`**方法中可以传入**`List<Object> list`**类型参数，也可以传入**`List<String> list`**类型参数，但是**`public void printList1(List<Object> list){}`**就只可以传入**`List<Object> list`**类型参数，因为`Object`类型并没有泛指谁，是一个确定的类型.

```java
public class TestDifferenceBetweenObjectAndT {
    public static void printList1(List<Object> list) {
        for (Object elem : list)
            System.out.println(elem + " ");
        System.out.println();
    }
    public static <T> void printList2(List<T> list) {
        for (T elem : list)
            System.out.println(elem + " ");
        System.out.println();
    }
    public static void printList3(List<?> list) {
        for (int i = 0;i<list.size();i++)
            System.out.println(list.get(i) + " ");
        System.out.println();
    }
    public static void main(String[] args) {
        List<Integer> test1 = Arrays.asList(1, 2, 3);
        List<String> test2 = Arrays.asList("one", "two", "three");
        List<Object> test3 = Arrays.asList(1, "two", 1.23);
        List<GenericsFruit.Fruit> test4 = Arrays.asList(new GenericsFruit.Apple(), new GenericsFruit.Banana());

        //下面这句会编译报错，因为参数不能转化成功
//        printList1(test4);
        printList1(test3);
        printList1(test3);
        printList2(test1);
        printList2(test2);
        printList2(test3);
        printList3(test1);
        printList3(test2);
        printList3(test3);
    }
}

//OUTPUT
========
> Task :TestDifferenceBetweenObjectAndT.main()
1 
two 
1.23 

1 
two 
1.23 

1 
2 
3 

one 
two 
three 

1 
two 
1.23 

1 
2 
3 

one 
two 
three 

1 
two 
1.23 

```

#### `<T>`，`Class<T>`，`Class<?>`的区别

前面说过`<T>`是指某个确定的类类型，如`String`, `Integer`, `Map`等。

那[`Class`](https://blog.csdn.net/javazejian/article/details/70768369)是什么呢? `Class`也是一个类，但在`Class`存放上`<String>, <List>, <Map>`等类信息的一个类，有点抽象，下面具体分析：

#####`Java`当中有3种获取`Class`的方式：

1. **调用`Object`类的`getClass()`方法来得到`Class`对象，这也是最常见的产生`Class`对象的方法**：

   ```JAVA
           List list = null;
           Class clazz1 = list.getClass();
   ```

2. **使用`Class`类的中静态`forName()`方法获得与字符串对应的`Class`对象**:

   ```JAVA
           Class clazz2 = Class.forName("interview.generics.Dog");
   ```

3. **如果`T`是一个`Java`类型，那么`T.class`就代表了匹配的类对象**:

   ```JAVA
           Class clazz3 = List.class;
   ```

Class<T>`和`Class<?>` 的使用场景:

使用`Class<T>`和`Class<?>`多发生在反射场景下，先看看如果我们不使用泛型，反射创建一个类是什么样的.

```java
       // 需要强转，如果反射的类型不是Dog类，就会报
       // java.lang.ClassCastException错误。
       Dog dog = (Dog) Class.forName("interview.generics.Dog").newInstance();
```

使用Class<T>泛型后，不用强转了。

```java
public class TestCreateClassWithGenerics {
    public static <T> T createInstance(Class<T> clazz) throws IllegalAccessException, InstantiationException {
        return clazz.newInstance();
    }
    public static void main(String[] args) throws InstantiationException, IllegalAccessException {
        Dog dog = createInstance(Dog.class);
    }
}
```

#####`Class<T>`和`Class<?>` 的区别:

**`Class<T>`在实例化的时候，`T`要替换成具体类**， 如前面那个例子中`createInstance(Dog.class)`，传入的是具体的**`Dog.class`**;

**`Class<?>`它是个通配泛型，`?`可以代表任何类型，主要用于声明时的限制情况** :

```java

		// 可以声明如下
		public Class<?> clazz1;
    public Class<? extends Number> clazz2;
    public Class<? super Number> clazz3;
		
		// 不可以声明，除非是在一个泛型类中 T 有提前声明
    public Class<T> clazz4;
```

### 泛型的类型擦除详解

前面我们举了[一个例子](###泛型的类型擦除)大概说明了一下什么是泛型的类型擦除：`Java`的泛型基本上都是在编译器这个层次上实现的，在生成的字节码中是不包含泛型中的类型信息的，使用泛型的时候加上类型参数，在编译器编译的时候会去掉，这个过程成为类型擦除。

如在代码中定义`List<Object>`和`List<String>`等类型，在编译后都会变成`List`，`JVM`看到的只是`List`，而由泛型附加的类型信息对`JVM`是看不到的。`Java`编译器会在编译时**尽可能**的发现可能出错的地方，但是**仍然无法发现在运行时刻出现的类型转换异常**的情况，类型擦除也是`Java`的泛型与`C++`模板机制实现方式之间的重要区别。

除了前面提到的那个例子，我们再用一个反射的例子，来说明类型擦除：

```java
public class TestGenericsTypeErasure {

    public static void main(String[] args) throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        ArrayList<Integer> list = new ArrayList<Integer>();

        list.add(1);

        list.getClass().getMethod("add", Object.class).invoke(list, "asd");

        for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
    }
}

//OUTPUT:
> Task :TestGenericsTypeErasure.main()
1
asd
```

在程序中定义了一个`ArrayList`泛型类型实例化为`Integer`对象，如果直接调用`add()`方法，那么只能存储整数数据，不过当我们利用反射调用`add()`方法的时候，却可以存储字符串，这说明了`Integer`泛型实例在编译之后被擦除掉了，只保留了原始类型。

#### 泛型类型擦除后保留的原始类型

##### 什么是原始类型？

就是在泛型类编译后，擦去了泛型信息，最后在字节码中参数类型的真正类型。

- 在没有限定泛型类型时（上界），泛型参数会被自动转成该方法中的几种类型的最小公共父类，直到`Object`类型（所有类的公共父类）；

- 在指定泛型类型时，该方法的几种类型必须是该泛型的实例的类型或者其子类。

  ```java
  public class TestPublicParentClass {
      public static void main(String[] args) {
          // 不指定泛型时
          int i = TestPublicParentClass.returnT(1, 2); //这两个参数都是Integer，所以T为Integer类型
          Number f = TestPublicParentClass.returnT(1, 1.2); //这两个参数一个是Integer，一个是Float，所以取同一父类的最小级，为Number
          Object o = TestPublicParentClass.returnT(1, "abc"); //这两个参数一个是Integer，一个是String，所以取同一父类的最小级，为Object
  
  
          // 指定泛型的时候
          int a = TestPublicParentClass.<Integer>returnT(1, 2); //指定了Integer，所以T只能为Integer类型或者其子类
          // int b = TestPublicParentClass.<Integer>returnT(1, 2.2); //编译错误，指定了Integer，不能为Float
          Number c = TestPublicParentClass.<Number>returnT(1, 2.2); //指定为Number，所以可以为Integer和Float
      }
      
      // 泛型方法
      public static <T> T returnT(T x, T y) {
          return y;
      }
  }
  ```

##### `Object`泛型

在泛型类中，如果不指定泛型的时候，这个时候的泛型为`Object`，就比如`ArrayList`中，如果不指定泛型，那么这个`ArrayList`可以存储任意的对象。

```java
        ArrayList<Object> list = new ArrayList(); // 即： ArrayList list = new ArrayList();
        list.add(1);
        list.add("121");
        list.add(new Date());
```

#### 先检查，再编译以及编译的对象和引用传递问题

##### 先检查，再编译

**问：** 前面提到过类型变量会在编译的时候擦除掉，那为什么我们往`ArrayList`创建的对象中添加整数会报错呢？不是说泛型变量`String`会在编译的时候变为`Object`类型吗？为什么不能存别的类型呢？既然类型擦除了，如何保证我们只能使用泛型变量限定的类型呢？

**答：**`Java`编译器是通过先检查代码中泛型的类型，然后在进行类型擦除，再进行编译。

```java
public static  void main(String[] args) {  
    ArrayList<String> list = new ArrayList<String>();  
    list.add("123");  
    list.add(123);//编译错误  
}
```

在上面的程序中，使用`add`方法添加一个整型，在`IDE`中，直接会报错，说明这就是在编译之前的检查，因为如果是在编译之后检查，类型擦除后，原始类型为`Object`，是应该允许任意引用类型添加的。可实际上却不是这样的，这恰恰说明了关于泛型变量的使用，是会在编译之前检查的。

还是以`ArrayList`为例：

```java
        //以前的写法
				ArrayList list1 = new ArrayList();
				//现在的写法
        ArrayList<String> list2 = new ArrayList<String>();
				
				//如果是与以前的代码兼容，各种引用传值之间，必然会出现如下的情况：
        ArrayList<String> list3 = new ArrayList<>(); //第一种情况
        ArrayList list4 = new ArrayList<String>(); //第二种情况
```

以上代码都能通过编译，不过在第一种情况，可以实现与完全使用泛型参数一样的效果，第二种则没有效果。

因为类型检查就是编译时完成的，`new ArrayList()`只是在内存中开辟了一个存储空间，可以存储任何类型对象，而真正设计类型检查的是它的引用，因为我们是使用它引用`list1`来调用它的方法，比如说调用`add`方法，所以`list1`引用能完成泛型类型的检查。而引用`list2`没有使用泛型，所以不行。

##### 编译的对象

```java
public class TestCheckingOfGenerics {
    public static void main(String[] args) {
        ArrayList<String> list1 = new ArrayList<>();
        list1.add("1"); //检查通过  编译通过
//        list1.add(1); //检查错误  编译错误
        String str1 = list1.get(0); //返回类型就是String

        ArrayList list2 = new ArrayList<String>();
        list2.add("1"); //检查通过  编译通过
        list2.add(1); //检查通过  编译通过
        Object object = list2.get(0); //返回类型就是Object

        new ArrayList<String>().add("1"); //检查通过  编译通过
//        new ArrayList<String>().add(22); //检查错误  编译错误

        String str2 = new ArrayList<String>().get(0); //返回类型就是String  
    }
}
```

通过上面的例子，我们可以明白，类型检查就是针对引用的，谁是一个引用，用这个引用调用泛型方法，就会对这个引用调用的方法进行类型检测，而无关它真正引用的对象。

#####  引用传递问题

有继承关系的两种情况，引用传递都是不允许的：

1. ```java
   ArrayList<String> list1 = new ArrayList<Object>(); //编译错误 
   ```

   将代码拓展：

   ```java
           ArrayList<Object> list11 = new ArrayList<Object>();
           list11.add(new Object());
           list11.add(new Object());
   //        ArrayList<String> list12 = list11; //编译错误
   
   // ERROR:
   error: incompatible types: ArrayList<Object> cannot be converted to ArrayList<String>
           ArrayList<String> list12 = list11; //编译错误
   ```

   实际上，在第4行代码的时候，就会有编译错误。那么，我们先假设它编译没错。那么当我们使用`list12`引用用`get()`方法取值的时候，返回的都是`String`类型的对象（上面提到了，类型检测是根据引用来决定的），可是它里面实际上已经被我们存放了`Object`类型的对象，这样就会有`ClassCastException`了。所以为了避免这种极易出现的错误，`Java`不允许进行这样的引用传递。（这也是泛型出现的原因，就是为了解决类型转换的问题，我们不能违背它的初衷）

2. ```java
   ArrayList<Object> list2 = new ArrayList<String>(); //编译错误
   ```

   将代码拓展：

   ```java
           ArrayList<String> list21 = new ArrayList<>();
           list21.add(new String());
           list21.add(new String());
   //        ArrayList<Object> list22 = list21; //编译错误
   
   // ERROR:
   error: incompatible types: ArrayList<String> cannot be converted to ArrayList<Object>
           ArrayList<Object> list22 = list21;
   ```

   泛型出现的原因，就是为了解决类型转换的问题。我们使用了泛型，到头来，还是要自己强转，违背了泛型设计的初衷。所以`java`不允许这么干。再说，你如果又用`list21`往里面`add()`新的对象，那么到时候取得时候，我怎么知道我取出来的到底是`String`类型的，还是`Object`类型的呢？

#### 自动类型转换

因为类型擦除，所有的泛型变量在编译以后都转为原始类型了，**那为什么我们从泛型集合内获取元素时，不需要强制类型转换？**

以`ArrayList`的`get()`方法为例：

```java
    public E get(int index) {
        rangeCheck(index);

        return elementData(index);
    }


    @SuppressWarnings("unchecked")
    E elementData(int index) {
        return (E) elementData[index];
    }
```

可以看到在retrun之前，泛型变量会先被强制转换。假设泛型类型变量为`Date`，虽然代码编译以后泛型信息会被擦除掉，但是会将`(E) elementData[index]`，编译为`(Date)elementData[index]`。所以我们不用自己进行强转。当存取一个泛型域时也会自动插入强制类型转换。

#### 类型擦除与多态

一个例子：

父类（泛型）：

```java
public class ClassErasureAndGenerics<T> {

    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }

//    public Object getValue(){
//        return new Object();
//    }
}
```

子类：

```java
public class ClassErasureAndGenericsSub extends ClassErasureAndGenerics<Date> {
    @Override
    public void setValue(Date value) {
        super.setValue(value);
    }

    @Override
    public Date getValue() {
        return super.getValue();
    }

    public static void main(String[] args) {
        ClassErasureAndGenericsSub sub = new ClassErasureAndGenericsSub();
        sub.setValue(new Date());
//        sub.setValue(new Object());
    }
}
```

按照前面提到，父类编译以后，`T`会被转换成原始类型`Object`：

```java
//javap
Mark:generics mark$ javap -c ClassErasureAndGenerics.class 
Compiled from "ClassErasureAndGenerics.java"
public class interview.generics.ClassErasureAndGenerics<T> {
  public interview.generics.ClassErasureAndGenerics();
    Code:
       0: aload_0
       1: invokespecial #1                  // Method java/lang/Object."<init>":()V
       4: return

  public void setValue(T);
    Code:
       0: aload_0
       1: aload_1
       2: putfield      #2                  // Field value:Ljava/lang/Object;
       5: return

  public T getValue();
    Code:
       0: aload_0
       1: getfield      #2                  // Field value:Ljava/lang/Object;
       4: areturn
}
```

那么在子类中的`setValue`方法调用的类型是`Date`，参数类型不一致，那在`java`中提到的，如果方法类型不一样，方法名一样，应该是重载，而不是重写，但是重载是发生在同一个类中的。

```java
    public static void main(String[] args) {
        ClassErasureAndGenericsSub sub = new ClassErasureAndGenericsSub();
        sub.setValue(new Date());
        // sub.setValue(new Object()); 编译错误
    }

//ERROR：
error: no suitable method found for setValue(Object)
        sub.setValue(new Object());
           ^
    method ClassErasureAndGenerics.setValue(Date) is not applicable
      (argument mismatch; Object cannot be converted to Date)
    method ClassErasureAndGenericsSub.setValue(Date) is not applicable
      (argument mismatch; Object cannot be converted to Date)
```

以上代码再次证明了，这个确实是重写，而不是重载。

这不是与我们之前解释的理论相矛盾了吗？从`Java`语法上来看，子类的类型是`Data`，而父类的类型在反编译中也很清楚是`Object`的，这样应该是重载呀。类型擦除就和多态有了冲突。`JVM`知道你的本意吗？知道！！！可是它能直接实现吗，不能！！！如果真的不能的话，那我们怎么去重写我们想要的`Date`类型参数的方法啊。

再看看`ClassErasureAndGenericsSub.class`的反编译：

```java
ark:generics mark$ javap -c ClassErasureAndGenericsSub.class 
Compiled from "ClassErasureAndGenericsSub.java"
public class interview.generics.ClassErasureAndGenericsSub extends interview.generics.ClassErasureAndGenerics<java.util.Date> {
  public interview.generics.ClassErasureAndGenericsSub();
    Code:
       0: aload_0
       1: invokespecial #1                  // Method interview/generics/ClassErasureAndGenerics."<init>":()V
       4: return

  public void setValue(java.util.Date);     // <--- Override setValue
    Code:
       0: aload_0
       1: aload_1
       2: invokespecial #2                  // Method interview/generics/ClassErasureAndGenerics.setValue:(Ljava/lang/Object;)V
       5: return
    
  public void setValue(java.lang.Object);
    Code:
       0: aload_0
       1: aload_1
       2: checkcast     #4                  // class java/util/Date
       5: invokevirtual #8                  // Method setValue:(Ljava/util/Date;)V
       8: return       
    
 -----------------------------------------------        
         
  public java.lang.Object getValue();       // <--- Override getValue
    Code:
       0: aload_0
       1: invokevirtual #9                  // Method getValue:()Ljava/util/Date;
       4: areturn

  public java.util.Date getValue();         
    Code:
       0: aload_0
       1: invokespecial #3                  // Method interview/generics/ClassErasureAndGenerics.getValue:()Ljava/lang/Object;
       4: checkcast     #4                  // class java/util/Date
       7: areturn
}

```

从编译的结果来看，我们本意重写`setValue`和`getValue`方法的子类，竟然有`4`个方法，其实不用惊奇，最后的两个方法，就是编译器自己生成的**桥方法**。可以看到桥方法的参数类型都是`Object`，也就是说，子类中真正覆盖父类两个方法的就是这两个我们看不到的桥方法。而打在我们自己定义的`setvalue`和`getValue`方法上面的`@Oveerride`只不过是假象。而桥方法的内部实现，就只是去调用我们自己重写的那两个方法。

所以，虚拟机巧妙的使用了桥方法，来解决了类型擦除和多态的冲突。

不过，要提到一点，这里面的`setValue`和`getValue`这两个桥方法的意义又有不同。

`setValue`方法是为了解决类型擦除与多态之间的冲突。

而`getValue`却有普遍的意义。

即如果这是一个普通的继承关系，那么父类的`getValue`方法如下：

```java
public Object getValue() {  
    return super.getValue();  
}
```

子类方法：

```java
public Date getValue() {  
    return super.getValue();  
}
```

这在普通的类继承中也是普遍存在的重写。

#### 为什么泛型变量不能是基本数据类型

因为类型擦除以后，假设原始类型转变为`Object`，而`Object`变量中无法存基本类型。

如： 没有`ArrayList<double>`，只有`ArrayList<Double>`。因为当类型擦除后，`ArrayList`的原始类型变为`Object`，但是`Object`类型不能存储`double`值，只能引用`Double`的值。

#### 为什么泛型类型不能使用`instanceof`

```JAVA
        Integer val = 1;
        if (val instanceof GenericClass<Integer>) {
            System.out.println("test");
        }
```

因为类型擦除后，`Integer`被转成原始类型，泛型信息`Integer`已经不存在了。



### 参考

-  [聊一聊-JAVA 泛型中的通配符 T，E，K，V，？](https://juejin.im/post/5d5789d26fb9a06ad0056bd9#heading-4) 
- [JAVA泛型通配符T，E，K，V区别，网友回复：一文秒懂](https://www.toutiao.com/a6694132392728199683)
- [java 泛型详解-绝对是对泛型方法讲解最详细的，没有之一](https://blog.csdn.net/s10461/article/details/53941091)
- [Java泛型类型擦除以及类型擦除带来的问题](https://www.cnblogs.com/wuqinglong/p/9456193.html)