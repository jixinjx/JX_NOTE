# 接口

在Java 程序设计语言中， 接口不是类，而是对类的一组需求描述，这些类要遵从接口描
述的统一格式进行定义。

我们经常听到服务提供商这样说：“ 如果类遵从某个特定接口，那么就履行这项服务' 下面给出一个具体的示例。Arrays 类中的sort 方法承诺可以对对象数组进行排序， 但要求满
足下列前提： 对象所属的类必须实现了Comparable 接口。



```java
public interface Comparable<T>
{
int compareTo(T other) ; / / parameter has type T
}
```

例如，在实现Comparable<Employee> 接口的类中， 必须提供下列方法

java

int coirpareTo(Employee other)


还可以使用不带类型参数的“ 原始” Comparable 类型。这样一来， compareTo 方法
就有一个Object 类型的参数， 必须手动将compareTo 方法的这个参数强制转换为所希望
的类型.

接口中的所有方法自动地属于public。因此， 在接口中声明方法时， **不必提供关键字**
**public**



# 类

## 定义子类

在Java 中， 所有的继承都是公有继承

```
public class Manager extends Employee
{

}
```







这使得代码具有更好的可读性。人们一看就知道这个数组列表中包含的是String 对象。

在Java SE 7 及以后的版本中， 构造函数中可以省略泛型类型：

```java
ArrayList<String> files = new ArrayList<>()；
```



## 泛型类

Pair 类引人了一个类型变量T，用尖括号( < >) 括起来，并放在类名的后面。泛型类可
以有多个类型变量。例如， 可以定义Pair 类，其中第一个域和第二个域使用不同的类型：

使用了Pair 类。静态的minmax 方法遍历了数组并同时计算出最小值和最大值。它用一个Pair 对象返回了两个结果。回想compareTo 方法比较两个字符串， 如果字符串相同则返回0 ; 如果按照字典顺序， 第一个字符串比第二个字符串靠前， 就返回负值， 否则， 返回正值。

```java
package pair1;

/**
 * @version 1.00 2004-05-10
 * @author Cay Horstmann
 */
public class Pair<T> 
{
   private T first;
   private T second;

   public Pair() { first = null; second = null; }
   public Pair(T first, T second) { this.first = first;  this.second = second; }

   public T getFirst() { return first; }
   public T getSecond() { return second; }

   public void setFirst(T newValue) { first = newValue; }
   public void setSecond(T newValue) { second = newValue; }
}

```



```java
package pair1;

/**
 * @version 1.01 2012-01-26
 * @author Cay Horstmann
 */
public class PairTest1
{
   public static void main(String[] args)
   {
      String[] words = { "Mary", "had", "a", "little", "lamb" };
      Pair<String> mm = ArrayAlg.minmax(words);
      System.out.println("min = " + mm.getFirst());
      System.out.println("max = " + mm.getSecond());
   }
}

class ArrayAlg
{
   /**
    * Gets the minimum and maximum of an array of strings.
    * @param a an array of strings
    * @return a pair with the min and max value, or null if a is null or empty
    */
   public static Pair<String> minmax(String[] a)
   {
      if (a == null || a.length == 0) return null;
      String min = a[0];
      String max = a[0];
      for (int i = 1; i < a.length; i++)
      {
         if (min.compareTo(a[i]) > 0) min = a[i];
         if (max.compareTo(a[i]) < 0) max = a[i];
      }
      return new Pair<>(min, max);
   }
}

```

## 泛型方法

前面已经介绍了如何定义一个泛型类。实际上，还可以定义一个带有类型参数的简单方法。

```
class ArrayAlg
{
public static <T> T getMiddle(T... a)
{
return a[a.length / 2];
}
}
```

这个方法是在普通类中定义的， 而不是在泛型类中定义的。然而，这是一个泛型方法，
可以从尖括号和类型变量看出这一点。注意，类型变量放在修饰符（这里是public static ) 的
后面，返回类型的前面。泛型方法可以定义在普通类中，也可以定义在泛型类中。
当调用一个泛型方法时’在方法名前的尖括号中放人具体的类型：

```
String middle = ArrayAlg.<String>getMiddle("]ohnM, "Q.n, "Public");
```

## 类型变量的限定

变量smallest 类型为T, 这意味着它可以是任何一个类的对象。怎么才能确信T 所属的类有compareTo 方法呢？
解决这个问题的方案是将T 限制为实现了Comparable 接口（只含一个方法compareTo 的标准接口）的类。可以通过对类型变量T 设置限定（bound) 实现这一点：

```
public static <T extends Coiparab1e> T a) . . .
```

实际上Comparable 接口本身就是一个泛型类型。目前， 我们忽略其复杂性以及编译器产
生的警告。第8.8 节讨论了如何在Comparable 接口中适当地使用类型参数。现在，泛型的min 方法只能被实现了Comparable 接口的类（如String、LocalDate 等）的数组调用。由于Rectangle 类没有实现Comparable 接口， 所以调用min 将会产生一个编译错误。



重新编写了一个泛型方法minmax。这个方法计算泛型数组的
最大值和最小值， 并返回Pair<T>。

