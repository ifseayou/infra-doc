# Scala

[API地址：](www.scala-lang.org/api)

Scala是一门以虚拟机为运行环境并面向对象和函数式编程的最佳特性结合在一起的静态类型编程语言。

* 支持面向对象和函数式编程
* Scala代码会被编译成`.class`文件在虚拟机上运行

![](img/scala/2.png)

实际发生的是：你输入的内容被快速的编译成字节码，然后这段字节码交给Java虚拟机去执行。

在Scala中，

~~~scala
// 你可以对数字执行方法操作：
scala> 1.toString
res11: String = 1

// 在scala中，使用java.lang.String来表示字符串，但可以通过StringOps类给字符串添加上百种操作
// String对象，"hello"被隐式转化为一个StingOps对象，接着StringOps的 intersect方法被调用
scala> "hello".intersect("world")  // 找出相同的部分
res12: String = lo

/*
Int  		RichInt
Double      RichDouble
Char		RichDouble
在对应的Rich**方法中，提供了更加丰富的方法，来进行数字的操作
*/

// 这里的1被转为RichInt对象，然后调用其to方法
scala> 1.to(6)
res14: scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5, 6)
~~~

### Chapter1

#### 算术和操作符号的重载

在Scala中，

~~~scala
// 在Scala中，a+b 其实是方法的调用，a.+(b)这里的
scala> 1+2
res18: Int = 3

scala> 1.+(2)
res17: Int = 3

/* 通常，你可以使用  
a 方法 b
来替代
a.方法（参数）
*/
~~~

#### Scala中的方法和函数

函数：在Scala中，你不需要调用某个特定类的静态方法来实现类似与求平方等操作。只是需要一个导包的操作：

~~~Scala
scala> import scala.math._  // 以 scala为前缀的包，可以省略scala.
import scala.math._

scala> pow(2,2)
res20: Double = 4.0
~~~

通常在Scala中，每一个类都会有一个伴生对象，其方法和Java的静态方法一样。例如，BigInt类有一个生成随机素数的方法，调用的形式和java几乎是一样的：

~~~scala 
scala> BigInt.probablePrime(100,scala.util.Random)
res23: scala.math.BigInt = 940640853769843387998341502449
~~~

#### apply方法

在Scala中使用**apply**方法构建对象的手法是`scala`创建对象的常用手法

~~~scala
scala> "Hello"(4)
res25: Char = o

// 上述的写法实际上是下面写法的简写
scala> "Hello".apply(4)
res26: Char = o

// 将数字转为BigInt对象的apply方法，
scala> BigInt("12334")
res27: scala.math.BigInt = 12334

// 上面语句是下面语句的简写，这个语句构建了一个新的BigInt对象，而不使用new
scala> BigInt.apply("12334")
res28: scala.math.BigInt = 12334
~~~

### Chapter2

#### 表达式

***Scala语言中的表达式是有值，有类型的。***

~~~scala
if(x >0) 1 else -1

// 上述的表达式是有值的，要么为1，要么为-1，
val s = if(x > 0) 1 else - 1  // 此时的s可以为val

// 也就等价于
if(x > 0) s = 1 else s = -1  // 此时的s必须是var
~~~

上述的表达式是有类型的，上面的表达式的类型是`Int`，因为两个分支都是`Int`类型，如果两个分支的类型不一样，那么就是两个类型的超类型。例如：

~~~scala
if (x > 0) "positive" else -1 // 此时该表达式的类型就是两个类型的公共超类型：Any

// 如果是下面的这个语句，没有else的情况的时候，这个表达式的值是Unit类型，该类型只有一个值（）
if (x>0) 1  // 这个语句等同于
if(x>0) 1 else ()  
~~~

在REPL中键入多行代码：

~~~scala
scala> :paste
// Entering paste mode (ctrl-D to finish)

val x = 2
if (x > 0 ) "positive" else -1

// Exiting paste mode, now interpreting.  使用  ctrl + D来结束输入

x: Int = 2
res40: Any = positive
~~~

**语句块{} 的值取决于语句块中最后一个表达式的值**，

#### 循环

**to ** 和 **until**  的区别在于，前者包含最后一个元素，而后者不包含

