---
title: Java源码分析——ArrayList
date: 2020-08-17 22:41:42
categories: Java
tags: Collection

---

### 简介

`ArrayList`是一种以数组实现的`List`，与数组相比，它具有动态扩展的能力，因此也可称之为动态数组。

在添加大量元素前，应用程序可以使用`ensureCapacity`操作来增加`ArrayList`实例的容量。这可以减少递增式再分配的数量。

是`Collection`集合框架下`List`接口的一种实现。

![Collection框架](Java源码分析——ArrayList/Collection框架.jpeg)

具体的继承体系如下：

> 蓝色路径：继承
>
> 绿色路径： 接口实现

![ArrayList继承体系](Java源码分析——ArrayList/ArrayList继承体系.png)

- `ArrayList`继承了**`AbstractList`**，实现了`List`。它是一个数组队列，提供了相关的添加、删除、修改、遍历等功能；
- `ArrayList`实现了**`RandomAccess`接口**， `RandomAccess`是一个标志接口，表明实现这个这个接口的List集合是支持**快速随机访问**的。在`ArrayList`中，我们即可以通过元素的序号快速获取元素对象，这就是快速随机访问。
- `ArrayList`实现了**`Cloneable`接口**，即覆盖了函数`clone()`，**能被克隆**；
- `ArrayList`实现**`java.io.Serializable`接口**，这意味着`ArrayList`**支持序列化**，**能通过序列化去传输**。

### 内部变量

```java
    
		// 序列化IDserialVersionUID是用来验证版本一致性的字段
		private static final long serialVersionUID = 8683452581122892189L;

    /**
     * Default initial capacity.
     */
		// 默认初始容量
    private static final int DEFAULT_CAPACITY = 10;

    /**
     * Shared empty array instance used for empty instances.
     */
		// 一个空数组，主要用于带参数构造函数初始话和读取序列化对象等（方便使用）
    private static final Object[] EMPTY_ELEMENTDATA = {};

    /**
     * Shared empty array instance used for default sized empty instances. We
     * distinguish this from EMPTY_ELEMENTDATA to know how much to inflate when
     * first element is added.
     * DEFAULTCAPACITY_EMPTY_ELEMENTDATA 和EMPTY_ELEMENTDATA 的区别：
     * 仅仅是为了区别用户带参为0的构造和默认构造的惰性初始模式对象。
     * 		当用户带参为0的构造，第一次add时，数组容量grow到1；
     *		当用户使用默认构造时，第一次add时，容量直接grow到DEFAULT_CAPACITY（10）；
     */
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

    /**
     * The array buffer into which the elements of the ArrayList are stored.
     * The capacity of the ArrayList is the length of this array buffer. Any
     * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
     * will be expanded to DEFAULT_CAPACITY when the first element is added.
     */
		// 当前数据对象存放地方，当前对象不参与序列化
		// 这个关键字最主要的作用就是当序列化时，被transient修饰的内容将不会被序列化
		// ArraryList另外实现了序列化与反序列化
    transient Object[] elementData; // non-private to simplify nested class access

    /**
     * The size of the ArrayList (the number of elements it contains).
     *
     * @serial
     */
		// 当前数组数组中的元素
    private int size;
	
		 /**
     * The maximum size of array to allocate.
     * Some VMs reserve some header words in an array.
     * Attempts to allocate larger arrays may result in
     * OutOfMemoryError: Requested array size exceeds VM limit
     */
		// 数组最大可分配容量 
		// 存储的最大容量也取决于运行Java代码的平台内存和JVM的堆比例
		// 8个byte是用来存储元数据，用来描述这个数组的长度
		private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;
		
		// 集合数组修改次数的标识（由AbstractList继承下来）（fail-fast机制）
    protected transient int modCount = 0;

```

### 源码分析

#### 构造函数