```
package pair2;

/**
 * @version 1.00 2004-05-10
 * @author Cay Horstmann
 */
public class Pair<T> 
{
   private T first;
   private T second;

   public Pair() { first = null; second = null; }
   public Pair(T first, T second) { this.first = first;  this.second = second; }

   public T getFirst() { return first; }
   public T getSecond() { return second; }

   public void setFirst(T newValue) { first = newValue; }
   public void setSecond(T newValue) { second = newValue; }
}

```



```
package pair2;

import java.time.*;

/**
 * @version 1.02 2015-06-21
 * @author Cay Horstmann
 */
public class PairTest2
{
   public static void main(String[] args)
   {
      LocalDate[] birthdays = 
         { 
            LocalDate.of(1906, 12, 9), // G. Hopper
            LocalDate.of(1815, 12, 10), // A. Lovelace
            LocalDate.of(1903, 12, 3), // J. von Neumann
            LocalDate.of(1910, 6, 22), // K. Zuse
         };
      Pair<LocalDate> mm = ArrayAlg.minmax(birthdays);
      System.out.println("min = " + mm.getFirst());
      System.out.println("max = " + mm.getSecond());
   }
}

class ArrayAlg
{
   /**
      Gets the minimum and maximum of an array of objects of type T.
      @param a an array of objects of type T
      @return a pair with the min and max value, or null if a is 
      null or empty
   */
   public static <T extends Comparable> Pair<T> minmax(T[] a) 
   {
      if (a == null || a.length == 0) return null;
      T min = a[0];
      T max = a[0];
      for (int i = 1; i < a.length; i++)
      {
         if (min.compareTo(a[i]) > 0) min = a[i];
         if (max.compareTo(a[i]) < 0) max = a[i];
      }
      return new Pair<>(min, max);
   }
}

```



# 集合框架

## 队列

队列接口指出可以在队列的尾部添加元素， 在队列的头部删除元素，并且可以査找队列中元素的个数。当需要收集对象， 并按照“ **先进先出**” 的规则检索对象时就应该使用队列

当在程序中使用队列时，一旦构建了集合就不需要知道究竟使用了哪种实现。因此， 只
有在构建集合对象时，使用具体的类才有意义。可以使用接口类型存放集合的引用。

```
Queue<Customer> expresslane = new CircularArrayQueue<>(100) :
expressLane.add(new Customer("Harry"));
```

## Collection 接口

在Java 类库中，集合类的基本接口是Collection 接口。这个接口有两个基本方法:

```
public interface Collection<b
{
boolean add(E element);
Iterator<E> iterator()；
...
}
```

add 方法用于向集合中添加元素。如果添加元素确实改变了集合就返回true, 如果集合
没有发生变化就返回false。例如， 如果试图向集中添加一个对象， 而这个对象在集中已经存
在，这个添加请求就没有实效，因为**集中不允许有重复的对象**。
iterator 方法用于返回一个实现了Iterator 接口的对象。可以使用这个迭代器对象依次访
问集合中的元素。

## 迭代器

Iterator 接口包含4 个方法：

```

public interface Iterator<E>
{
E next();
boolean hasNext();
void remove();
default void forEachRemaining(Consumer<? super E> action) ;
}

```

通过反复调用next 方法，可以逐个访问集合中的每个元素。但是， 如果到达了集合的末尾，next 方法将抛出一个NoSuchElementException。因此，需要在调用next 之前调用hasNext方法。如果迭代器对象还有多个供访问的元素， 这个方法就返回true。如果想要査看集合中的所有元素，就请求一个迭代器，并在hasNext 返回true 时反复地调用next 方法。例如：

```
Collection<String> c = . . .;
Iterator<String> iter = c.iterator()；
while (iter.hasNextO)
{
String element = iter.next()；
do something with element
}

```

用“ foreach” 循环可以更加简练地表示同样的循环操作：

```
for (String element : c)
{
do something with element
}
```

在Java SE 8 中， 甚至不用写循环。可以调用forEachRemaining 方法并提供一lambda
表达式（它会处理一个元素）。将对迭代器的每一个元素调用这个lambda 表达式，直到再没
有元素为止。

```
i terator.forEachRemai ni ng(el ement -> do something with element) ;
```

### Iterator 接口的remove 方法

Iterator 接口的remove 方法将会删除上次调用next 方法时返回的元素。在大多数情况
下，在决定删除某个元素之前应该先看一下这个元素是很具有实际意义的。然而， 如果想要
删除指定位置上的元素， 仍然需要越过这个元素。例如， 下面是如何删除字符串集合中第一
个元素的方法：

```
Iterator<String> it = c.iterator()
it.next(); // skip over the first element
it.remove() ; // now remove it
```

更重要的是，对next 方法和remove 方法的调用具有互相依赖性。如果**调用remove 之前**
**没有调用next 将是不合法的**。如果这样做， 将会抛出一个IllegalStateException 异常。
如果想删除两个相邻的元素， 不能直接地这样调用：

```
it.remove()；
it.remove()； // Error!
```

相反地， 必须先调用next 越过将要删除的元素。

```
it.remove();
it.next()；
it.remove() ; // OK
```