~~~scala
for(i <- 表达式)  // 让变量i去遍历表达式所有的值，举个例子

for(i <- 1 to n) // i 遍历 [1,n] 之间所有的值

// 直接遍历字符串所有的值
scala> for(i<-"Hello") print(i+"\t")
H       e       l       l       o
~~~

#### 如何break

这里提供一种方法是：`scala.util.control.Breaks`

#### 双层for循环

~~~scala
// 这里生成器之间要使用；隔开
scala> for(i<-1 to 3;j <- "cat") print( i+""+ j + "\t")
1c      1a      1t      2c      2a      2t      3c      3a      3t

// 每个生成器后面可以添加守卫
scala> for(i<-1 to 3;j <- "cat" if j != 'c') print( i+""+ j + "\t")
1a      1t      2a      2t      3a      3t

// for 循环体以yield开始的话，则该循环会构造出来一个集合
scala> for(i <- 1 to 6) yield i % 3
res8: scala.collection.immutable.IndexedSeq[Int] = Vector(1, 2, 0, 1, 2, 0)
~~~

#### 函数

Scala处了方法，还支持函数，方法对对象进行操作，函数不是。在Java中我们只能使用静态方法来模拟函数。

下面是Scala中函数的定义和使用：

![](img/scala/3.png)

函数的返回值类型，Scala自己会根据函数体的最后一个表达式的值来进行确定，所以不指定返回类型是很好的，除了**该函数是递归函数，如果是递归函数，必须指定该函数的返回类型**

#### 默认参数

![](img/scala/4.png)

#### 变长参数

如下例子：

![](img/scala/5.png)

#### 过程

Scala对于不返回值的函函数叫做过程，**过程** 不返回值，调用它仅仅是为了她的副作用。例如下面的box过程例子：

~~~java
/**
  * -------------
  * |Hello world|
  * -------------
  */

object ScalaGrammer {
  def main(args: Array[String]): Unit = { // 
    box("Hello world")
  }
  def box(s:String): Unit = {
    val border = "-" * s.length + "--\n"
    println(border + "|" + s + "|\n" + border)
  }
}
~~~

上面的过程是显示定义返回类型是***Unit***，下面的方式是直接省略这一过程：

![](img/scala/6.png)

#### Lazy懒值

懒值对于开销较大的初始化语句比较有用，懒值是位于***`val`和def***的中间状态：

~~~ scala
    // 在word1定义的时候即被取值
    val word1 = scala.io.Source.fromFile("").mkString
    // 在words首次被使用的是时候，被取值
    lazy val word2 = scala.io.Source.fromFile("").mkString

  // 在每一次words首次使用的时候取值
  def words = scala.io.Source.fromFile("**").mkString
~~~

### Chapter3 数组

* 若长度固定使用 ***Array*** ，如果长度不固定，使用***`ArrayBuffer`***

* 提供初始值的时候不要使用new
* 使用***（）***来访问元素
* 使用***`for(ele <-arr)`***来遍历元素
* 使用***`for(ele<-arr if...)...yield...`*** 来讲原数组转型为新数组
* Scala数组和java数组可以相互转化：用`ArrayBuffer`，使用`scala.collection.JavaConversions`中的转换函数。

#### 定长数组

Scala中的Array是Java数组方式实现的，下面例子中的Array[String] 的类型在JVM中就是`java.lang.String[]` ，Array[1,2,3] 在JVM中就是***`int[]`***

![](img/scala/7.png)

#### 变长数组：数组缓冲

长度变化的数组在java中的是`ArrayList`，在Scala中等效是`ArrayBuffer`

![](img/scala/8.png)

遍历数组：

![](img/scala/9.png)

**从数组出发，你会得到一个新的数组，从缓冲数组出发，你会得到一个缓冲数组**

![](img/scala/10.png)

#### 算法

~~~java
  val sum = Array(4, 2, 3)
    println(sum.sum) // 9
    println(ArrayBuffer("Mary", "had", "a", "little", "boy").max) // little
    // sorted方法将原有的数组或者是缓冲数组排序
    // 并返回新的数组或者是数组缓冲,原有的数组或者是缓冲数组不会被改变
    val sorted: Array[Int] = sum.sorted
    for (i <- sorted) print(i + "\t")  // 2	3	4

    val arr = Array(1,7,2,9)
    // 可以直接对一个数组排序，但是不能直接对缓冲数组排序
    scala.util.Sorting.quickSort(arr)
    // 此时arr的被改变了 ,参数的为是三个的时候，前缀，分隔符，后缀
    println(arr) // [I@6574b225 直接打印一个Array没有意义
    println(arr.mkString("<", ",", ">"))  // <1,2,7,9>