```java
    /**
     * Constructs an empty list with an initial capacity of ten.
     */
		// 无参（默认）构造函数
    public ArrayList() {
      	// 只有这个地方会引用DEFAULTCAPACITY_EMPTY_ELEMENTDATA
      	// 使用这个数组是在添加第一个元素的时候会扩容到默认大小10
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }

    /**
     * Constructs an empty list with the specified initial capacity.
     *
     * @param  initialCapacity  the initial capacity of the list
     * @throws IllegalArgumentException if the specified initial capacity
     *         is negative
     */
		// 当用户带参为0的构造，第一次add时，数组容量grow到1；
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
          	// 如果传入的初始容量大于0，就新建一个数组存储元素
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            // 使用EMPTY_ELEMENTDATA，在其他的多个地方可能会引用EMPTY_ELEMENTDATA
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }

    /**
     * Constructs a list containing the elements of the specified
     * collection, in the order they are returned by the collection's
     * iterator.
     *
     * @param c the collection whose elements are to be placed into this list
     * @throws NullPointerException if the specified collection is null
     */
    public ArrayList(Collection<? extends E> c) {
      	// 集合转数组给elementData(toArray浅拷贝？) 
        elementData = c.toArray();
        if ((size = elementData.length) != 0) {
            // c.toArray might (incorrectly) not return Object[] (see 6260652)
          	// 若c.toArray()返回的数组类型不是Object[]，则利用Arrays.copyOf(); 来构造一个大小为size的Object[]数组
            // 此时elementData是指向传入集合的内存，还需要创建新的内存区域深拷贝给elementData 
            if (elementData.getClass() != Object[].class)
                elementData = Arrays.copyOf(elementData, size, Object[].class);
        } else {
            // replace with empty array.
            this.elementData = EMPTY_ELEMENTDATA;
        }
    }
```

#### 添加

```java
		// 在数组最后添加新元素
    public boolean add(E e) {
      	// 确保数组已使用长度（size）加1之后足够存下 下一个数据
        ensureCapacityInternal(size + 1);  // Increments modCount!!
      	// 数组的下一个index存放传入元素。
        elementData[size++] = e;
        return true;
    }

		// 在数组指定位置插入新元素
    public void add(int index, E element) {
        rangeCheckForAdd(index);
				
      	// 确保数组已使用长度（size）加1之后足够存下 下一个数据
        ensureCapacityInternal(size + 1);  // Increments modCount!!
      	// 将index及其之后的元素往后挪一位，则index位置处就空出来了
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index);
      	// 数组的下一个index存放传入元素
        elementData[index] = element;
      	// 数组长度加1
        size++;
    }
		
		// 添加一个结合元素
    public boolean addAll(Collection<? extends E> c) {
      	// 将集合c转为数组 
        Object[] a = c.toArray();
        int numNew = a.length;
      	// 检查是否需要扩容
        ensureCapacityInternal(size + numNew);  // Increments modCount
      	// 将c中元素全部拷贝到数组的最后
        System.arraycopy(a, 0, elementData, size, numNew);
      	// 大小增加c的大小
        size += numNew;
      	// 如果c不为空就返回true，否则返回false
        return numNew != 0;
    }
		
		// 在指定位置，添加一个集合元素
    public boolean addAll(int index, Collection<? extends E> c) {
      	// 检查索引是否在范围内
        rangeCheckForAdd(index);

        Object[] a = c.toArray();
        int numNew = a.length;
        ensureCapacityInternal(size + numNew);  // Increments modCount
				// 原数组中需要平移的元素的数量
        int numMoved = size - index;
        if (numMoved > 0)
          	// 将需要平移的数组元素向后平移数组长度
            System.arraycopy(elementData, index, elementData, index + numNew,
                             numMoved);
				// 将新的集合元素 拷贝目标数组中
        System.arraycopy(a, 0, elementData, index, numNew);
        size += numNew;
        return numNew != 0;
    }

    private void ensureCapacityInternal(int minCapacity) {
        ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
    }

    private static int calculateCapacity(Object[] elementData, int minCapacity) {
      	// 这里就是DEFAULTCAPACITY_EMPTY_ELEMENTDATA 和 EMPTY_ELEMENTDATA 最主要的区别，
      	// 如果是空数组DEFAULTCAPACITY_EMPTY_ELEMENTDATA，就初始化为默认大小10
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
          	// 默认构造第一次add返回10
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
      	// 带参为0构造第一次add返回 1 （0 + 1）
        return minCapacity;
    }

    private void ensureExplicitCapacity(int minCapacity) {
      	// 自增修改计数
        modCount++;

        // overflow-conscious code
      	// 当前数组容量小于需要的最小容量
        if (minCapacity - elementData.length > 0)
          	// 准备扩容数组
            grow(minCapacity);
    }
		
    private void grow(int minCapacity) {
        // overflow-conscious code
      	// 获得当前数组容量
        int oldCapacity = elementData.length;
      	// 新数组容量为1.5倍的旧数组容量
      	// 如果新容量发现比需要的容量还小，则以需要的容量为准
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
          	// 若newCapacity依旧小于minCapacity
            newCapacity = minCapacity;
      	// 如果新容量已经超过最大容量了，则使用最大容量
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
      	// 以新容量拷贝数组到一个新数组
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```

