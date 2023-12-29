# Java学习笔记2

## 类的继承

继承是java面向对象编程技术的一块基石，因为它允许创建分等级层次的类。
继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。

### 类的继承格式

    class 父类 {
    }
    
    class 子类 extends 父类 {
    }

### 为什么需要继承

接下来我们通过实例来说明这个需求。
开发动物类，其中动物分别为企鹅以及老鼠，要求如下：

- 企鹅：属性（姓名，id），方法（吃，睡，自我介绍）
- 老鼠：属性（姓名，id），方法（吃，睡，自我介绍）

#### 企鹅类：

    public class Penguin { 
        private String name; 
        private int id; 
        public Penguin(String myName, int  myid) { 
            name = myName; 
            id = myid; 
        } 
        public void eat(){ 
            System.out.println(name+"正在吃"); 
        }
        public void sleep(){
            System.out.println(name+"正在睡");
        }
        public void introduction() { 
            System.out.println("大家好！我是"    + id + "号" + name + "."); 
        } 
    }

#### 老鼠类：

    public class Mouse { 
        private String name; 
        private int id; 
        public Mouse(String myName, int  myid) { 
            name = myName; 
            id = myid; 
        } 
        public void eat(){ 
            System.out.println(name+"正在吃"); 
        }
        public void sleep(){
            System.out.println(name+"正在睡");
        }
        public void introduction() { 
            System.out.println("大家好！我是"     + id + "号" + name + "."); 
        } 
    }

从这两段代码可以看出来，代码存在重复了，导致后果就是代码量大且臃肿，而且维护性不高(维护性主要是后期需要修改的时候，就需要修改很多的代码，容易出错)，所以要从根本上解决这两段代码的问题，就需要继承，将两段代码中相同的部分提取出来组成 一个父类：

#### 公共父类：

    public class Animal { 
        private String name;  
        private int id; 
        public Animal(String myName, int myid) { 
            name = myName; 
            id = myid;
        } 
        public void eat(){ 
            System.out.println(name+"正在吃"); 
        }
        public void sleep(){
            System.out.println(name+"正在睡");
        }
        public void introduction() { 
            System.out.println("大家好！我是"         + id + "号" + name + "."); 
        } 
    }

这个Animal类就可以作为一个父类，然后企鹅类和老鼠类继承这个类之后，就具有父类当中的属性和方法，子类就不会存在重复的代码，维护性也提高，代码也更加简洁，提高代码的复用性（复用性主要是可以多次使用，不用再多次写同样的代码） 继承之后的代码：

#### 企鹅类：

    public class Penguin extends Animal { 
        public Penguin(String myName, int myid) { 
            super(myName, myid); 
        } 
    }

#### 老鼠类：

    public class Mouse extends Animal { 
        public Mouse(String myName, int myid) { 
            super(myName, myid); 
        } 
    }

*需要注意的是 Java 不支持多继承，但支持多重继承。*

### 继承的特性

- 子类拥有父类非 private 的属性、方法。
- 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。
- 子类可以用自己的方式实现父类的方法。
- Java 的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类，多重继承就是，例如 B 类继承 A 类，C 类继承 B 类，所以按照关系就是 B 类是 C 类的父类，A 类是 B 类的父类，这是 Java 继承区别于 C++ 继承的一个特性。
- 提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系越紧密，代码独立性越差）。

### 继承关键字

继承可以使用 extends 和 implements 这两个关键字来实现继承，而且所有的类都是继承于 java.lang.Object，当一个类没有继承的两个关键字，则默认继承 Object（这个类在 **java.lang** 包中，所以不需要 **import**）祖先类。

#### extends关键字