~~~

### Character4：映射和元组

#### 映射的创建，添加，更新，删除

~~~scala
// 构建一个不可变的Map[String,Int] 其值不能被改变
val score1 = Map("Alice" -> 10,"Bob" -> 3,"Cindy" -> 8)
// 构建一个可以改变的映射，-> 操作符号用来创建对偶
val score2 = scala.collection.mutable.Map("Aice"->10,"Bob" -> 3,"Cindy"->8)

// 更新Map的值
score2("Alice") = 100

// 使用 +=操作来添加多个关系
score2 += ("Ice" -> 20,"Linda" -> 22)

// 使用 -= 来减少多个关系
score2 -= ("Ice") // 注意这里只是需要填写键就OK了

// 如果想从一个空的映射开始，需要选定映射的实现并给出参数类型
val scores = new mutable.HashMap[String,Int]()

// 使用括号的方式来构建映射
val score3 = Map(("Alice",10),("Bob",3),("cindy",8))

// 获取score3中的值
val bobsScore: Int = score3.getOrElse("Bob",0)

// 你不能更新一个不可变的映射，但是你可以根据一个不可变的映射得到一个新的映射
val newScore: Map[String, Int] = score1 + ("Baby" -> 33,"Lind"-> 23)
~~~

#### 映射的迭代和反转

~~~scala
// 构建一个不可变的Map[String,Int] 其值不能被改变
val score1 = Map("Alice" -> 10, "Bob" -> 3, "Cindy" -> 8)
// 映射的迭代
for ((k, v) <- score1) println(k + "->" + v)

// 分别迭代映射的key 和value
for (k <- score1.keySet) print(k + "\t")
for (v <- score1.values) print(v + "\t")

// 将映射反转
for ((k,v) <- score1) yield (v,k)
~~~

在操作映射的时候，你需要选定一个实现，一个哈希表或者是一个平衡树，默认情况下，scala给的是哈希表，`scala`中的不可变的树形映射是：

~~~scala
val sortedMap = scala.collection.immutable.SortedMap("A" -> 1,"B"-> 2)

// 如果希望按照插入的顺序访问所有的键，和java一样使用LinkedHashMap
scala.collection.mutable.LinkedHashMap("Jun"->1,"Fub"->2)
~~~

#### 元组

~~~scala
// 元组
val tuple: (String, Int, Boolean) = ("Bob",20,false)
// 获取tuple的第二个值
tuple._2

// 通常使用模式匹配来获取元组的组元，如下，并不是所有的部件都需要类型，不需要的使用_
val tuple2: (String, Int, _) = tuple

// 元组可以用于函数需要返回不止一个值的情况，如StringOps的partition方法
println("New York".partition(_.isUpper)) // (NY,ew ork)
~~~

#### 拉链

使用元组的目的：把多个值绑定在一起，以便他们能够被一起处理。通常使用**Zip**方法来完成

~~~scala
val symbols = Array("<", "-", ">")
val counts = Array(2,10,2)
// 拉链，将两个数组的值拉在一起
val pairs: Array[(String, Int)] = symbols.zip(counts)
for ((s,n)<-pairs) print(s * n) //<<---------->>

// 将对偶的集合转为映射
val map: Map[String, Int] = pairs.toMap
~~~

### Chapter5：类

* 类中的字段自动带有getter和setter方法
* 你可以用定制的getter/setter方法替换掉字段定义，而不必修改使用类的客户端--即统一访问原则
* 使用`@BeanProperty` 注解来生成`JavaBean`的`getXxx/setXxx`方法
* 每个类都有一个主要的构造器，这个构造器和类定义，交织在一起，他的参数直接成为类的字段，主构造器执行类中所有的语句。
* 辅助构造器是可选的，他们都叫***this***

#### 简单类和无参方法