#### 删除

```java
		// 删除指定位置的元素
    public E remove(int index) {
      	// 检查index范围
        rangeCheck(index);
				
        modCount++;
  			// 需要删除的元素
        E oldValue = elementData(index);
				
      	// 如果index不是最后一位，则将index之后的元素往前挪一位
        int numMoved = size - index - 1;
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
      	// 将最后一个元素删除，帮助GC
        elementData[--size] = null; // clear to let GC do its work
				// 返回旧值
        return oldValue;
    }
		
		// 删除指定元素值的元素，时间复杂度为O(n)
    public boolean remove(Object o) {
        if (o == null) {
          	// 遍历整个数组，找到元素第一次出现的位置，并将其快速删除
            for (int index = 0; index < size; index++)
              	// 如果要删除的元素为null，则以null进行比较，使用 “==”
                if (elementData[index] == null) {
                    fastRemove(index);
                    return true;
                }
        } else {
          	// 遍历整个数组，找到元素第一次出现的位置，并将其快速删除
            for (int index = 0; index < size; index++)
              	// 如果要删除的元素不为null，则进行比较，使用 “equals()” 方法
                if (o.equals(elementData[index])) {
                    fastRemove(index);
                    return true;
                }
        }
        return false;
    }

    private void fastRemove(int index) {
        modCount++;
      	// 如果index不是最后一位，则将index之后的元素往前挪一位
        int numMoved = size - index - 1;
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
        elementData[--size] = null; // clear to let GC do its work
    }
		
		// 批量删除 数组中 集合c的元素
    public boolean removeAll(Collection<?> c) {
      	// 集合c 不能为null
        Objects.requireNonNull(c);
        return batchRemove(c, false);
    }
		
		// 批量删除元素
		// complement 为true表示删除数组中，c不包含的元素
		// complement 为false表示删除数组中，c包含的元素
    private boolean batchRemove(Collection<?> c, boolean complement) {
        final Object[] elementData = this.elementData;
        // 使用读写两个指针同时遍历数组
    		// 读指针每次自增1，写指针放入元素的时候才加1
    		// 这样不需要额外的空间，只需要在原有的数组上操作就可以了
        int r = 0, w = 0;
        boolean modified = false;
        try {
          	// 遍历整个数组，如果c中包含该元素，则把该元素放到写指针的位置（以complement为准）
            for (; r < size; r++)
                if (c.contains(elementData[r]) == complement)
                    elementData[w++] = elementData[r];
        } finally {
            // Preserve behavioral compatibility with AbstractCollection,
            // even if c.contains() throws.
          	// 正常来说r最后是等于size的，除非c.contains()抛出了异常
            if (r != size) {
              	// 如果c.contains()抛出了异常，则把未读的元素都拷贝到写指针之后
                System.arraycopy(elementData, r,
                                 elementData, w,
                                 size - r);
                w += size - r;
            }
            if (w != size) {
                // clear to let GC do its work
                for (int i = w; i < size; i++)
                    elementData[i] = null;
                modCount += size - w;
              	// 新大小等于写指针的位置（因为每写一次写指针就加1，所以新大小正好等于写指针的位置）
                size = w;
                modified = true;
            }
        }
        return modified;
    }
```

#### 更新