在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。

    public class Animal { 
        private String name;   
        private int id; 
        public Animal(String myName, int myid) { 
            //初始化属性值
        } 
        public void eat() {  //吃东西方法的具体实现  } 
        public void sleep() { //睡觉方法的具体实现  } 
    } 
     
    public class Penguin  extends  Animal{ 
    }

#### implements关键字

使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。

    public interface A {
        public void eat();
        public void sleep();
    }
     
    public interface B {
        public void show();
    }
     
    public class C implements A,B {
    }

#### super 与 this 关键字

- super关键字：我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类。
- this关键字：指向自己的引用。

```
class Animal {
  void eat() {
    System.out.println("animal : eat");
  }
}
 
class Dog extends Animal {
  void eat() {
    System.out.println("dog : eat");
  }
  void eatTest() {
    this.eat();   // this 调用自己的方法
    super.eat();  // super 调用父类方法
  }
}
 
public class Test {
  public static void main(String[] args) {
    Animal a = new Animal();
    a.eat();
    Dog d = new Dog();
    d.eatTest();
  }
}
```

输出结果为：

    animal : eat
    dog : eat
    animal : eat

#### final 关键字

final 可以用来修饰变量（包括类属性、对象属性、局部变量和形参）、方法（包括类方法和对象方法）和类。
final 含义为 "最终的"。
使用 final 关键字声明类，就是把类定义定义为最终类，不能被继承，或者用于修饰方法，该方法不能被子类重写：

- 声明类：

        final class 类名 {//类体}

- 声明方法：

        修饰符(public/private/default/protected) final 返回值类型 方法名(){//方法体}

*注： final 定义的类，其中的属性、方法不是 final 的。*

### 构造器

子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。如果父类的构造器带有参数，则必须在子类的构造器中显式地通过` super` 关键字调用父类的构造器并配以适当的参数列表。

如果父类构造器没有参数，则在子类的构造器中不需要使用` super `关键字调用父类构造器，系统会自动调用父类的无参构造器。

    class SuperClass {
      private int n;
      SuperClass(){
        System.out.println("SuperClass()");
      }
      SuperClass(int n) {
        System.out.println("SuperClass(int n)");
        this.n = n;
      }
    }
    // SubClass 类继承
    class SubClass extends SuperClass{
      private int n;
      
      SubClass(){ // 自动调用父类的无参数构造器
        System.out.println("SubClass");
      }  
      
      public SubClass(int n){ 
        super(300);  // 调用父类中带有参数的构造器
        System.out.println("SubClass(int n):"+n);
        this.n = n;
      }
    }
    // SubClass2 类继承
    class SubClass2 extends SuperClass{
      private int n;
      
      SubClass2(){
        super(300);  // 调用父类中带有参数的构造器
        System.out.println("SubClass2");
      }  
      
      public SubClass2(int n){ // 自动调用父类的无参数构造器
        System.out.println("SubClass2(int n):"+n);
        this.n = n;
      }
    }
    public class TestSuperSub{
      public static void main (String args[]){
        System.out.println("------SubClass 类继承------");
        SubClass sc1 = new SubClass();
        SubClass sc2 = new SubClass(100); 
        System.out.println("------SubClass2 类继承------");
        SubClass2 sc3 = new SubClass2();
        SubClass2 sc4 = new SubClass2(200); 
      }
    }

输出结果为：

    ------SubClass 类继承------
    SuperClass()
    SubClass
    SuperClass(int n)
    SubClass(int n):100
    ------SubClass2 类继承------
    SuperClass(int n)
    SubClass2
    SuperClass()
    SubClass2(int n):200

## Java 多态

多态是同一个行为具有多个不同表现形式或形态的能力。
多态就是同一个接口，使用不同的实例而执行不同操作。

### 多态的优点

1. 消除类型之间的耦合关系
2. 可替换性
3. 可扩充性
4. 接口性
5. 灵活性
6. 简化性

### 多态存在的三个必要条件

- 继承
- 重写
- 父类引用指向子类对象：`Parent p = new Child();`

```
class Shape {
    void draw() {}
}
  
class Circle extends Shape {
    void draw() {
        System.out.println("Circle.draw()");
    }
}
  
class Square extends Shape {
    void draw() {
        System.out.println("Square.draw()");
    }
}
  
class Triangle extends Shape {
    void draw() {
        System.out.println("Triangle.draw()");
    }
}
```

当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，再去调用子类的同名方法。
*多态的好处：可以使程序有良好的扩展，并可以对所有类的对象进行通用处理。*

### 重写

方法的重写，也就是子类能够重写父类的方法。
当子类对象调用重写的方法时，调用的是子类的方法，而不是父类中被重写的方法。
要想调用父类中被重写的方法，则必须使用关键字 `super`。

## Java 抽象类

在面向对象的概念中，所有的对象都是通过类来描绘的，但是反过来，并不是所有的类都是用来描绘对象的，如果一个类中没有包含足够的信息来描绘一个具体的对象，这样的类就是抽象类。
抽象类除了不能实例化对象之外，类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。
由于抽象类不能实例化对象，所以抽象类必须被继承，才能被使用。也是因为这个原因，通常在设计阶段决定要不要设计抽象类。
父类包含了子类集合的常见的方法，但是由于父类本身是抽象的，所以不能使用这些方法。
在 Java 中抽象类表示的是一种继承关系，一个类只能继承一个抽象类，而一个类却可以实现多个接口。

### 抽象类

在 Java 语言中使用 abstract class 来定义抽象类。如下实例：

    /* 文件名 : Employee.java */
    public abstract class Employee
    {
       private String name;
       private String address;
       private int number;
       public Employee(String name, String address, int number)
       {
          System.out.println("Constructing an Employee");
          this.name = name;
          this.address = address;
          this.number = number;
       }
       public double computePay()
       {
         System.out.println("Inside Employee computePay");
         return 0.0;
       }
       public void mailCheck()
       {
          System.out.println("Mailing a check to " + this.name
           + " " + this.address);
       }
       public String toString()
       {
          return name + " " + address + " " + number;
       }
       public String getName()
       {
          return name;
       }
       public String getAddress()
       {
          return address;
       }
       public void setAddress(String newAddress)
       {
          address = newAddress;
       }
       public int getNumber()
       {
         return number;
       }
    }

### 抽象方法

如果你想设计这样一个类，该类包含一个特别的成员方法，该方法的具体实现由它的子类确定，那么你可以在父类中声明该方法为抽象方法。
Abstract 关键字同样可以用来声明抽象方法，抽象方法只包含一个方法名，而没有方法体。
抽象方法没有定义，方法名后面直接跟一个分号，而不是花括号。

    public abstract class Employee
    {
       private String name;
       private String address;
       private int number;
       
       public abstract double computePay();
       
       //其余代码
    }

声明抽象方法会造成以下两个结果：
- 如果一个类包含抽象方法，那么该类必须是抽象类。
- 任何子类必须重写父类的抽象方法，或者声明自身为抽象类。

继承抽象方法的子类必须重写该方法。否则，该子类也必须声明为抽象类。最终，必须有子类实现该抽象方法，否则，从最初的父类到最终的子类都不能用来实例化对象

### 抽象类总结规定

- 1. 抽象类不能被实例化，如果被实例化，就会报错，编译无法通过。只有抽象类的非抽象子类可以创建对象。
- 2. 抽象类中不一定包含抽象方法，但是有抽象方法的类必定是抽象类。
- 3. 抽象类中的抽象方法只是声明，不包含方法体，就是不给出方法的具体实现也就是方法的具体功能。
- 4. 构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。
- 5. 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。

## Java 接口

接口（英文：Interface），在JAVA编程语言中是一个抽象类型，是抽象方法的集合，接口通常以interface来声明。一个类通过继承接口的方式，从而来继承接口的抽象方法。
接口并不是类，编写接口的方式和类很相似，但是它们属于不同的概念。类描述对象的属性和方法。接口则包含类要实现的方法。
除非实现接口的类是抽象类，否则该类要定义接口中的所有方法。
接口无法被实例化，但是可以被实现。一个实现接口的类，必须实现接口内所描述的所有方法，否则就必须声明为抽象类。另外，在 Java 中，接口类型可用来声明一个变量，他们可以成为一个空指针，或是被绑定在一个以此接口实现的对象。

### 接口与类相似点：

- 一个接口可以有多个方法。
- 接口文件保存在 .java 结尾的文件中，文件名使用接口名。
- 接口的字节码文件保存在 .class 结尾的文件中。
- 接口相应的字节码文件必须在与包名称相匹配的目录结构中。

### 接口与类的区别：

- 接口不能用于实例化对象。
- 接口没有构造方法。
- 接口中所有的方法必须是抽象方法，Java 8 之后 接口中可以使用 default 关键字修饰的非抽象方法。
- 接口不能包含成员变量，除了 static 和 final 变量。
- 接口不是被类继承了，而是要被类实现。
- 接口支持多继承。

### 接口特性

- 接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 **public abstract**（只能是 public abstract，其他修饰符都会报错）。
- 接口中可以含有变量，但是接口中的变量会被隐式的指定为 **public static final** 变量（并且只能是 public，用 private 修饰会报编译错误）。
- 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。

### 抽象类和接口的区别

- 1. 抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
- 2. 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 **public static final** 类型的。
- 3. 接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
- 4. 一个类只能继承一个抽象类，而一个类却可以实现多个接口。

### 接口的声明

Interface关键字用来声明一个接口。下面是接口声明的一个简单例子。

    /* 文件名 : NameOfInterface.java */
    import java.lang.*;
    //引入包
     
    public interface NameOfInterface
    {
       //任何类型 final, static 字段
       //抽象方法
    }

接口有以下特性：

- 接口是隐式抽象的，当声明一个接口的时候，不必使用**abstract**关键字。
- 接口中每一个方法也是隐式抽象的，声明时同样不需要**abstract**关键字。
- 接口中的方法都是公有的。

### 接口的实现

当类实现接口的时候，类要实现接口中所有的方法。否则，类必须声明为抽象的类。
类使用implements关键字实现接口。在类声明中，Implements关键字放在class声明后面。

#### 重写接口中声明的方法时，需要注意以下规则：

- 类在实现接口的方法时，不能抛出强制性异常，只能在接口中，或者继承接口的抽象类中抛出该强制性异常。
- 类在重写方法时要保持一致的方法名，并且应该保持相同或者相兼容的返回值类型。
- 如果实现接口的类是抽象类，那么就没必要实现该接口的方法。

#### 在实现接口的时候，也要注意一些规则：

- 一个类可以同时实现多个接口。
- 一个类只能继承一个类，但是能实现多个接口。
- 一个接口能继承另一个接口，这和类之间的继承比较相似。

### 接口的继承

一个接口能继承另一个接口，和类之间的继承方式比较相似。接口的继承使用extends关键字，子接口继承父接口的方法。

### 接口的多继承

在Java中，类的多继承是不合法，但接口允许多继承。

## Java 异常处理

异常是程序中的一些错误，但并不是所有的错误都是异常，并且错误有时候是可以避免的。
比如说，代码少了一个分号，那么运行出来结果是提示是错误 java.lang.Error；如果你用System.out.println(11/0)，那么是因为用0做了除数，会抛出 java.lang.ArithmeticException 的异常。

异常发生的原因有很多，通常包含以下几大类：

- 用户输入了非法数据。
- 要打开的文件不存在。
- 网络通信时连接中断，或者JVM内存溢出。

这些异常有的是因为用户错误引起，有的是程序错误引起的，还有其它一些是因为物理错误引起的。-  

要理解Java异常处理是如何工作的，需要掌握以下三种类型的异常：

- **检查性异常：**最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。
- **运行时异常：** 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。
- **错误：** 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。