~~~scala
object ScalaGrammer {
  def main(args: Array[String]): Unit = {
    val myCounter = new Counter
    // 对于调用无参方法，可以写上括号，也可以不写
    myCounter.increment() // 对于改值器的方法，即改变对象状态的方法，使用()
    println(myCounter.current) // 对于取值器的方法（不会改变对象状态的方法）去掉()
  }
}

// 在Scala中，类并不声明为public，Scala源文件可以包含多个类，所有的这些类都具有公有可见性
class Counter{
  private var value = 0 // 你必须初始化字段
  def increment() = {value += 1 }

  def current() = value
  def cur = value // 可以使用通过不带()的方法声明current来强制以上的风格
}
~~~

#### `getX和setX`

```scala
class Person{
  var age = 0 // 必须初始化
}

// scala在生成面向JVM的类的啥时候，其中有一个私有的age字段和相应的getter和setter方法
// 这两个方法是公有的，因为我们没有将age声明为private，对私有的字段来说，getter和setter
// 方法是私有的。scala中的getter和setter叫做：age 和 age_=

/**
  * 如果字段是私有的，则getter和setter方法也是私有的
  * 如果字段是val，则只有getter方法被生成
  */
```

#### 只带getter属性

如果属性的值在对象构建完成之后就不在改变，则可以使用***`val`***字段，

~~~scala
class Message{
  val date = new java.util.Date
  // scala会生成一个私有的final字段和一个getter方法，没有setter
}
~~~

**Scala中，方法可以访问该类的所有对象的私有字段，和java一样。**

~~~scala
class Counter{
  private var value = 0
  def increment() {value += 1}
  def isLess(other:Counter) = value < other.value
  // 可以访问另外一个对象的私有字段
}
~~~

很多Java工具有依赖setter和getter的命名习惯，如果想要这样的方法：

~~~scala
class Person{
  @BeanProperty var name :String = _
  /**
    * 会生成：
    *       name
    *       name_=
    *       getName()
    *       setName()
    */
}
~~~

#### 辅助构造器

* 辅助构造器的名字是***this***
* 每一个辅助构造器都由其他辅助构造器或者是主构造器开始

#### 主构造器

下面是一个java类：

```java 
public class PersonJ {
    private String name;
    private int age;
    public PersonJ(String name,int age){
        this.name = name;
        this.age = age;
    }
    public String nage(){return name;}
    public int age(){return age;}
}
```

Scala只需要下面的代码就能搞定

~~~scala 
class PersonS(val name:String,val age :Int){ // 注意这里是val，是没有set方法的
}
~~~

Scala中，每一个类都有主构造器，***主构造器和类交织在一起***。

~~~scala
class PersonS(val name:String,val age :Int){
  print("PersonS is coming...")
  // print语句是主构造器的一部分，每当有对象被构造出来的时候，上述的代码就会被执行
  // 当你需要在构造的过程中配置某个字段的时候，特别有用
}
~~~

通常可以通过在主构造器中使用默认参数来避免过多的使用辅助构造器。

~~~scala
class Person(val name:String="",val age:Int=0)
~~~

**在Scala中，类也接收参数，就像方法一样。** 如果构造参数不带`val`或`var`的参数至少被一个方法使用，她将被升为字段。否则，该参数将不被保存为字段，仅仅是一个可以被主构造器访问的普通参数。

![](img/scala/13.png)

#### 嵌套类

在Scala中，你可以在函数中定义函数，在类中定义类：

### Chapter 对象

* 用对象作为单例或者存放工具方法
* 类可以拥有一个同名的伴生对象
* 对象可以扩展类或特质
* 对象的apply方法通常用来构造伴生类的新实例
* 如果不想显示定义main方法，可以扩展APP特质的对象
* 你可以通过enumeration对象来实现枚举

#### 单例对象

Scala中没有静态方法或者静态字段，你可以用object这个语法来达到同样的目的，对应定义了某个类的单个实例，包含你想要的特性，如：

~~~scala
object Accounts {
  private var lastNumber = 0 
  def newUniqueNumber() = { lastNumber += 1; lastNumber}
} 
// 当你的程序需要一个新的唯一的账号的时候，调用
Account.newUniqueNumber() //即可
~~~