```java
    // 更新数组指定位置的元素
		public E set(int index, E element) {
      	// 数组index检查
        rangeCheck(index);
				
      	// 取出要更新的位置的元素（旧值）
        E oldValue = elementData(index);
      	// 更新新值
        elementData[index] = element;
      	// 返回旧值
        return oldValue;
    }
```

#### 查找

```java
    // 查找数组
		public E get(int index) {
        rangeCheck(index);

        return elementData(index);
    }
```

#### 序列化问题

`ArrayList`实现了`java.io.Serializable`接口，但是自己定义了序列化和反序列化。这是因为`ArrayList`是基于数组实现，并且具有动态扩容特性，在这个过程当中会进行新老数组的拷贝，因此原来保存元素的数组不一定都会被使用，那么久没必要全部进行序列化。因此 `elementData`数组使用`transient`修饰，可以防止被自动序列化。

```java
    // 序列化
		private void writeObject(java.io.ObjectOutputStream s)
        throws java.io.IOException{
        // Write out element count, and any hidden stuff
      	// 防止序列化期间数组元素有修改
        int expectedModCount = modCount;
      	// 写出非transient非static属性（会写出size属性）
        s.defaultWriteObject();

        // Write out size as capacity for behavioural compatibility with clone()
      	// 序列化数组包含元素数量，为了向后兼容
        // 两次将size写入流
        s.writeInt(size);

        // Write out all elements in the proper order
      	// 按照顺序写入，只写入到数组包含元素的结尾，并不会把数组的所有容量区域全部写入
        for (int i=0; i<size; i++) {
            s.writeObject(elementData[i]);
        }
				
      	// 判断是否触发Fast-Fail
        if (modCount != expectedModCount) {
            throw new ConcurrentModificationException();
        }
    }

		// 反序列化
    private void readObject(java.io.ObjectInputStream s)
        throws java.io.IOException, ClassNotFoundException {
      	// 设置数组引用空数组
        elementData = EMPTY_ELEMENTDATA;

        // Read in size, and any hidden stuff
        // 将流中的的非静态(non-static)和非瞬态(non-transient)字段读取到当前类
        // 包含 size
        s.defaultReadObject();

        // Read in capacity
      	// 读入元素个数，没什么用，只是因为写出的时候写了size属性，读的时候也要按顺序来读
        s.readInt(); // ignored

        if (size > 0) {
            // be like clone(), allocate array based upon size not capacity
          	// 根据size计算容量
            int capacity = calculateCapacity(elementData, size);
          	// 用于调用另一个包中的实现专用方法，而不使用反射。TODO
            SharedSecrets.getJavaOISAccess().checkArray(s, Object[].class, capacity);
          	// 检查是否需要扩容
            ensureCapacityInternal(size);

            Object[] a = elementData;
            // Read in all elements in the proper order.
            for (int i=0; i<size; i++) {
              	// 依次读取元素到数组中
                a[i] = s.readObject();
            }
        }
    }
```

`ArrayList`为什么要序列化两次？

>在序列化的代码中，`s.defaultWriteObject()`;中`size`应该也被序列化了。为什么还要再单独调用`s.writeInt(size)`序列化一次呢？
>
>其实是出于兼容性考虑。
>
>旧版本的JDK中，`ArrayList`实现不同，会对`length`字段序列化；而新版的`JDK`中，优化了实现，不再序列化`length`字段。如果去掉`s.writeInt(size)`，那么新版`JDK`序列化的对象，在旧版本中无法正确反序列化了，因为缺少了`length`字段。

#### 关于`System.arraycopy()`和`Arrays.copyOf()`

通过上面的源码可以知道两种实现数组复制的方法`System.arraycopy()`和`Arrays.copyOf()`，其中`arraycopy`方法实现数组自己复制自己；其中`copyOf`以正确的顺序（从第一个到最后一个元素）返回一个包含此列表中所有元素的数组；

**联系：** 

- 看两者源代码可以发现`copyOf()`内部调用了`System.arraycopy()`方法；

**区别：**

- `arraycopy()`需要目标数组，将原数组拷贝到你自己定义的数组里，而且可以选择拷贝的起点和长度以及放入新数组中的位置；
- `copyOf()`是系统自动在内部新建一个数组，并返回该数组

#### 关于`Fail-Fast`机制

`fail-fast`机制，即快速失败机制，是`Java`集合`(Collection)`中的一种错误检测机制。当在迭代集合的过程中该集合在结构上发生改变的时候，就有可能会发生`fail-fast`，即抛出`ConcurrentModificationException`异常。`fail-fast`机制并不保证在不同步的修改下一定会抛出异常，它只是尽最大努力去抛出，所以这种机制一般仅用于检测`bug`。

> 结构发生变化是指添加或者删除至少一个元素的所有操作，或者是调整内部数组大小，仅仅只是设置元素的值不算结构发生变化。
>
> 在进行序列化或者迭代操作时，需要比较操作前后`modCount`是否改变，如果改变了需要跑出`ConcurrentModificationException`

#### DEMO

```JAVA
public class ArrayListDemo {

    public static void main(String[] srgs){
         ArrayList<Integer> arrayList = new ArrayList<Integer>();

         System.out.printf("Before add:arrayList.size() = %d\n",arrayList.size());

         arrayList.add(1);
         arrayList.add(3);
         arrayList.add(5);
         arrayList.add(7);
         arrayList.add(9);
         System.out.printf("After add:arrayList.size() = %d\n",arrayList.size());

         System.out.println("Printing elements of arrayList");
         // 三种遍历方式打印元素
         // 第一种：通过迭代器遍历
         System.out.print("通过迭代器遍历:");
         Iterator<Integer> it = arrayList.iterator();
         while(it.hasNext()){
             System.out.print(it.next() + " ");
         }
         System.out.println();

         // 第二种：通过随机索引值遍历
         System.out.print("通过索引值遍历:");
         for(int i = 0; i < arrayList.size(); i++){
             System.out.print(arrayList.get(i) + " ");
         }
         System.out.println();

         // 第三种：for循环遍历
         System.out.print("foreach循环遍历:");
         for(Integer number : arrayList){
             System.out.print(number + " ");
         }

         // toArray用法
         // 第一种方式(最常用)
         Integer[] integer = arrayList.toArray(new Integer[0]);

         // 第二种方式(容易理解)
         Integer[] integer1 = new Integer[arrayList.size()];
         arrayList.toArray(integer1);

         // 抛出异常，java不支持向下转型
         //Integer[] integer2 = new Integer[arrayList.size()];
         //integer2 = arrayList.toArray();
         System.out.println();

         // 在指定位置添加元素
         arrayList.add(2,2);
         // 删除指定位置上的元素
         arrayList.remove(2);    
         // 删除指定元素
         arrayList.remove((Object)3);
         // 判断arrayList是否包含5
         System.out.println("ArrayList contains 5 is: " + arrayList.contains(5));

         // 清空ArrayList
         arrayList.clear();
         // 判断ArrayList是否为空
         System.out.println("ArrayList is empty: " + arrayList.isEmpty());
    }
}
```

其中遍历效率最高的是索引随机访问`for`，`foreach`和`iterator`效率差不多。主要原因是`ArrayList`实现了`RandomAccess`接口，可以快速随机访问集合，所以效率比较高。而`foreach`的底层是`for+iterator`实现的，所以效率差不多。

### 总结

- `ArrayList`基于数组方式实现，无容量的限制（会扩容）；
- 添加元素时可能要扩容（所以最好预判一下），删除元素时不会减少容量（若希望减少容量可以使用`trimToSize()`），删除元素时，将删除掉的位置元素置为`null`，下次`gc`就会回收这些元素所占的内存空间；
- 线程不安全；
- `add(int index, E element)`：添加元素到数组中指定位置的时候，需要将该位置及其后边所有的元素都整块向后复制一位；
- `get(int index)`：获取指定位置上的元素时，可以通过索引直接获取`（O(1)）`；
- `remove(Object o)`需要遍历数组；
- `remove(int index)`不需要遍历数组，只需判断`index`是否符合条件即可，效率比`remove(Object o)`高；
- `contains(E)`需要遍历数组；