对象的构造器在对该对象第一次调用时使用，如果一个对象从未被使用，那么其构造器也不会被执行。对象本质上拥有类的所有特性。scala中使用对象来实现：

* 作为存放工具函数或者是常量的地方
* 高效的共享单个不可变实例
* 需要单个实例来协调调某个服务的时候

类和它的 伴生对象可以相互访问私有属性，但是他们必须在同一个文件中。

#### 扩展类或者特质的对象

一个object可以扩展类以及一个或者多个特质，其结果是扩展了指定类和特质类的对象，同时游泳堆中定义中给出的所有特性。

#### apply方法

通常会定义和使用对象的apply方法，如果遇到

~~~scala
Object(parm1,,parmN)
~~~

通常apply方法返回的是伴生类的对象。如：Array对象定义了apply方法，让我们可以使用下面的方法来创建数组：

~~~scala 
Array("marry","had","a","toy")
~~~

为什么不使用构造器呢？对于嵌套表达式来说，省去new关键词会很方便：

~~~scala 
Array(Array(1,7),Array(2,3))
~~~

这里注意的：

~~~scala 
Array(100)  # 调用的是：apply(100)，单元素Array[Int]
new Array(100)  # 调用的是 this(100),Array[Nothing] 包含100个null元素
~~~

#### 应用程序对象

每个`scala`程序都必须从一个对象的main方法开始，处理每次都提供自己的main方法之外，还可以扩展APP特质，然后将程序代码放入构造器方法体内：

~~~scala 
object Hello{
  def main(args: Array[String]): Unit = {
    println("hello scala....")
  }
}

object HelloAPP extends App{
  println("hello , app")
}
~~~

### 特质

#### 当做接口使用

~~~scala
trait Logger{
    def log(msg:String)// 这是个抽象方法，不需要声明为abstract，特质中未被实现的方法就是抽象方法
}
~~~

子类可以给出实现：

~~~scala 
class ConsoleLogger extends Logger with AnotherTrait{ 
    // 这里使用extend不是implements
    def log(msg:String) {println(msg)} //  不需要写override
}
~~~

和java一样，`scala`类只能有一个超类，但可以有任意数量的特质。在Scala中，特质中的方法不一定是抽象的。这一点和java是不一样的。















## Scala开发环境的搭建

和安装JDK的步骤几乎一致，这里不做介绍。在Windows环境和Linux环境下均可。

## Scala的hello-world

基于在IDEA的环境下开发，第一次使用开发工具开发`Scala`的项目的时候，注意要引入Scala框架

## Scala的数据类型等

* `val` 表示的是常量的定义，常量确定值之后是不能被修改的

* `var` 表示的变量的定义，声明变量的时候必须进行初始化，不能先声明在初始化，声明变量的时候可以不进行初始化，Scala会进行类型推断

* 每个语句的后面不需要添加分号；

* Scala中的数据类型主要有两类，值类型`AnyVal`和引用类型`AnyRef`


注释和java一样，单行注释，多行注释，文档注释



![1564701046179](img/scala/1.png)



Scala中的运算符都是以方法的形式存在的。



## 小tip





## 伴生对象

* 使用 **Object** 来声明，伴生对象中声明的都是"静态内容" 可以用伴生对象名称直接调用。
* 和伴生对象对应的是伴生类，伴生类的所有的静态信息都可以放置在伴生对象中。

## 样例类和模式匹配

- 样例类是为了模式匹配而生
- 在样例类对应的伴生对象中提供了`apply`方法，可以让你不需要new就可以创建对象。
- 提供了`unapply`方法可以让模式匹配可以工作

## Spark源码中常用Scala语法

~~~scala
// ClassTag 表示可推断类型  
map[U: ClassTag]

//表示类型是可以变化的。
(f: T => U) 

def parallelize[T: ClassTag](
    seq: Seq[T],
    numSlices: Int = defaultParallelism): RDD[T] = withScope {
  assertNotStopped()
  new ParallelCollectionRDD[T](this, seq, numSlices, Map[Int, Seq[String]]())
}

// 这就是Scala的函数，一个函数其中有两个参数，函数的返回类型是RDD[T] 函数体就是 withScopt{}
defaultParallelism 是默认并行度，这是一个方法。

~~~



### 调用函数时使用{}来传递参数

